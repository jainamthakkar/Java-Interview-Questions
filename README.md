# Java-Interview-Questions

## Java Platform

### 1. Why is Java so Popular?

**Answer:**
Two main reasons for popularity of Java are

1. Platform Independence
2. Object Oriented Language

### 2. What is Platform Independence?

**Answer:**

- Platform Independence is also called build once, run anywhere. Java is one of the most popular platform
  independent languages. Once we compile a java program and build a jar, we can run the jar (compiled
  java program) in any Operating System - where a JVM is installed.
- Java achieves Platform Independence in a beautiful way. On compiling a java file the output is a class file which contains an internal java representation called bytecode. JVM converts bytecode to executable
  instructions. The executable instructions are different in different operating systems. So, there are
  different JVM's for different operating systems. A JVM for windows is different from a JVM for mac.
  However, both the JVM's understand the bytecode and convert it to the executable code for the
  respective operating system.

### 3. What is ByteCode?

**Answer:**
Java bytecode is the instruction set of the Java virtual machine. Each bytecode is composed of one, or in
some cases two bytes that represent the instruction (opcode), along with zero or more bytes for passing
parameters.

### 4. Compare JDK vs JVM VS JRE.

**Answer:**

![alt text](imgs/image-1.png)

1. JVM
   a. Virtual machine that run the Java bytecode.
   b. Makes java portable.
2. JRE
   a. JVM + Libraries + Other Components (to run applets and other java applications)

3. JDK
   a. JRE + Compilers + Debuggers

### 5. What are the important differences between C++ and Java?

**Answer:**

1. Java is platform independent. C++ is not platform independent.
2. Java & C++ are both NOT pure Object Oriented Languages. However, Java is more purer Object
   Oriented Language (except for primitive variables). In C++, one can write structural programs
   without using objects.
3. C++ has pointers (access to internal memory). Java has no concept called pointers.
4. In C++, programmer has to handle memory management. A programmer has to write code to
   remove an object from memory. In Java, JVM takes care of removing objects from memory
   using a process called Garbage Collection.
5. C++ supports Multiple Inheritance. Java does not support Multiple Inheritance.

### 6. What is the role for a ClassLoader in Java?

**Answer:**
A Java program is made up of a number of custom classes (written by programmers like us) and core
classes (which come pre-packaged with Java). When a program is executed, JVM needs to load the
content of all the needed class. JVM uses a ClassLoader to find the classes.

Three Class Loaders are shown in the picture

- System Class Loader - Loads all classes from CLASSPATH
- Extension Class Loader - Loads all classes from extension directory
- Bootstrap Class Loader - Loads all the Java core files

When JVM needs to find a class, it starts with System Class Loader. If it is not found, it checks with
Extension Class Loader. If it not found, it goes to the Bootstrap Class Loader. If a class is still not found, a ClassNotFoundException is thrown.

## Wrapper Classes

### 7. What are wrapper classes?

**Answer:**
A primitive wrapper class in the Java programming language is one of eight classes provided in the
java.lang package to provide object methods for the eight primitive types. All of the primitive wrapper
classes in Java are immutable.

Wrapper: Boolean,Byte,Character,Double,Float,Integer,Long,Short

Primitive: boolean,byte,char ,double, float, int , long,short

### 8. Why do we need Wrapper Classes in Java?

**Answer:**
A wrapper class wraps (encloses) around a data type and gives it an object appearance.

Reasons why we need Wrapper Classes

- null is a possible value
- use it in a Collection
- Methods that support Object like creation from other types.. like String
- `Integer	number2 =	new Integer("55");//String`

### 9. What are the different ways of creating Wrapper Class Instances?

**Answer:**
Two ways of creating Wrapper Class Instances are described below.

1. Using a Wrapper Class Constructor

```
Integer	number =	new Integer(55);//int
Integer	number2 =	new Integer("55");//String
Float	number3 =	new Float(55.0);//double	argument
Float	number4 =	new Float(55.0f);//float	argument
Float	number5 =	new Float("55.0f");//String

Character	c1 =	new Character('C');//Only	char	constructor
//Character	c2	=	new	Character(124);//COMPILER	ERROR
Boolean	b =	new Boolean(true);
//"true"	"True"	"tRUe"	- all	String	Values	give	True

//Anything	else	gives	false
Boolean	b1 =	new Boolean("true");//value	stored	- true
Boolean	b2 =	new Boolean("True");//value	stored	- true
Boolean	b3 =	new Boolean("False");//value	stored	- false
Boolean	b4 =	new Boolean("SomeString");//value	stored	- false
```

2. valueOf Static Methods

Provide another way of creating a Wrapper Object

```
Integer	hundred =	Integer.valueOf("100");//100	is	stored	in	variable
Integer	seven	=	Integer.valueOf("111",	2);//binary	111	is	converted	to	7
```

### 10. What are differences in the two ways of creating Wrapper Classes?

**Answer:**

The difference is that using the Constructor you will always create a new object, while using valueOf()
static method, it may return you a cached value with-in a range.
For example : The cached values for long are between [-128 to 127].
We should prefer static valueOf method, because it may save you some memory. To understand it further,
here is an implementation of valueOf method in the Long class.

```
 /**
 * Returns an {@code Integer} instance representing the specified
 * {@code int} value. If a new {@code Integer} instance is not
 * required, this method should generally be used in preference to
 * the constructor {@link #Integer(int)}, as this method is likely
 * to yield significantly better space and time performance by
 * caching frequently requested values.
 *
 * This method will always cache values in the range -128 to 127,
 * inclusive, and may cache other values outside of this range.
 *
 * @param i an {@code int} value.
 * @return an {@code Integer} instance representing {@code i}.
 * @since 1.5
 */
 public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
}
```
