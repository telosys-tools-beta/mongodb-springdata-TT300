# mongodb-springdata-TT300
MongoDB width Spring Data

# Sample

## Model (Telosys DSL)

```js
Employee {
	id : integer { @Id }; // the id
	firstName : string ;
	birthDate : date ;
	country 
}
```

```js
Country {
    code: string { @Id };
    label: string ;
}
```

## Generated files

### Entity beans

#### Employee.java
```java
/*
 * Java bean class
 * Created on 26 mars 2015 ( Date ISO 2015-03-26 - Time 13:48:26 )
 * Generated by Telosys Tools Generator ( version 2.1.1 )
 */

package org.demo.bean;

import java.io.Serializable;

import java.util.Date;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

/**
 * Entity bean
 *
 * @author Telosys Tools Generator
 *
 */
@Document(collection = "employees")
public class Employee implements Serializable
{
    private static final long serialVersionUID = 1L;

    private Date birthDate;
    private String firstName;
    @Id
    private Integer id;

    /**
     * Default constructor
     */
    public Employee()
    {
        super();
    }
    
    /**
     * Set the "birthDate" field value
     * @param birthDate
     */
    public void setBirthDate( Date birthDate )
    {
        this.birthDate = birthDate;
    }
        
    /**
     * Get the "birthDate" field value
     * @return the field value
     */
    public Date getBirthDate()
    {
        return this.birthDate;
    }
        
    /**
     * Set the "firstName" field value
     * @param firstName
     */
    public void setFirstName( String firstName )
    {
        this.firstName = firstName;
    }
        
    /**
     * Get the "firstName" field value
     * @return the field value
     */
    public String getFirstName()
    {
        return this.firstName;
    }
        
    /**
     * Set the "id" field value
     * @param id
     */
    public void setId( Integer id )
    {
        this.id = id;
    }
        
    /**
     * Get the "id" field value
     * @return the field value
     */
    public Integer getId()
    {
        return this.id;
    }
    
    public String toString() { 
        StringBuffer sb = new StringBuffer(); 
        sb.append(birthDate);
        sb.append("|");
        sb.append(firstName);
        sb.append("|");
        sb.append(id);
        return sb.toString(); 
    } 

}
```

#### Country.java
```java
/*
 * Java bean class
 * Created on 26 mars 2015 ( Date ISO 2015-03-26 - Time 13:48:27 )
 * Generated by Telosys Tools Generator ( version 2.1.1 )
 */

package org.demo.bean;

import java.io.Serializable;


import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

/**
 * Entity bean
 *
 * @author Telosys Tools Generator
 *
 */
@Document(collection = "countrys")
public class Country implements Serializable
{
    private static final long serialVersionUID = 1L;

    private String label;
    @Id
    private String code;

    /**
     * Default constructor
     */
    public Country()
    {
        super();
    }
    
    /**
     * Set the "label" field value
     * @param label
     */
    public void setLabel( String label )
    {
        this.label = label;
    }
        
    /**
     * Get the "label" field value
     * @return the field value
     */
    public String getLabel()
    {
        return this.label;
    }
        
    /**
     * Set the "code" field value
     * @param code
     */
    public void setCode( String code )
    {
        this.code = code;
    }
        
    /**
     * Get the "code" field value
     * @return the field value
     */
    public String getCode()
    {
        return this.code;
    }
    
    public String toString() { 
        StringBuffer sb = new StringBuffer(); 
        sb.append(label);
        sb.append("|");
        sb.append(code);
        return sb.toString(); 
    } 


}
```

### MongoDB Spring Data Repositories

#### EmployeeRepository.java
```java
/*
* Java bean class
* Created on 26 mars 2015 ( Date ISO 2015-03-26 - Time 13:48:26 )
* Generated by Telosys Tools Generator ( version 2.1.1 )
*/

package org.demo.repository;

import java.io.Serializable;

import java.util.Date;

import org.springframework.data.repository.PagingAndSortingRepository;
import org.demo.bean.Employee;

/**
 * Repository
 *
 * @author Telosys Tools Generator
 *
 */
public interface EmployeeRepository extends PagingAndSortingRepository<Employee, String>
{

}
```

#### CountryRepository.java
```java
/*
* Java bean class
* Created on 26 mars 2015 ( Date ISO 2015-03-26 - Time 13:48:27 )
* Generated by Telosys Tools Generator ( version 2.1.1 )
*/

package org.demo.repository;

import java.io.Serializable;


import org.springframework.data.repository.PagingAndSortingRepository;
import org.demo.bean.Country;

/**
 * Repository
 *
 * @author Telosys Tools Generator
 *
 */
public interface CountryRepository extends PagingAndSortingRepository<Country, String>
{

}
```

