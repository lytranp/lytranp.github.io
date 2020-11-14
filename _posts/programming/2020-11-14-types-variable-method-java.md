---
layout: post
mathjax: true
title: "Types of variables and methods in Java"
read: 15
secondary: programming
date: 2020-11-13
---

**Situation**

Declaring variables and methods in Java might be confusing. That is the reason this post is written. 

## 1. Variable

**a. General syntax of variable declare**

Access Modifiers + Primitive Data Type + Variable name

                ```private int volumeLevel = 1;```

*Primitive Data Type*: byte, short, int, long, float, double, boolean, char

*Access Modifiers*: include 4 types (Default, Private, Public, Protected)

![](/sources/Programming-types-variable-method-java.png){:height="60%" width="60%"}

**Example:**
Here is the structure of a package. In a package, there are many classes. For example, in package myOOP, there are many classes.java. 

![](/sources/Programming-types-variable-method-java2.png){:height="60%" width="60%"}

Let's in class "BankAccount.java", we declare a variable

```
                    int test = 10; (a)
                    private int test1 = 10; (b)
                    public int test2 = 10; (c)
```

Let's say class "BankAccountMain.java" wants to call the variable "test" from "BankAccount.java"

+ (a): it is default (because no access modifier): It can be called within same package, but acts as private outside the package. Because "BankAccountMain.java" and "BankAccount.java" are at the same package, (a) and (c) can be called. 

+ (b): it is private, so it only works in the class "BankAccount.java"

+ (c): it is public, so it can work in another package (eg. default package)

**b. Call variable**

*Important note*: Access Modifiers only help us know where variable can be called. But declare variable with access modifiers is not enough if we want to call variable. We have to combine between *Access Modifiers* and *Types of variable* in order to call variable. So, we need to understand *Types of variable*. 

*Object-Oriented Programming (OOP):* Before mentioning about *Types of variable*, let's have quick review about main terms of OOP

![](/sources/Programming-types-variable-method-java3.png){:height="60%" width="60%"}

![](/sources/Programming-types-variable-method-java4.png){:height="60%" width="60%"}

*Types of variable*

![](/sources/Programming-types-variable-method-java5.png){:height="60%" width="60%"}

**Example**
+ Local variable: 
  
  + In the function "isPrime", divisor is a local variable that only works within this function. So, it is not necessary to declare private, or public. 
  
  + Usage: It is called directly in this function. 
   
                    ```System.out.println(divisor);```
  
![](/sources/Programming-types-variable-method-java6.png){:height="60%" width="60%"}

+ Instance variable: 
  
  + 5 first variables in class Airplane are instance variable. Each object is called will have different values for 5 first variables. If 1 object changes value of one of 5 variables, it does not affect on other objects. Values of 5 variables for other objects are not changed.

  + Usage: It is called through object. Meaning that we have to initialize the object first, then we can call instance variable

            ```
            Airplane newAirplane = new Airplane("AIRBUS", 320);
            newAirplane.model;
            ```

*Note*: Because model is private, so it can not be called outside of class. Actually, it should be called through a method of class "getModel()"

                    ```newAirplane.getModel();```

![](/sources/Programming-types-variable-method-java7.png){:height="60%" width="60%"}

+ Static variable: 
  
  + The last variable "private static int airfcraftCount" is a static variable because of "static" keyword. So, if the value of this variable changes, all of objects will have the same value for this variable.

  + Usage: It is called directly from class (without having to initialize object)

                    ```Airplane.aircraftCount;```


## 2. Function/Method
**a. General syntax of function declare**

Access Modifiers + Primitive Data Type + Function name ()

                    ```*public boolean deposit(double amount)*```
 
**Access Modifiers*: remain true to functions and methods

**b. Call function/method**

- Instance method: Firstly, we also have to initialize object. Then, we call method through object

```newAirplane.getModel();```

- Static method: We can call methods and functions directly from Class "AirPlane" (or call through object).

> ![](/sources/Programming-types-variable-method-java8.png){:height="60%" width="60%"}

>``` AirPlane.getAircraftCount(); or newAirplane.getAircraftCount();```









