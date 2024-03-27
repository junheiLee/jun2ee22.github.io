---
layout: single
title: "JPA - AttributeConverter"
tag: etc
categories: etc
---
post by [chocolaggibbiddori](https://chocolaggibbiddori.github.io)

<br>
# JPA의 AttributeConverter 인터페이스 사용법

&nbsp;&nbsp; 프로젝트 진행 중 데이터를 암호화하여 저장해야하는 경우가 발생했다.
암호화, 복호화를 수행하는 메서드나 클래스를 만들면 되겠지만, 모든 서비스 로직에 암복호화 로직이 들어간다고 생각하니 너무 끔찍했다.
이 문제를 해결하기 위한 방법을 찾던 도중 JPA의 `AttributeConverter` 인터페이스를 알게 되어 기록하고자 한다.

<br>

## AttributeConverter

&nbsp;&nbsp; JPA가 엔티티의 필드와 RDB 테이블의 컬럼을 매핑할 때 사용하는 컨버터를 지정하는 인터페이스.
즉, JPA가 DB에 값을 넣거나 뺄 때 `AttributeConverter` 인터페이스를 구현한 객체를 컨버터로서 사용할 수 있다.

&nbsp;&nbsp; `AttributeConverter` 인터페이스는 다음과 같이 정의되어 있다.

```java
package javax.persistence;

/**
 * A class that implements this interface can be used to convert 
 * entity attribute state into database column representation 
 * and back again.
 * Note that the X and Y types may be the same Java type.
 *
 * @param <X>  the type of the entity attribute
 * @param <Y>  the type of the database column
 */
public interface AttributeConverter<X, Y> {

    /**
     * Converts the value stored in the entity attribute into the 
     * data representation to be stored in the database.
     *
     * @param attribute  the entity attribute value to be converted
     * @return the converted data to be stored in the database 
     *          column
     */
    public Y convertToDatabaseColumn(X attribute);

    /**
     * Converts the data stored in the database column into the 
     * value to be stored in the entity attribute.
     * Note that it is the responsibility of the converter writer to
     * specify the correct <code>dbData</code> type for the corresponding 
     * column for use by the JDBC driver: i.e., persistence providers are 
     * not expected to do such type conversion.
     *
     * @param dbData  the data from the database column to be 
     *                converted
     * @return the converted value to be stored in the entity 
     *          attribute
     */
    public X convertToEntityAttribute(Y dbData);
}
```

&nbsp;&nbsp; 여기서 X 타입은 엔티티의 필드 타입이고, Y 타입은 DB의 컬럼 타입이다.
메서드 명만 봐도 인터페이스의 역할이 대충 유추가 되는데, DB에 값을 넣을 때와 DB에서 값을 조회할 때 두 가지 경우에 데이터를 어떻게 변환할 지만 정해주면 된다.  
&nbsp;&nbsp; 우리 프로젝트에서는 위 인터페이스를 이용하여 암호화 및 복호화 작업을 수행하는 컨버터를 만들었다.

```java
import com.miracle.userservice.cypher.SymmetricCypher;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Component;

import javax.persistence.AttributeConverter;
import javax.persistence.Converter;

@RequiredArgsConstructor
@Component
@Converter
public class SymmetricCypherConverter implements AttributeConverter<String, String> {

    private final SymmetricCypher symmetricCypher;

    @Override
    public String convertToDatabaseColumn(String attribute) {
        return symmetricCypher.encrypt(attribute);
    }

    @Override
    public String convertToEntityAttribute(String dbData) {
        return symmetricCypher.decrypt(dbData);
    }
}
```

&nbsp;&nbsp; `@Converter` 어노테이션을 사용해 해당 클래스가 컨버터임을 명시한다. 그러면 JPA가 해당 컨버터를 사용해서 데이터를 변환해줄 수 있다.
`@Converter` 어노테이션에는 `boolean` 타입의 `autoApply()` 속성이 하나 있는데, 이 값을 `true`로 설정하게 되면 X 타입 필드에 자동으로 해당 컨버터를 적용하게 된다.
위와 같이 X 타입이 `String` 타입일 경우에는 모든 `String` 타입이 암호화가 될 것이므로, `autoApply()` 속성을 `false`로 설정하여 해당 컨버터가 동작하는 필드를 수동으로 적용하였다.

### @Convert

&nbsp;&nbsp; `@Convert` 어노테이션을 사용하여 엔티티 필드에 수동으로 컨버터를 지정해줄 수 있다.

```java
@Convert(converter = EmailConverter.class)
@Column(nullable = false, length = 50)
private String userEmail;

@Column(nullable = false, length = 30)
private String userName;

@Convert(converter = SymmetricCypherConverter.class)
@Column(nullable = false, length = 20)
private String userPhone;
```

&nbsp;&nbsp; 위 코드는 `ApplicationLetter` 엔티티의 일부를 발췌한 것인데, `userEmail` 필드와 `userPhone` 필드에 각각 컨버터가 적용되어 있다.
이를 통해 JPA가 `ApplicationLetter` 엔티티를 취급할 때 해당 필드들에 컨버터를 적용함으로써 서비스 로직마다 반복되는 작업들(예를 들어, 암호화 로직)을 한 번에 처리할 수 있게 되었다.

&nbsp;&nbsp; `@Converter` 어노테이션은 `converter()` 속성 말고도 두 개의 속성을 더 가지고 있고 해당 속성들을 통해 더 많은 역할을 수행할 수 있는데, 해당 부분은 아래 주석 예제를 통해 쉽게 이해할 수 있을 것이다.

```java
package javax.persistence;

import java.lang.annotation.Repeatable;
import java.lang.annotation.Target;
import java.lang.annotation.Retention;
import static java.lang.annotation.ElementType.TYPE;
import static java.lang.annotation.ElementType.METHOD;
import static java.lang.annotation.ElementType.FIELD;
import static java.lang.annotation.RetentionPolicy.RUNTIME;

/**
 *  ...
 *
 *  <pre>
 *     Example 1:  Convert a basic attribute
 *
 *     &#064;Converter
 *     public class BooleanToIntegerConverter 
 *        implements AttributeConverter&#060;Boolean, Integer&#062; {  ... }
 *
 *     &#064;Entity
 *     public class Employee {
 *         &#064;Id long id;
 *
 *         &#064;Convert(converter=BooleanToIntegerConverter.class)
 *          boolean fullTime;
 *          ...
 *     }
 *
 *
 *     Example 2:  Auto-apply conversion of a basic attribute
 *
 *     &#064;Converter(autoApply=true)
 *     public class EmployeeDateConverter 
 *        implements AttributeConverter&#060;com.acme.EmployeeDate, java.sql.Date&#062; {  ... }
 *
 *     &#064;Entity
 *     public class Employee {
 *         &#064;Id long id;
 *         ...
 *         // EmployeeDateConverter is applied automatically
 *         EmployeeDate startDate;
 *     }
 *
 *
 *     Example 3:  Disable conversion in the presence of an autoapply converter
 *
 *     &#064;Convert(disableConversion=true)
 *     EmployeeDate lastReview;
 *
 *
 *     Example 4:  Apply a converter to an element collection of basic type
 *
 *     &#064;ElementCollection
 *     // applies to each element in the collection
 *     &#064;Convert(converter=NameConverter.class) 
 *     List&#060;String&#062; names;
 *
 *
 *     Example 5:  Apply a converter to an element collection that is a map or basic values.  
 *                 The converter is applied to the map value.
 *
 *     &#064;ElementCollection
 *     &#064;Convert(converter=EmployeeNameConverter.class)
 *     Map&#060;String, String&#062; responsibilities;
 *
 *
 *     Example 6:  Apply a converter to a map key of basic type
 *
 *     &#064;OneToMany
 *     &#064;Convert(converter=ResponsibilityCodeConverter.class, 
 *              attributeName="key")
 *     Map&#060;String, Employee&#062; responsibilities;
 *
 *
 *     Example 7:  Apply a converter to an embeddable attribute
 *
 *     &#064;Embedded
 *     &#064;Convert(converter=CountryConverter.class, 
 *              attributeName="country")
 *     Address address;
 * 
 *
 *     Example 8:  Apply a converter to a nested embeddable attribute
 * 
 *     &#064;Embedded
 *     &#064;Convert(converter=CityConverter.class, 
 *              attributeName="region.city")
 *     Address address;
 *
 *
 *     Example 9:  Apply a converter to a nested attribute of an embeddable that is a map key 
 *                 of an element collection
 *
 *     &#064;Entity public class PropertyRecord {
 *          ...
 *         &#064;Convert(attributeName="key.region.city", 
 *                  converter=CityConverter.class)
 *         &#064;ElementCollection
 *         Map&#060;Address, PropertyInfo&#062; parcels;
 *     }
 *
 *
 *     Example 10: Apply a converter to an embeddable that is a map key for a relationship
 *
 *     &#064;OneToMany
 *     &#064;Convert(attributeName="key.jobType", 
 *              converter=ResponsibilityTypeConverter.class)
 *     Map&#060;Responsibility, Employee&#062; responsibilities;
 *
 *
 *     Example 11: Override conversion mappings for attributes inherited from a mapped superclass
 *
 *     &#064;Entity
 *         &#064;Converts({
 *            &#064;Convert(attributeName="startDate", 
 *                     converter=DateConverter.class),
 *            &#064;Convert(attributeName="endDate", 
 *                     converter=DateConverter.class)})
 *     public class FullTimeEmployee extends GenericEmployee { ... }
 *  </pre>
 *
 * ...
 */
@Repeatable(Converts.class)
@Target({METHOD, FIELD, TYPE}) @Retention(RUNTIME)
public @interface Convert {

    /**
     * Specifies the converter to be applied.  A value for this
     * element must be specified if multiple converters would
     * otherwise apply.
     */
    Class converter() default void.class;

    /**
     * The <code>attributeName</code> element must be specified unless the 
     * <code>Convert</code> annotation is on an attribute of basic type 
     * or on an element collection of basic type.  In these cases, the
     * <code>attributeName</code> element  must not be specified.
     */
    String attributeName() default "";

    /**
     * Used to disable an auto-apply or inherited converter.
     * If disableConversion is true, the <code>converter</code> element should
     * not be specified.
     */
    boolean disableConversion() default false;
}
```