### Tests

#### EmployeeRepositoryTest.java
```java
/*
* Java bean class
* Created on 26 mars 2015 ( Date ISO 2015-03-26 - Time 13:48:27 )
* Generated by Telosys Tools Generator ( version 2.1.1 )
*/

package org.demo.repository;

import java.util.Date;

import com.mongodb.*;
import cz.jirutka.spring.embedmongo.EmbeddedMongoBuilder;
import org.demo.ApplicationConfigTest;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.SpringApplicationConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.beans.factory.annotation.Autowired;
import org.demo.bean.Employee;

import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

/**
 * Repository
 *
 * @author Telosys Tools Generator
 *
 */
@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = ApplicationConfigTest.class)
public class EmployeeRepositoryTest
{

    /**
     * Spring Data Repository
     */
    @Autowired
    EmployeeRepository employeeRepository;

    /**
     * MongoDB Java client
     */
    @Autowired
    Mongo mongo;

    /**
     * Initialize MongoDB with Java client
     */
    @Before
    public void setUp() throws Exception {

        // Drop database
        mongo.dropDatabase("test");

        // Create database
        DB db = mongo.getDB("test");

        // Documents collection
        DBCollection collection = db.getCollection("employees");
    }

    /**
     * Spring Data : Create and search Employee in MongoDB
     */
    @Test
    public void test() {
    
        Employee employee = new Employee();
        employee.setFirstName("Test");
        employee.setId(1);
        employeeRepository.save(employee);
        
        Iterable<Employee> employees = employeeRepository.findAll();
    
        System.out.println("Employees :");
        for(Employee employee2 : employees) {
            System.out.println(employee2);
        }

    }

    /**
     * Clean MongoDB with Java client
     */
    @After
    public void after() {

        // Create database
        DB db = mongo.getDB("test");
    
        // Documents collection
        DBCollection collection = db.getCollection("employees");
    
        // Results
        System.out.println("\nResult:");
        DBCursor cursor = collection.find();
        if(cursor.count() == 0) {
            System.out.println("<vide>");
        } else {
            while(cursor.hasNext()) {
                System.out.println(cursor.next());
            }
        }
        cursor.close();

        // Drop database
        mongo.dropDatabase("test");

    }

}
```

#### CountryRepositoryTest.java
```java
/*
* Java bean class
* Created on 26 mars 2015 ( Date ISO 2015-03-26 - Time 13:48:27 )
* Generated by Telosys Tools Generator ( version 2.1.1 )
*/

package org.demo.repository;


import com.mongodb.*;
import cz.jirutka.spring.embedmongo.EmbeddedMongoBuilder;
import org.demo.ApplicationConfigTest;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.SpringApplicationConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.beans.factory.annotation.Autowired;
import org.demo.bean.Country;

import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

/**
 * Repository
 *
 * @author Telosys Tools Generator
 *
 */
@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = ApplicationConfigTest.class)
public class CountryRepositoryTest
{

    /**
     * Spring Data Repository
     */
    @Autowired
    CountryRepository countryRepository;

    /**
     * MongoDB Java client
     */
    @Autowired
    Mongo mongo;

    /**
     * Initialize MongoDB with Java client
     */
    @Before
    public void setUp() throws Exception {

        // Drop database
        mongo.dropDatabase("test");

        // Create database
        DB db = mongo.getDB("test");

        // Documents collection
        DBCollection collection = db.getCollection("countrys");
    }

    /**
     * Spring Data : Create and search Country in MongoDB
     */
    @Test
    public void test() {
    
        Country country = new Country();
        country.setLabel("Test");
        country.setCode("Test");
        countryRepository.save(country);
        
        Iterable<Country> countrys = countryRepository.findAll();
    
        System.out.println("Countrys :");
        for(Country country2 : countrys) {
            System.out.println(country2);
        }

    }

    /**
     * Clean MongoDB with Java client
     */
    @After
    public void after() {

        // Create database
        DB db = mongo.getDB("test");
    
        // Documents collection
        DBCollection collection = db.getCollection("countrys");
    
        // Results
        System.out.println("\nResult:");
        DBCursor cursor = collection.find();
        if(cursor.count() == 0) {
            System.out.println("<vide>");
        } else {
            while(cursor.hasNext()) {
                System.out.println(cursor.next());
            }
        }
        cursor.close();

        // Drop database
        mongo.dropDatabase("test");

    }

}
```
