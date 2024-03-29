# Java Revision Notes

---

[https://docs.oracle.com/javase/tutorial/reallybigindex.html](https://docs.oracle.com/javase/tutorial/reallybigindex.html)

[https://www.baeldung.com/java-tutorial](https://www.baeldung.com/java-tutorial)

### Java Compilation and Execution

**References**

[Complete Compilation Process of a Java Program](https://www.geeksforgeeks.org/compilation-execution-java-program/).

[How Java Compiler work](https://www.baeldung.com/java-compiled-interpreted) 

[JIT Deep Dive](https://www.baeldung.com/graal-java-jit-compiler)

[JVM Architecture](https://dzone.com/articles/jvm-architecture-explained)

Languages are classified based on abstraction level like high level languages(Java, C++, Go) and Low Level (Assembler).
High Level Codes Need to be translated in Machine Code(Low Level).

Java uses javac in built Java SDK compile tool to convert our source codes in Byte codes (.class File) which are native machine language code for JVM.

Compiled codes need to be rebuilt every time after code changes as it is platform CPU architecture dependent. 
Interpreted codes have no build step their codes. Interpreters operate on the source code of the program while executing it.

**Compiled languages tend to be faster than Interpreted codes, but with Just in Time Complier the gap is shrinking JIT compilers turn code from the interpreted language into machine native code as the program runs.**

Compiled Codes are Platform Specific whereas Interpreted codes are Platform Independent.

Java is Platform Independent as JVM is designed for different platforms and compiled codes are generated as bytes code which are executed by JVM.

> **JVM Architecture**
> 

The JVM is composed of five subsystems:

- **ClassLoader** ( Loads .class Files in JVM Memory)
Beside Loading it also perform various linking and initialization process like
Verifying the bytecode for any security breaches
Allocating memory for static variables
Replacing symbolic memory references with the original references
Assigning original values to static variables
Executing all static code blocks
- **JVM memory**
- **Execution engine**
Reads the byte code and convert to machine code and execute it
Since the *JVM* is platform-neutral, it *uses an* *interpreter to execute bytecode*
The *JIT compiler improves performance by compiling bytecode to native code for repeated method calls*
The Garbage collector collects and removes all unreferenced objects
The execution engine makes use of the Native method interface (JNI) to call native libraries and applications.
- **[Native method interface](https://www.baeldung.com/jni) and**
- **Native method library**

> **How Just in Time Compilation Works**
> 

Modern JVMs also have a JIT compiler. This means that the JVM optimizes our code at runtime.

The main disadvantage of an interpreter is that every time a method is called, it requires interpretation, which can be slower than compiled native code. Java makes use of the JIT compiler to overcome this issue.

The JIT compiler doesn't completely replace the interpreter. The execution engine still uses it. However, the JVM uses the JIT compiler based on how frequently a method is called.

The JIT compiler compiles the entire method's bytecode to machine native code, so it can be reused directly.

A profiler is a special component of the JIT compiler responsible for finding hotspots. The JVM decides which code to JIT compile based on the profiling information collected during runtime.

### Java Basics

*basic type*

- byte/8
- char/16
- short/16
- int/32
- float/32
- long/64
- double/64
- boolean/~

boolean has only two values: true and false, which can be stored in 1 bit, but the specific size is not clearly specified. The JVM will convert boolean type data to int at compile time, using 1 to represent true and 0 to represent false. JVM supports boolean array, but it is realized by reading and writing byte array.

c*omments* 

```java
Comments can be single line, multi line or documention comment
// a single line comment

/* 
		A multiline comment
*/

/**
		A Documentation Comment
*/
```

- Java does not provide low-level programming functionalities like pointers.
- Also, Java codes are always written in the form of classes and objects.
- Everything in Java should be in class and every class should be in independent file unless it’s inner class
- The name of class file should be exactly same as public class, however The name of the file can be a different name if it does not have any public class.
- Java is Case sensitive
- *Execution point of each java program is main method*
- Identifiers used to identify data/instructions points.
- Keywords define functionalities and literals define a value.
- The Java platform stores **character values using Unicode conventions.**
- Java cannot perform down casting implicitly, as this would result in loss of precision.
- Since the literal 1 is of type int, which has higher precision than short, the int cannot be implicitly downcast to short.
    
    ```java
    short s1 = 1;
    // s1 = s1 + 1;
    ```
    
    But using the += or ++ operators will perform an implicit type conversion.
    
    ```java
    s1 += 1;
    s1++;
    ```
    
    The above statement is equivalent to down casting the calculation result of s1 + 1:
    
    ```java
    s1 = (short) (s1 + 1);
    ```
    
    [why-dont-javas-compound-assignment-operators-require-casting](https://stackoverflow.com/questions/8710619/why-dont-javas-compound-assignment-operators-require-casting)
    
    For basic types, == judges whether two values are equal, and basic types do not have an equals() method.
    For reference types, == judges whether two variables refer to the same object, and equals() judges whether the referenced objects are equivalent.
    
    ***switch***
    
    Beginning with Java 7, String objects can be used in switch conditional statements.
    
    ```java
    String s = "a";
    switch (s) {
        case "a":
            System.out.println("aaa");
            break;
        case "b":
            System.out.println("bbb");
            break;
    }
    ```
    
    switch does not support long, float, double, because the original intention of switch is to judge the equivalence of those types with only a few values. If the value is too complicated, it is more appropriate to use if.
    
    ```java
    // long x = 111;
    // switch (x) { // Incompatible types. Found: 'long', required: 'char, byte, short, int, Character, Byte, Short, Integer, String, or an enum'
    //     case 111:
    //         System.out.println(111);
    //         break;
    //     case 222:
    //         System.out.println(222);
    //         break;
    // }
    ```
    
    **[StackOverflow : Why can't your switch statement data type be long, Java?](https://stackoverflow.com/questions/2676210/why-cant-your-switch-statement-data-type-be-long-java)**
    

*Wrapper Classes* **** 

- Classes which can wrap or contain a primitive data type.
- Autoboxing is conversion of a primitive datatype to wrapper class of it, Unboxing is reverse of it
- Wrapper Classes cannot be Inherited

### *cache pool*

The difference between new Integer(123) and Integer.valueOf(123) is:

- new Integer(123) creates a new object every time;
- Integer.valueOf(123) will use the object in the buffer pool, multiple calls will get the reference of the same object.
    
    ```java
    Integer x = new Integer(123);
    Integer y = new Integer(123);
    System.out.println(x == y);    // false
    Integer z = Integer.valueOf(123);
    Integer k = Integer.valueOf(123);
    System.out.println(z == k);   // true
    ```
    
    The implementation of the valueOf() method is relatively simple, which is to first judge whether the value is in the cache pool, and if so, directly return the content of the cache pool.
    
    ```java
    public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
    ```
    
    In Java 8, the size of the Integer buffer pool defaults to -128~127.
    
    ```java
    static final int low = -128;
    static final int high;
    static final Integer cache[];static {
        // high value may be configured by property
        int h = 127;
        String integerCacheHighPropValue =
            sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
        if (integerCacheHighPropValue != null) {
            try {
                int i = parseInt(integerCacheHighPropValue);
                i = Math.max(i, 127);
                // Maximum array size is Integer.MAX_VALUE
                h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
            } catch( NumberFormatException nfe) {
                // If the property cannot be parsed into an int, ignore it.
            }
        }
        high = h;
        cache = new Integer[(high - low) + 1];
        int j = low;
        for(int k = 0; k < cache.length; k++)
            cache[k] = new Integer(j++);// range [-128, 127] must be interned (JLS7 5.1.7)
        assert IntegerCache.high >= 127;
    }
    ```
    
    The compiler will call the valueOf() method during the autoboxing process, so multiple Integer instances with the same value and within the scope of the buffer pool are created using autoboxing, and they will refer to the same object.
    
    ```java
    Integer m = 123;
    Integer n = 123;
    System.out.println(m == n); // true
    ```
    
    The buffer pools corresponding to the basic types are as follows:
    
    - boolean values true and false
    - all byte values
    - short values between -128 and 127
    - int values between -128 and 127
    - char in the range \u0000 to \u007F
    
    When using the packaging types corresponding to these basic types, if the value range is within the scope of the buffer pool, you can directly use the objects in the buffer pool.
    
    Among all the numeric buffer pools in jdk 1.8, the Integer buffer pool IntegerCache is very special. The lower bound of this buffer pool is -128, and the upper bound is 127 by default, but this upper bound is adjustable. When starting the jvm, pass -XX:AutoBoxCacheMax=<size> to specify the size of the buffer pool, this option will set a system property named java.lang.IntegerCache.high when the JVM is initialized, and then IntegerCache will read the system property when it is initialized attribute to determine the upper bound.
    

### *Strings*

String is declared final, so it cannot be inherited. (Wrapper classes such as Integer cannot be inherited)

In Java 8, String internally uses a char array to store data.

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
}
```

After Java 9, the implementation of the String class uses a byte array to store strings instead, and uses to `coder`identify which encoding is used.

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final byte[] value;/** The identifier of the encoding used to encode the bytes in {@code value}. */
    private final byte coder;
}
```

The value array is declared final, which means that after the value array is initialized, it cannot refer to other arrays. And there is no method to change the value array inside String, so String can be guaranteed immutable.

### *Why String is Immutable in Java*

- It is made immutable for security purpose and memory usage enhancements.
- Since strings are immutable whenever we create a new same string, the JVM will first look into string constant pool a memory are that stores string literals. if any string literal matches it will create a new reference to same object thus saving heap memory.
- Strings are consider thread-safe implicitly. and can be used in multiple threads without synchronization.
- If we don’t make the String immutable, it will pose a serious security threat to the application. For example, database usernames, passwords are passed as strings to receive database connections. The socket programming host and port descriptions are also passed as strings. The String is immutable, so its value cannot be changed. If the String doesn’t remain immutable, any hacker can cause a security issue in the application by changing the reference value.

[more…](https://www.programcreek.com/2013/04/why-string-is-immutable-in-java/)

*String Buffer and String Builder*

String Builder and String Buffer both provides alternative for String Class and provides a mutable sequence of characters.
String Builder is preferred where performance is required, but it is not considered thread safe.
String Buffer is considered thread safe.

*A little bit about Array*

- A **Jagged Array** is an array of arrays such that member arrays can be of different sizes, i.e., we can create a 2-D array but with a variable number of columns in each row. These types of arrays are also known as Jagged arrays.
- **Final arrays ,** we can not make the final array refer to some other array but the data within an array that is made final can be changed/manipulated.

[util.Arrays vs reflect.Array](https://www.geeksforgeeks.org/util-arrays-vs-reflect-array-in-java-with-examples/)

- reflect.array class cannot be is immutable and provides method to work with arrays and is considered thread safe.
- util array can be extended and are not thread safe

### **String Pool**

- String constant pool (String Pool) saves all string literals (literal strings), these literals are determined at compile time. Not only that, but you can also use String's intern() method to add strings to the String Pool during operation.
- When a string calls the intern() method, if there is already a string in the String Pool that is equal to the value of the string (using the equals() method to determine), then a reference to the string in the String Pool will be returned; otherwise, A new string will be added to the String Pool and a reference to the new string will be returned.
- In the following example, s1 and s2 use new String() to create two different strings, while s3 and s4 obtain the same string reference through s1.intern() and s2.intern() methods. intern() puts "aaa" in the String Pool first, and then returns the string reference, so s3 and s4 refer to the same string.
    
    ```java
    String s1 = new String("aaa");
    String s2 = new String("aaa");
    System.out.println(s1 == s2);           // false
    String s3 = s1.intern();
    String s4 = s2.intern();
    System.out.println(s3 == s4);           // true
    ```
    
- If a string is created in the literal form of "bbb", the string will be automatically put into the String Pool.
    
    ```java
    String s5 = "bbb";
    String s6 = "bbb";
    System.out.println(s5 == s6);  // true
    ```
    
- Before Java 7, String Pool was placed in the runtime constant pool, which belonged to the permanent generation. And in Java 7, String Pool was moved to the heap. This is because the space of the permanent generation is limited, and OutOfMemoryError will occur in scenarios where a large number of strings are used.
    
    **[StackOverflow : What is String interning?(opens new window)](https://stackoverflow.com/questions/10578984/what-is-string-interning)**
    
    **[In-depth analysis of String#intern(opens new window)](https://tech.meituan.com/in_depth_understanding_string_intern.html)**
    

### **new String("abc")**

In this way, a total of two string objects will be created (provided that there is no "abc" string object in the String Pool).

- "abc" is a string literal, so a string object will be created in the String Pool during compilation, pointing to this "abc" string literal;
- The way to use new will create a string object in the heap.

Create a test class that uses this method in its main method to create string objects.

```java
public class NewStringTest {
    public static void main(String[] args) {
        String s = new String("abc");
    }
}
```

Decompile with javap -verbose and get the following:

```java
// ...
Constant pool:
// ...
   #2 = Class              #18            // java/lang/String
   #3 = String             #19            // abc
// ...
  #18 = Utf8               java/lang/String
  #19 = Utf8               abc
// ...public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=3, locals=2, args_size=1
         0: new           #2                  // class java/lang/String
         3: dup
         4: ldc           #3                  // String abc
         6: invokespecial #4                  // Method java/lang/String."<init>":(Ljava/lang/String;)V
         9: astore_1
// ...
```

In the Constant Pool, #19 stores the string literal "abc", and #3 is the string object of the String Pool, which points to the string literal of #19. In the main method, line 0: uses new #2 to create a string object in the heap, and uses ldc #3 to use the string object in the String Pool as a parameter of the String constructor.

The following is the source code of the String constructor. You can see that when a string object is used as the constructor parameter of another string object, the content of the value array will not be completely copied, but will all point to the same value array.

```java
public String(String original) {
    this.value = original.value;
    this.hash = original.hash;
}
```

*More on String* 

***String.intern,** String joiner and String tokenizer*

***[more here….](https://www.baeldung.com/string/intern)***

[https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value](https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value)

### Java Input / Output

[Link](https://www.baeldung.com/java-io)

There are different ways to create a file in Java

```java
// Using Files.createFile() From NIO Package
Path newFilePath = Paths.get(FILE_NAME);
Files.createFile(newFilePath);

// Using the java.io.File class
File newFile = new File(FILE_NAME);
boolean success = newFile.createNewFile();
assertTrue(success);

/*
	Using FileOutputStream
	In this case, a new file is created when we instantiate the FileOutputStream object.
	If a file with a given name already exists, it will be overwritten. 
	If, however, the existing file is a directory or a new file cannot be created 
	for any reason, then we'll get a FileNotFoundException
*/

try(FileOutputStream fileOutputStream = new FileOutputStream(FILE_NAME))
```

JDK has two sets of I/O packages:

1. the Standard I/O (in package `java.io`), introduced since JDK 1.0 for stream-based I/O, and
2. the New I/O (in packages `java.nio`), introduced in JDK 1.4, for more efficient buffer-based I/O.

### **Byte Streams**

Programs use *byte streams* to perform input and output of 8-bit bytes. There are many byte stream classes e.g. `[FileInputStream](https://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html)` and `[FileOutputStream](https://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html)`

One byte at a time, we can select the number of bytes to read as well.

### ****Character Streams****

Character stream I/O automatically translates this internal format to and from the local character set and is ready for internationalization without extra effort by the programmer

All character stream classes are descended from Reader and Writer. There are character stream classes that specialize in file I/O: FileReader and FileWriter.

The int variable holds a character value in its last 16 bits; in CopyBytes, the int variable holds a byte value in its last 8 bits.
There are two general-purpose byte-to-character "bridge" streams: InputStreamReader and OutputStreamWriter.

Character I/O usually occurs in bigger units than single characters. One common unit is the line A string of characters with a line terminator at the end. (Line)
A line terminator can be a carriage-return/line-feed sequence ("\r\n"), a single carriage-return ("\r"), or a single line-feed ("\n”)

### Buffered Streams

In Un-Buffered ways like above each read or write request is handled directly by the underlying OS. This can make a program much less efficient, since each such request often triggers disk access, network activity, or some other operation that is relatively expensive.

To reduce this kind of overhead, the Java platform implements buffered I/O streams.

Buffered input streams read data from a memory area known as a buffer; the native input API is called only when the buffer is empty. Similarly, buffered output streams write data to a buffer, and the native output API is called only when the buffer is full.

There are four buffered stream classes used to wrap unbuffered streams: `[BufferedInputStream](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedInputStream.html)`and `[BufferedOutputStream](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedOutputStream.html)`create buffered byte streams,while `[BufferedReader](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html)`and `[BufferedWriter](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedWriter.html)`create buffered character streams.

**Flushing Buffered Streams**
It often makes sense to write out a buffer at critical points, without waiting for it to fill. This is known as flushing the buffer.

Some buffered output classes support autoflush, specified by an optional constructor argument. When autoflush is enabled, certain key events cause the buffer to be flushed.
To flush a stream manually, invoke its flush method

### **Scanner**

Scanner are useful for breaking down formatted input into tokens and translating individual tokens according to their data type. By default, a scanner uses white space to separate tokens.
To use a different token separator, invoke scannerobject.useDelimiter().

**Input Output from Command Line**

For Input output from command line we use Standard Streams and Console

Standard Streams are : [System.in](http://System.in), System.out, System.err. all are Byte Stream.

[Syste](http://System.in)m.out and System.err uses `PrintStream`,`PrintStream`utilizes an internal character stream object to emulate many of the features of character streams.

[System.in](http://System.in) is byte stream purely so we have to use InputStreamReader to emulate character stream.

**System.Console**

It is more advance than standard stream, The Console object also provides input and output streams that are true character streams, through its reader and writer methods. It is used for securely reading passwords as it doesn’t echo it using method .readPassword()

readPassword returns a character array, not a String, so the password can be overwritten, removing it from memory as soon as it is no longer needed.

Before a program can use the Console, it must attempt to retrieve the Console object by invoking System.console(). If the Console object is available, this method returns it. If System.console returns NULL, then Console operations are not permitted, either because the OS doesn't support them or because the program was launched in a noninteractive environment.

Many More Method for Password like verify, change.

### Annotations

Annotation are like metadata that provide some information to the compilers. It is used as @annotation_name. It can be applied to declaration of program elements. Their are predefined as well as custom annotation we can create.

Annotation types are a form of interface.

Example of a annotation type.

```java
@Documented
@interface ClassPreamble {
   String author();
   String date();
   int currentRevision() default 1;
   String lastModified() default "N/A";
   String lastModifiedBy() default "N/A";
   // Note use of array
   String[] reviewers();
}

@ClassPreamble (
   author = "John Doe",
   date = "3/17/2002",
   currentRevision = 6,
   lastModified = "4/12/2004",
   lastModifiedBy = "Jane Doe",
   // Note array notation
   reviewers = {"Alice", "Bob", "Cindy"}
)
public class Generation3List extends Generation2List {

// class code goes here

}

Note: To make the information in @ClassPreamble appear in Javadoc-generated documentation, 
you must annotate the @ClassPreamble definition with the @Documented annotation

```

@Deprecated annotation indicates that the marked element is deprecated and should no longer be used. The compiler generates a warning whenever a program uses a method, class, or field with the @Deprecated annotation.

If a method marked with `@Override`fails to correctly override a method in one of its superclasses, the compiler generates an error.

A few examples of where types are used are class instance creation expressions (new), casts, implements clauses, and throws clauses. This form of annotation is called a type annotation.
Type annotations were created to support improved analysis of Java programs way of ensuring stronger type checking.

Example: **`@NonNull** String str;`

**Repeating Annotation** is when we use same annotation multiple times to a declaration or type.

For compatibility reasons, repeating annotations are stored in a container annotation that is automatically generated by the Java compiler. In order for the compiler to do this, two declarations are required in your code.

****Step 1: Declare a Repeatable Annotation Type****

```java
@Repeatable(Schedules.class)
public @interface Schedule {
  String dayOfMonth() default "first";
  String dayOfWeek() default "Mon";
  int hour() default 12;
}
```

The value of the @Repeatable meta-annotation, in parentheses, is the type of the container annotation that the Java compiler generates to store repeating annotations. In this example, the containing annotation type is Schedules, so repeating @Schedule annotations is stored in an @Schedules annotation.

I will throw compile time error if we don’t define annotation as repatable and use it repeadtely

**Step 2: Declare the Containing Annotation Type**

The containing annotation type must have a `value` element with an array type. The component type of the array type must be the repeatable annotation type. The declaration for the `Schedules` containing annotation type is the following:

`public @interface Schedules {
    Schedule[] value();
}`

There are several methods available in the Reflection API that can be used to retrieve annotations.

When designing an annotation type, you must consider the cardinality of annotations of that type. It is now possible to use an annotation zero times, once, or, if the annotation's type is marked as @Repeatable, more than once. It is also possible to restrict where an annotation type can be used by using the @Target meta-annotation.

### Packages

Packages are to keep related things classes and method together.

Packages should be name in all lower case and it’s good to use domain name.

we define a package by using `package package_name` at the top of  every source file which belong to that package.

### **Name Ambiguities**

If a member in one package shares its name with a member in another package and both packages are imported, you must refer to each member by its qualified name. For example, the `graphics` package defined a class named `Rectangle`. The `java.awt` package also contains a `Rectangle` class. If both `graphics` and `java.awt` have been imported, the following is ambiguous.

`Rectangle rect;`

In such a situation, you have to use the member's fully qualified name to indicate exactly which `Rectangle` class you want. For example,

`graphics.Rectangle rect;`

**Static Import**

The static import statement gives you a way to import the constants and static methods that you want to use so that you do not need to prefix the name of their class.

You can use the static import statement to import the static members of java.lang.Math so that you don't need to prefix the class name, `Math`. The static members of `Math` can be imported either individually:

`import **static** java.lang.Math.PI;`

or as a group:

`import **static** java.lang.Math.*;`

Once they have been imported, the static members can be used without qualification. For example, the previous code snippet would become:

`double r = cos(PI * theta);`

Todo: Managing Files and Class Variables in Java
[https://docs.oracle.com/javase/tutorial/java/package/managingfiles.html](https://docs.oracle.com/javase/tutorial/java/package/managingfiles.html) 

### **Generic Types**

A *generic type* is a generic class or interface that is parameterized over types.

A *generic class* is defined with the following format:

`class name<T1, T2, ..., Tn> { /* ... */ }`

The type parameter section, delimited by angle brackets (<>), follows the class name. It specifies the *type parameters* (also called *type variables*) T1, T2, ..., and Tn.

A type variable can be any **non-primitive** type you specify: any class type, any interface type, any array type, or even another type variable.

This same technique can be applied to create generic interfaces.

Convention is to use capital letters for type (’E’).

The most commonly used type parameter names are:

- E - Element (used extensively by the Java Collections Framework)
- K - Key
- N - Number
- T - Type
- V - Value
- S,U,V etc. - 2nd, 3rd, 4th types

*Difference between Type Parameter and Type Argument and how to instantiate generic types.* 

```java
class Box<T>{
	T variable_name;
	
	Box(){//Constructor}
	
	T get_variable_name(){}
}
```

How we instantiate it.

`Box<Integer> integerBox = new Box<Integer>();`

Here T is Type Parameter and Integer is Type argument.

In Java SE 7 and later, we can invoke the constructor of a generic class with an empty set of type arguments (<>) as long as the compiler can determine.

We can have Multiple Parameterized type and parmatrized type paramters as well in Generic Type.

```java
// Multiple Parameter Type
class example<E,T>{}

class example2<E,example<T>>{}
```

****Raw Types****

```java
public class Box<T> {
    public void set(T t) { /* ... */ }
    // ...
}
```

To create a parameterized type of Box<T>, you supply an actual type argument for the formal type parameter T:

`Box<Integer> intBox = new Box<>();`

If the actual type argument is omitted, you create a raw type of Box<T>:

`Box rawBox = new Box();`

Therefore, Box is the raw type of the generic type Box<T>

```java
//assigning a parameterized type to its raw type is allowed

Box<String> stringBox = new Box<>();
Box rawBox = stringBox;               // OK

// But if you assign a raw type to a parameterized type, you get a warning:

Box rawBox = new Box();           // rawBox is a raw type of Box<T>
Box<Integer> intBox = rawBox;     // warning: unchecked conversion

// You also get a warning if you use a raw type to invoke generic methods defined 
// in the corresponding generic type
```

[more..](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html)

****Generic Methods****

The syntax for a generic method includes a list of type parameters, inside angle brackets, which appears before the method's return type. For static generic methods, the type parameter section must appear before the method's return type.

```java
// The Util class includes a generic method, compare, which compares two Pair objects:

public class Util {
    public static <K, V> boolean compare(Pair<K, V> p1, Pair<K, V> p2) {
        return p1.getKey().equals(p2.getKey()) &&
               p1.getValue().equals(p2.getValue());
    }
}

public class Pair<K, V> {

    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public void setKey(K key) { this.key = key; }
    public void setValue(V value) { this.value = value; }
    public K getKey()   { return key; }
    public V getValue() { return value; }
}
// The complete syntax for invoking this method would be:

Pair<Integer, String> p1 = new Pair<>(1, "apple");
Pair<Integer, String> p2 = new Pair<>(2, "pear");
boolean same = Util.<Integer, String>compare(p1, p2);

// The type has been explicitly provided, as shown in bold. Generally, 
// this can be left out and the compiler will infer the type that is needed

Pair<Integer, String> p1 = new Pair<>(1, "apple");
Pair<Integer, String> p2 = new Pair<>(2, "pear");
boolean same = Util.compare(p1, p2);
```

*This feature, known as type inference, allows you to invoke a generic method as an ordinary method,*

Type Inference enables us to invoke a method without a type in <> brackets.
If we omit the type, Java compiler automatically infers from the method's arguments.

[More here](https://docs.oracle.com/javase/tutorial/java/generics/genTypeInference.html#:~:text=listOne%20%3D%20Collections.emptyList()%3B-,This%20statement%20is%20expecting%20an%20instance%20of%20List%3CString%3E%3B%20this,processStringList(Collections.emptyList())%3B,-See%20Target%20Typing)

**Bounded Type**

It is used when we want to restrict the type of parameters in Generic.

Bounded type parameters are key to the implementation of generic algorithms

```java
public <U extends Number> void inspect(U u){
        System.out.println("T: " + t.getClass().getName());
        System.out.println("U: " + u.getClass().getName());
    }

// Multiple Bound

Class A { /* ... */ }
interface B { /* ... */ }
interface C { /* ... */ }

class D <T extends A & B & C> { /* ... */ }

// Classes should be always first
```

Inheritance with Generics : [Read Here](https://docs.oracle.com/javase/tutorial/java/generics/inheritance.html)

### Concurrency

In concurrent programming, there are two basic units of execution: processes and threads

Processing time for a single core is shared among processes and threads through an OS feature called time slicing

### Processes

A process has a self-contained execution environment. A process generally has a complete, private set of basic run-time resources; in particular, each process has its own memory space.

Inter Process Communication (IPC) resources, such as pipes and sockets.
**Pipes : 
Sockets :**

### Threads

Threads are sometimes called lightweight processes. Both processes and threads provide an execution environment, but creating a new thread requires fewer resources than creating a new process.

Threads exist within a process — every process has at least one. Threads share the process's resources, including memory and open files.

***Defining Threads***

Create a class the implements Runnable and provide definition of run method.

Extend Thread Class and provide definition to run method.

Execution of Thread.
`thread.start()`

***Pause Thread with sleep method***

`threadobj.sleep(second)`

It takes value in nanoseconds

`threadobj.interrupt` will raise interrupted exception it is used to stop execution

**JOINS**

The `join` method allows one thread to wait for the completion of another. If `t` is a `Thread` object whose thread is currently executing,`t.join();`causes the current thread to pause execution until `t`'s thread terminates.

A simple Thread Program : [here](https://docs.oracle.com/javase/tutorial/essential/concurrency/simple.html)

### **Synchronization**

Threads communicate primarily by sharing access to fields and the objects reference fields refer to. This form of communication is extremely efficient, but makes two kinds of errors possible: *thread interference* and *memory consistency errors*. The tool needed to prevent these errors is *synchronization*.

However, synchronization can introduce *thread contention*, which occurs when two or more threads try to access the same resource simultaneously *and*
 cause the Java runtime to execute one or more threads more slowly, or even suspend their execution. [Starvation and livelock](https://docs.oracle.com/javase/tutorial/essential/concurrency/starvelive.html)
 are forms of thread contention.

### **Synchronization**

Two basic synchronization idioms: synchronized methods and synchronized statements.

### More on Synchronized

These methods synchronized has two effects:

- First, it is not possible for two invocations of synchronized methods on the same object to interleave. When one thread is executing a synchronized method for an object, all other threads that invoke synchronized methods for the same object block (suspend execution) until the first thread is done with the object.
- Second, when a synchronized method exits, it automatically establishes a happens-before relationship with *any subsequent invocation* of a synchronized method for the same object. This guarantees that changes to the state of the object are visible to all threads.

Note that constructors cannot be synchronized — using the `synchronized` keyword with a constructor is a syntax error. Synchronizing constructors doesn't make sense, because only the thread that creates an object should have access to it while it is being constructed.

---

**Warning:**

When constructing an object that will be shared between threads, be very careful that a reference to the object does not "leak" prematurely. For example, suppose you want to maintain a

```
List
```

called

```
instances
```

containing every instance of class. You might be tempted to add the following line to your constructor:

`instances.add(this);`

But then other threads can use

```
instances
```

to access the object before construction of the object is complete.

---

Synchronized methods enable a simple strategy for preventing thread interference and memory consistency errors: if an object is visible to more than one thread, all reads or writes to that object's variables are done through `synchronized` methods. (An important exception: `final` fields, which cannot be modified after the object is constructed, can be safely read through non-synchronized methods, once the object is constructed) This strategy is effective, but can present problems with [liveness](https://docs.oracle.com/javase/tutorial/essential/concurrency/liveness.html), as we'll see later in this lesson.

Synchronized Methods and Statement Syntax

```jsx
public class example{

	public synchronized void method_name() {
	        // More Codes
	    }
	
	synchronized(this){
				// More Codes
			}
}
```

whenever a synchronized method is called by a thread the intrinsic lock or monitor lock of that object get acquired by the thread.
until the thread release it no other thread can acquire it.

when a static synchronized method is invoked, since a static method is associated with a class, not an object.

Allowing a thread to acquire the same lock more than once enables ***re-entrant synchronization.***

an atomic action is one that effectively happens all at once. An atomic action cannot stop in the middle: it either happens completely, or it doesn't happen at all

`volatile variables` are thread safe.
`java.util.concurrent` package provide atomic methods that do not rely on synchronization

*Volatile Variables*

### Liveness

A concurrent application's ability to execute in a timely manner is known as its liveness.

Two common Liveness Problem are **Deadlock** and **Starvation** 

Starvation happens when a greedy thread holds and make frequent call to shared resources, that make other threads wait very long

**Live Lock**

When threads are too busy to answer other thread call.

**Dead Lock**

[High Level Concurrency Objects](https://docs.oracle.com/javase/tutorial/essential/concurrency/highlevel.html)

 In `java.util.concurrent` packages. There are also new concurrent data structures in the Java Collections Framework.

- [Lock objects](https://docs.oracle.com/javase/tutorial/essential/concurrency/newlocks.html) support locking idioms that simplify many concurrent applications.
- [Executors](https://docs.oracle.com/javase/tutorial/essential/concurrency/executors.html) define a high-level API for launching and managing threads. Executor implementations provided by `java.util.concurrent` provide thread pool management suitable for large-scale applications.
- [Concurrent collections](https://docs.oracle.com/javase/tutorial/essential/concurrency/collections.html) make it easier to manage large collections of data, and can greatly reduce the need for synchronization.
- [Atomic variables](https://docs.oracle.com/javase/tutorial/essential/concurrency/atomicvars.html) have features that minimize synchronization and help avoid memory consistency errors.
- `[ThreadLocalRandom](https://docs.oracle.com/javase/tutorial/essential/concurrency/threadlocalrandom.html)` (in JDK 7) provides efficient generation of pseudo-random numbers from multiple threads.

***Lock Objects :*** Lock objects work very much like the implicit locks used by synchronized code.

The biggest advantage of Lock objects over implicit locks is their ability to back out of an attempt to acquire a lock. The tryLock method backs out if the lock is not available immediately or before a timeout expires (if specified). The lockInterruptibly method backs out if another thread sends an interrupt before the lock is acquired.

In Small Application we can work with Runnable and Thread class for thread management, but in Large Application we can use a separate thread management and creation. Objects that encapsulate these functions are known as ***executors**.*

The `java.util.concurrent` package defines three executor interfaces:

- `Executor`, a simple interface that supports launching new tasks.
- `ExecutorService`, a subinterface of `Executor`, which adds features that help manage the life cycle, both of the individual tasks and of the executor itself.
- `ScheduledExecutorService`, a subinterface of `ExecutorService`, supports future and/or periodic execution of tasks.

Executor takes a runnable and callable object and run it with already existing thread object.
It will wait for the thread to be available unlike the thread.start() way which create a new thread and execute.

Most of the executor implementations in java.util.concurrent use thread pools, which consist of worker threads. This kind of thread exists separately from the Runnable and Callable tasks it executes and is often used to execute multiple tasks.

One common type of thread pool is the fixed thread pool. This type of pool always has a specified number of threads running; if a thread is somehow terminated while it is still in use, it is automatically replaced with a new thread. Tasks are submitted to the pool via an internal queue, which holds extra tasks whenever there are more active tasks than threads.

An important advantage of the fixed thread pool is that applications using it *degrade gracefully*
. To understand this, consider a web server application where each HTTP request is handled by a separate thread. If the application simply creates a new thread for every new HTTP request, and the system receives more requests than it can handle immediately, the application will suddenly stop responding to *all*
 requests when the overhead of all those threads exceed the capacity of the system. With a limit on the number of the threads that can be created, the application will not be servicing HTTP requests as quickly as they come in, but it will be servicing them as quickly as the system can sustain.

### **Constructors in Java**

Constructor cannot be final, static or abstract. it will throw modifier not allowed here error.

A constructor is not inherited by child class, and cannot be overridden.

We can overload constructor but we need to define default constructor also, Java only define constructor when we don’t define any by our self.

**Private Constructor**

If we declare a class constructor private, we cannot subclass it also cannot create it’s object outside the class. it follows singleton design pattern.

Yes. Constructors in Java can be private. All classes including abstract classes can have private constructors. Using private constructors we can prevent the class from being instantiated or we can limit the number of objects of that class.

**Static Constructor**

We cannot have static constructor

We cannot use `this` , `super`on static context

We cannot extend a class having no default constructor, to extend such class we need to call the base class parametrized constructor in base class constructor.

private static fields can be accessed through private static methods of the class.

**Final Constructors**

When there is no chance of constructor overriding, there is no chance of modification also. When there is no chance of modification, then no sense of restricting modification there. We know that the final keyword restricts further modification.

**Final Methods**

Final Methods cannot be Overridden

***Can we Overload Static Methods?***

Yes we can have more than one definition of static methods with different signature in a class.

***Can we have a static method and a non static method with same name and same signature?***

No we cannot it will throw already defined error

We can have with different signature, with different parameters

### OOP Concepts

## **Encapsulation**

Bundling code into individual software objects provides a number of benefits, including:

- Modularity: The source code for an object can be written and maintained independently of the source code for other objects. Once created, an object can be easily passed around inside the system.
- Information-hiding: By interacting only with an object's methods, the details of its internal implementation remain hidden from the outside world.
- Code re-use: If an object already exists (perhaps written by another software developer), you can use that object in your program. This allows specialists to implement/test/debug complex, task-specific objects, which you can then trust to run in your own code.
- Pluggability and debugging ease: If a particular object turns out to be problematic, you can simply remove it from your application and plug in a different object as its replacement. This is analogous to fixing mechanical problems in the real world. If a bolt breaks, you replace it, not the entire machine.

What Is an Object?

- An object is a software bundle of related state and behaviour.
- Software objects are often used to model the real-world objects that you find in everyday life.

****[What Is a Class?](https://docs.oracle.com/javase/tutorial/java/concepts/class.html)**

- class that models the state and behaviour of a real-world object
- A class is a blueprint or prototype from which objects are created

```java
// Declaration Syntax
public class classname Extends parentclassname
implements interface1name,interface2name, ....{
  .................
  .................
}
```

- *Parameters are passed as value*
- Java is always Pass by value.

To Achieve Pass by Reference:

- Use Class member to store value
- Use Collection object array, list etc
- return modified value and store it in same variable

We can create a fully encapsulated class in Java by making all the data members of the class private

Read-Only Class : Private members with getter methods only

Write-Only Class : Private members with setter methods only

Variable Arguments in Java

```java
public class methodname(dataype... parametername){
    // parametername will be an array of datatype
}
```

*Access Modifiers*

| Access Modifier | Within Class | Within Package | Outside Package by subclass only | Outside Package |
| --- | --- | --- | --- | --- |
| Private | Y | N | N | N |
| Default | Y | Y | N | N |
| Protected | Y | Y | Y | N |
| Public | Y | Y | Y | Y |

***this*** is a reference to current object and ***super*** is a reference to parent object

***static*** keyword is used to create fields and methods that belong to the class, rather than to an instance of the class.

***final*** is used to create constant fields

- Final class cannot be extended
- Final methods cannot be overridden.
- We cannot make an interface final in Java.

**Final Methods and Classes**

- Final Methods cannot be Overridden
- Final Classes cannot be extended.

***Tip:*** we should declare methods used in constructor to be final so any user cannot be override it ,If a constructor calls a non-final method, a subclass may redefine that method with surprising or undesirable results.

*A class that is declared final cannot be sub classed. This is particularly useful, for example, when creating an immutable class like the String class.*

Constructor

- Overloading a Constructor
    
    Yes we can overload constructors.
    
- Overriding a Constructor
    
    Constructor is not inherited, and cannot be overridden.
    

- Private, Protected , Public and Default Constructors.

- static constructor
    
    Nothing like static constructor in java
    

- final constructor
    
    Nothing like final constructor in java
    

Object class is superclass, Every class is a descendant, direct or indirect, of the `Object` class, It have some in-built methods which are inherited by default in all class.

- `protected Object clone() throws CloneNotSupportedException` Creates and returns a copy of this object.
- `public boolean equals(Object obj)` Indicates whether some other object is "equal to" this one.
- `protected void finalize() throws Throwable` Called by the garbage collector on an object when garbage collection determines that there are no more references to the object
- `public final Class getClass()` Returns the runtime class of an object.
- `public int hashCode()` Returns a hash code value for the object.
- `public String toString()` Returns a string representation of the object.

### **enum**

- enum define a class (enum type)
- enum body can contain variables and methods but constants should be define first.
- We can add a constructor in enum
    
    ```java
    public enum Planet {
        MERCURY (3.303e+23, 2.4397e6),
        VENUS   (4.869e+24, 6.0518e6),
        EARTH   (5.976e+24, 6.37814e6),
        MARS    (6.421e+23, 3.3972e6),
        JUPITER (1.9e+27,   7.1492e7),
        SATURN  (5.688e+26, 6.0268e7),
        URANUS  (8.686e+25, 2.5559e7),
        NEPTUNE (1.024e+26, 2.4746e7);
    
        private final double mass;   // in kilograms
        private final double radius; // in meters
        Planet(double mass, double radius) {
            this.mass = mass;
            this.radius = radius;
        }
        private double mass() { return mass; }
        private double radius() { return radius; }
    
        // universal gravitational constant  (m3 kg-1 s-2)
        public static final double G = 6.67300E-11;
    
        double surfaceGravity() {
            return G * mass / (radius * radius);
        }
        double surfaceWeight(double otherMass) {
            return otherMass * surfaceGravity();
        }
        public static void main(String[] args) {
            if (args.length != 1) {
                System.err.println("Usage: java Planet <earth_weight>");
                System.exit(-1);
            }
            double earthWeight = Double.parseDouble(args[0]);
            double mass = earthWeight/EARTH.surfaceGravity();
            for (Planet p : Planet.values())
               System.out.printf("Your weight on %s is %f%n",
                                 p, p.surfaceWeight(mass));
        }
    }
    ```
    

It is possible to assign an object of one type to an object of another type provided that the types are compatible

**Static Initialization Blocks**

- A static initialization block is a normal block of code enclosed in braces, { }, and preceded by the static keyword.

```jsx
static {
// whatever code is needed for initialization goes here
}
```

- A class can have any number of static initialization blocks, and they can appear anywhere in the class body. The runtime system guarantees that static initialization blocks are called in the order that they appear in the source code.
- The advantage of private static methods is that they can be reused later if you need to reinitialize the class variable.

**Instance Initialization Blocks**

***Two ways to initialize instance variables :***

**Initializer blocks** 

```java
public class classname{
	{
		// Initalizer Block
	}
}
```

By default Java Copies all initializer blocks inside the constructor

**Final methods**

```java
class Whatever {
private varType myVar = initializeInstanceVariable();
		protected final varType initializeInstanceVariable() {
				// initialization code goes here
		}
}

```

This is especially useful if subclasses might want to reuse the initialization method.

### **[Nested Classes](https://www.geeksforgeeks.org/inner-class-java/)**

Nested classes are divided into two categories: non-static and static. Non-static nested classes are called inner classes. Nested classes that are declared static are called static nested classes.

**Inner Classes**

- Inner class is associated with an instance of outer class
- It cannot define any static members itself

Two Types of Inner Classes are local classes and anonymous classes.

**Local Classes**

- Local classes are classes that are defined in a *block.* Mostly Found inside method body.
Local classes are similar to inner classes because they cannot define or declare any static members. Local classes are non-static because they have access to instance members of the enclosing block.
- A local class can have static members provided that they are constant variables.

**Anonymous Classes**

This are similar to inner classes, except name.

```java
// An anonymous class with HelloWorld as Base class
HelloWorld frenchGreeting = new HelloWorld() {
            String name = "tout le monde";
            public void greet() {
                greetSomeone("tout le monde");
            }
            public void greetSomeone(String someone) {
                name = someone;
                System.out.println("Salut " + name);
            }
        };
```

## **Accessing Local Variables of the Enclosing Scope, and Declaring and Accessing Members of the Anonymous Class**

Like local classes, anonymous classes can [capture variables](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html#accessing-members-of-an-enclosing-class); they have the same access to local variables of the enclosing scope:

- An anonymous class has access to the members of its enclosing class.
- An anonymous class cannot access local variables in its enclosing scope that are not declared as `final` or effectively final.
- Like a nested class, a declaration of a type (such as a variable) in an anonymous class shadows any other declarations in the enclosing scope that have the same name. See [Shadowing](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html#shadowing) for more information.

Anonymous classes also have the same restrictions as local classes with respect to their members:

- You cannot declare static initializers or member interfaces in an anonymous class.
- An anonymous class can have static members provided that they are constant variables.

Note that you can declare the following in anonymous classes:

- Fields
- Extra methods (even if they do not implement any methods of the supertype)
- Instance initializers
- Local classes

**Static Nested Class [Todo]**

1. **Static Nested Class**:
    - Visibility of members: A static nested class can access only the static members (fields and methods) of its enclosing class.
    - Accessibility from enclosing class: It can be accessed directly from the enclosing class, just like any other static member.
    - Accessibility from other classes: It can be accessed using the enclosing class name (e.g., **`EnclosingClass.StaticNestedClass`**) from other classes, but only public or package-private members are accessible.
2. **Non-Static Nested Class (Inner Class)**:
    - Visibility of members: An inner class can access both static and non-static members (fields and methods) of its enclosing class.
    - Accessibility from enclosing class: It can be accessed directly from the enclosing class, just like any other member.
    - Accessibility from other classes: An instance of an inner class is associated with an instance of the enclosing class. Accessing it from other classes typically requires an instance of the enclosing class. Inner classes can access private members of the enclosing class.
3. **Local Inner Class** (Defined inside a method):
    - Visibility of members: Similar to non-static inner classes, local inner classes can access both static and non-static members of their enclosing method and enclosing class.
    - Accessibility from enclosing method and class: They can be accessed directly from the enclosing method and class.
    - Accessibility from other classes: Local inner classes are not directly accessible from other classes, as they are scoped to the enclosing method. However, if you return an instance of the local inner class from the method, it can be used in other classes.
4. **Anonymous Inner Class**:
    - Visibility of members: Anonymous inner classes can access both static and non-static members of their enclosing class, similar to regular inner classes.
    - Accessibility from enclosing class: They can be accessed directly from the enclosing class.
    - Accessibility from other classes: Anonymous inner classes are typically used for short-lived, single-use instances and are not directly accessible from other classes.

Inheritance has the following effects on nested classes in Java:

- Nested classes (static and non-static) are inherited along with the outer class when a subclass is created.
- Inner classes (non-static) have an implicit reference to the outer class, and this reference is also inherited.
- Static nested classes do not inherit any reference to the outer class.
- Inner classes can be shadowed by subclasses if they are redefined with the same name.
- Subclasses can access public and protected members of inherited nested classes.
- The visibility of nested classes in a subclass is determined by their access modifiers.
- Subclasses can create instances of nested classes and use them.

<aside>
💡 Access Modifier effects on Nested Classes

</aside>

<aside>
💡 Inheritance effects on Nested classes

</aside>

<aside>
💡 Difference between member variable and Instance Variable

</aside>

### Package

Advantage of Java Package

1. Java package is used to categorize the classes and interfaces so that they can be easily maintained.
2. Java package provides access protection.
3. Java package removes naming collision.

If you import a package, all the classes and interface of that package will be imported excluding the classes and interfaces of the sub packages. Hence, you need to import the sub package as well.

<aside>
💡 Accessing members with different access modifier from different level of packages

</aside>

<aside>
💡 Inheritance effects on packages

</aside>

## **Inheritance**

- A subclass owns all the properties and methods of the parent class object (including private properties and private methods), but the private properties and methods in the parent class are inaccessible and **only owned**.
- A nested class has access to all the private members of its enclosing class—both fields and methods. Therefore, a public or protected nested class inherited by a subclass has indirect access to all of the private members of the superclass.

*5 Types of Inheritance*

- Single Inheritance
- Multi-Level Inheritance
- Multiple Inheritance ( Through Interfaces)
- Hybrid Inheritance (many to one)
- Hierarchical Inheritance ( one to many )

Usually the default constructor of the parent class is called.

**Instance Methods in Subclass**

- Instance methods can be override with same name, same method signature and same return type.
- Instance methods in subclass can return subtype of parent method return type this is called *covariant return type*
- when overriding a class we use @override annotation, if superclass doesn’t have it it will raise compile time error

**Static Methods in Subclass**

If a subclass defines a static method with the same signature as a static method in the superclass, then the method in the subclass hides the one in the superclass.

The distinction between hiding a static method and overriding an instance method has important implications:

- The version of the overridden instance method that gets invoked is the one in the subclass.
- The version of the hidden static method that gets invoked depends on whether it is invoked from the superclass or the subclass.

Static Method

Is Static Method Inherited?

No

Hiding parent Static Method?

We can hide a parent class's static method in a subclass by declaring a static method with the same name in the subclass.

Method hiding does not follow the polymorphic behaviour associated with method overriding for instance methods.

Can we make a class static?

The concept of static typically applies to methods, fields, or nested classes within a class

Can we directly access parent static method in child class

yes we can directly access parent static method without using parent reference in child class.

**Virtual Method Invocation**

When we override methods in child classes, irrespective of the variable type the method invoked will be from the object type.

```java
Dog dog = new GSD();
Dog dog2 = new Dog();

// Here method called will be from GSD if overridden otherwise from Dog.
dog.method();

// Here method called will be from GSD if overridden otherwise from Dog.
dog2.method();

GSD dog3 = new Dog(); //Error we cannot convert from child to parent type.
```

If Variables in parent class and child class are with same name irrespective of type we can access variable from parent class using super keyword

Does Private member of parent class get inherited?

In Java, private members of a parent class are not visible or accessible in child classes

Does Protected member accessible if we extend a class outside package?

Yes, but methods with default access modifier are not accessible in subclass outside package

Can we assign a child object to parent variable and vice versa?

It’s possible to assigning a child object to a parent variable without casting because it's always a valid relationship, but assigning a parent object to a child variable requires explicit casting and should be done carefully to avoid runtime errors

What will be order of call chain made for multiple constructor in same class and child class?

The constructor chaining continues down the class hierarchy, with each constructor calling its immediate superclass constructor using super() or relying on the default superclass constructor if not explicitly called.

***Diamond Problem***

The diamond problem occurs when a class inherits from two or more classes that have a common ancestor. This common ancestor's methods or attributes become ambiguous because the inheriting class doesn't know which implementation to use. Here's a simplified example of the diamond problem:

```css
cssCopy code
      A
     / \
    B   C
     \ /
      D

```

In this diagram, class **`D`** inherits from both classes **`B`** and **`C`**, which themselves inherit from class **`A`**. If both **`B`** and **`C`** have methods or attributes with the same name, it becomes ambiguous in **`D`**.

In Java, this problem is avoided through a mechanism called "interface inheritance" and "method overriding." In Java:

1. A class can implement multiple interfaces, allowing it to inherit multiple sets of method signatures without conflict.
2. If a class inherits from two interfaces that have methods with the same signature, it's the responsibility of the class to provide an implementation for that method, resolving the ambiguity.

Java's approach to inheritance and interface implementation is designed to prevent the diamond problem by requiring explicit method implementations and providing a clear mechanism for resolving conflicts when they arise.

There are two levels of access control:

- At the top level—`public`, or *package-private* (no explicit modifier).(in classes)
- At the member level—`public`, `private`, `protected`, or *package-private* (no explicit modifier).

Protected access is almost identical to default access. But with one critical exception. Protected access allows subclasses to inherit the protected members even if those subclasses are outside the package of the superclass they extend.

[For a subclass outside the package, the protected member can be accessed only through inheritance and not by parent class reference’](https://www.bogotobogo.com/Java/tutorials/defaultandprotected.php)

- Inheritance (Is-A), 
- Assertation (Has-a), 
- Composition(Part-of)

### ***Association***

Association is relation of a class with another which establishes through their Objects.

Association can be one-to-one, one-to-many, many-to-one, many-to-many.

Two types of Association

Aggregation (Has-A): It’s Unidirectional, one class can have object of other class.

Composition (Part-of): one class is a type of another class or part of another class

**Aggregation**

- It represents Has-A’s relationship.
- It is a unidirectional association i.e. a one-way relationship. For example, a department can have students but vice versa is not possible and thus unidirectional in nature.
- In Aggregation, both entries can survive individually which means ending one entity will not affect the other entity.

**Composition**

Composition is a restricted form of Aggregation in which two entities are highly dependent on each other.

- It represents part-of relationship.
- In composition, both entities are dependent on each other.
- When there is a composition between two entities, the composed object cannot exist without the other entity.

Composition is a strong Association whereas Aggregation is a weak Association.

Inheritance should be used only if the relationship is-a is maintained throughout the lifetime of the objects involved; otherwise, aggregation is the best choice.

## Polymorphism

Performing a single task in different ways. A single interface having multiple implementations is also called polymorphism.

Polymorphism in Java can be achieved in two ways i.e., method overloading and method overriding.

Polymorphism in Java is mainly divided into two types.

- Compile-time polymorphism
- Runtime polymorphism

Compile-time polymorphism can be achieved by method overloading, and Runtime polymorphism can be achieved by method overriding.

Compile Time polymorphism is also called Static method dispatch.

Runtime polymorphism is also called Dynamic method dispatch.

The two forms of polymorphism can be implemented in Java: inheritance (the overriding of the same method by multiple subclasses) and interfaces (implementing an interface and overriding the same method in an interface).

***Overloading***

A class can have multiple methods of the same name, and each method can be differentiated either by bypassing different types of parameters or bypassing a different number of parameters.

***Overriding***

In order to satisfy the Li style substitution principle, rewriting has the following three restrictions:

- The access rights of the subclass method must be greater than or equal to the parent class method.
- The return type of the subclass method must be the return type of the superclass method or its subtype.
- The exception type thrown by the subclass method must be the exception type thrown by the parent class or its subtype.

Existing in the same class means that a method has the same name as an existing method, but at least one parameter type, number, and order are different.

It should be noted that the return value is different, but everything else is the same is not overloading.

***Overload***

<aside>
💡 What are part of method signature and how we can have multiple method signature with same method name?

</aside>

<aside>
💡 How methods differentiate on Overloading?

</aside>

<aside>
💡 What is Method Signature and how it differentiate ?

</aside>

<aside>
💡 Can we Overload  Constructor?

Yes we can

</aside>

<aside>
💡 Can we overload static method?

Yes, you can overload static methods in Java just like you can overload instance methods.

</aside>

<aside>
💡 Can we overload default and static method in interface?

Yes, you can overload both default and static methods in an interface in Java.

</aside>

***Override***

<aside>
💡 Calling a Overridden Method from parent and child type variables.

```java
public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();
        Child child = new Child();

        parent.display(); // Calls the display method of the Parent class.
        child.display();  // Calls the overridden display method of the Child class.

        // Using parent type variable to call the overridden method in Child class.
        Parent parentRefToChild = new Child();
        parentRefToChild.display(); // Calls the overridden display method of the Child class.

        // Using child type variable to call the overridden method in Parent class.
        Child childRefToParent = new Parent(); // This is not common but technically allowed.
        childRefToParent.display(); // Calls the display method of the Parent class.
    }
}

```

Here's what happens in each case:

1. **`parent.display()`**: Calls the **`display`** method of the **`Parent`** class because the variable is of type **`Parent`**.
2. **`child.display()`**: Calls the overridden **`display`** method of the **`Child`** class because the variable is of type **`Child`**.
3. **`parentRefToChild.display()`**: Calls the overridden **`display`** method of the **`Child`** class. This is known as runtime polymorphism or dynamic method dispatch because it's determined by the actual object type at runtime.
4. **`childRefToParent.display()`**: Calls the **`display`** method of the **`Parent`** class because the variable is of type **`Child`**, but it's referencing an instance of the **`Parent`** class. This is technically allowed but not common or recommended because it can lead to confusion. The method called depends on the reference type, not the object's actual type.
</aside>

***Dynamic method lookup***

Dynamic method lookup, also known as dynamic method dispatch, is a mechanism in object-oriented programming languages like Java that allows the selection of which method to call at runtime, based on the actual object type rather than the reference type.

## Abstraction

## **Interface**

- An Interface in Java programming language is defined as an abstract type used to specify the behaviour of a class.
- It is used to achieve abstraction and multiple inheritance in Java.
- An interface is an extension of an abstract class. Before Java 8, it can be regarded as a completely abstract class, which means it cannot have any method implementation.
- Starting with Java 8, interfaces can also have default method implementations, because interfaces that do not support default methods are too expensive to maintain. Before Java 8, if an interface wanted to add a new method, then all classes implementing the interface had to be modified so that they all implement the new method.
- It can contain *only* constants, method signatures, default methods, static methods, and nested types.
- All abstract, default, and static methods in an interface are implicitly public.
- All constant values defined in an interface are implicitly public, static, and final.
- It can contain only interface type variables
- Interface members (fields + methods) are public by default, and are not allowed to be defined as private or protected. Starting from Java 9, methods are allowed to be defined as private, so that some reusable code can be defined without exposing the method.
- The fields of the interface are static and final by default.
- Method bodies exist only for default methods and static methods.
- Interfaces cannot be instantiated—they can only be implemented by classes or extended by other interfaces.
- *You cannot declare an interface inside a block; interfaces are inherently static.*
- Methods in an interface that are not declared as default or static are implicitly abstract.
- When an abstract class implements an interface, it inherits all of its abstract and default methods.

```java
public interface GroupedInterface extends Interface1, Interface2, Interface3 {

    // constant declarations

    // base of natural logarithms
    double E = 2.718282;

    // method signatures
    void doSomething (int i, double x);
    int doSomethingElse(String s);
}
```

- The public access specifier indicates that the interface can be used by any class in any package. If you do not specify that the interface is public, then your interface is accessible only to classes defined in the same package as the interface.
- If we Design an Interface and later modify it the users code may break as they will need to re-code and do new implementations. To Overcame this we will extend the older interface with a new interface as per our need or we can use default methods.

### **Rules for Creating Interfaces**

In an interface, we're allowed to use:

- **[constants variables](https://www.baeldung.com/java-final)**
- **[abstract methods](https://www.baeldung.com/java-abstract-class)**
- **[static methods](https://www.baeldung.com/java-static-default-methods)**
- **[default methods](https://www.baeldung.com/java-static-default-methods)**
- [private variables and private methods (From Java 9)](https://www.geeksforgeeks.org/private-methods-java-9-interfaces/)

We also should remember that:

- we can't instantiate interfaces directly
- an interface can be empty, with no methods or variables in it
- we can't use the *final* word in the interface definition, as it will result in a compiler error.
Making an interface final would contradict this fundamental purpose because it would prevent any class from implementing the interface
- all interface declarations having the *public* or default access modifier; the *abstract* modifier will be added automatically by the compiler
- an interface abstract method can't be *protected* or *final*
- up until Java 9, interface methods could not be *private*; however, Java 9 introduced the possibility to define **[private methods in interfaces](https://www.baeldung.com/java-interface-private-methods)**
- interface variables are *public*, *static*, and *final* by definition; we're not allowed to change their visibility (Java 8)
- private methods are inherently final

### Inner Interface

We can define an interface inside a class. This is known as a nested interface. A nested interface is simply an interface that is declared within the scope of a class or another interface.

Declaration of an inner interface occurs in the body of another interface or class.

They are implicitly public and static as well as their fields when declared in another interface ( similar to field declarations in top-level interfaces)

Inner interfaces declared within another class are also static, but they can have access specifiers which can constrain where they can be implemented

an inner interface can inherit methods and variables from the enclosing interface or class. As with instance methods and variables, an inner class is associated with an instance of its enclosing class and has direct access to that object’s methods and fields

A nested interface can access private members of the enclosing class. This is because nested interfaces, like nested classes, have access to all members (including private members) of their enclosing class.

***Interface Inside Interface***

The accessibility of members in an inner interface depends on their access modifiers and the package structure. Public members are accessible from anywhere, default members are accessible within the same package, and private members are not accessible from inner interfaces.

***Interface Inside class***

Inner interfaces in Java have access to all members of their enclosing class, including fields, methods, and static members, regardless of their access modifiers. This allows inner interfaces to interact with and utilize the enclosing class's functionality.

***Class inside Interface***

A class declared inside an interface in Java can access public, protected, default, and static members of the interface, but it cannot access private members. Additionally, it can access nested interfaces and classes declared within the interface.

<aside>
💡 Can Inner Interface access enclosing class or interface restricted members?

</aside>

<aside>
💡 Can Inner Interface be extended in a class outside package

</aside>

We cannot extend an inner interface (nested interface) outside of its containing class or interface, regardless of whether the inner interface is declared as **`private`**, **`protected`**, or package-private (default access). Inner interfaces are implicitly **`static`** and associated with their containing class or interface, which means they cannot be extended by other classes or interfaces outside of the container.

The access modifiers (**`private`**, **`protected`**, and package-private) determine the visibility of the inner interface within the same package and for subclasses, but they do not change the fundamental rule that inner interfaces are associated with the containing class or interface.

<aside>
💡 Can Inner Interface override and overload enclosing interface or class methods?

</aside>

### Extending a Interface

When an interface extends another interface, it inherits all of that interface's abstract methods.

the accessibility of members of an inner interface when extending it with another interface depends on access modifiers and package boundaries:

Same Package: Public and default members are accessible, protected members are accessible if inherited, and private members are not accessible.

Different Packages: Only public members are accessible, while default, protected, and private members are not accessible.

Here are the rules for extending an inner interface with different access modifiers from outside the package:

1. **Public Inner Interface in a Public Enclosing Class/Interface**: If the inner interface is declared as **`public`** and the enclosing class/interface is also **`public`**, you can extend the inner interface from anywhere, including outside the package.
2. **Public Inner Interface in a Non-Public Enclosing Class/Interface**: If the inner interface is declared as **`public`**, but the enclosing class/interface is not **`public`**, you cannot extend the inner interface from outside the package.
3. **Non-Public Inner Interface**: If the inner interface is not declared as **`public`** (i.e., it has default or package-private access), you cannot extend it from outside the package.

Marker Interface

A marker interface, also known as a tag interface, is an interface in Java that doesn't declare any methods or fields. Its sole purpose is to signal to the compiler or runtime that the classes implementing the interface possess some special behaviour or characteristics associated with the interface.

<aside>
💡 Can we define a class inside the interface?
Yes, if we define a class inside the interface, the Java compiler creates a static nested class

</aside>

<aside>
💡 Difference Between static and default methods in interface?

</aside>

<aside>
💡 Does static and default methods get Inherited?

Default Methods get Inherited but static doesn’t get inherited.

</aside>

<aside>
💡 Access Modifiers used in interface.

public: for the accessibility across all the classes, just like the methods present in the interface

static: as interface cannot have an object, the interfaceName.variableName can be used to reference it or directly the variableName in the class implementing it.

final: to make them constants. If 2 classes implement the same interface and you give both of them the right to change the value, conflict will occur in the current value of the var, which is why only one time initialization is permitted.

Also all these modifiers are implicit for an interface, you don't really need to specify any of them.

Interfaces can declare only constants, not instance variables.

</aside>

<aside>
💡 Can we define variables in interface?

Prior to Java 9, you couldn't define private instance variables in Java interfaces. All variables declared within an interface were implicitly public, static, and final (constants), even if you didn't explicitly declare them as such. This was because interfaces were primarily intended for declaring method signatures and constants.

However, with the introduction of Java 9, private instance variables, as well as private methods, were allowed in interfaces. This was done to support the concept of "private" methods and state within interfaces without exposing them to implementing classes.

Remember that private instance variables in interfaces are not visible to implementing classes and are used primarily for internal implementation within the interface itself, like supporting private methods or encapsulating data.

</aside>

<aside>
💡 Can we Instantiate interface?

No

</aside>

<aside>
💡 Can we define private or protected as method type in Interface?

No we cannot define, all methods are implicitly public in interface  in Java 8

From Java 9 we can define private methods and variables in interface

[https://www.baeldung.com/java-interface-private-methods](https://www.baeldung.com/java-interface-private-methods)

[Protected in Interfaces](https://stackoverflow.com/questions/5376970/protected-in-interfaces)

</aside>

<aside>
💡 What happens when a class implements several interfaces that define the same default methods.

The code simply won't compile, as there's a conflict caused by multiple interface inheritance (Diamond Problem)

To solve this ambiguity, we must explicitly provide an implementation for the methods

</aside>

<aside>
💡 Why are class static methods inherited but not interface static methods?

</aside>

### **Abstract Methods and Classes**

- Abstract methods are those which have only declaration

```java
abstract void methodname(int param1,String param2);
```

- Abstract classes are declared with abstract keyword
- It may or may not include abstract methods.
- It can be sub classed. subclass should implement abstract methods or should be abstract itself
- Abstract Class can have both constructor and main methods.
- The abstract keyword cannot be combined with static, private, or final keyword.
- Any class that contains one or more abstract methods must also be declared abstract.
- Abstract classes can have both abstract and concrete methods.

<aside>
💡 Can we define constructor in Abstract Class ?

Like any other classes in Java, abstract classes can have constructors even when they are only called from their concrete subclasses.

</aside>

<aside>
💡 Can we define variables in Abstract Class?

We can declare fields that are not static and final.

Abstract classes can contain instance variables, which can be used by both the abstract class and its subclasses. 

Subclasses can access these variables directly, just like any other instance variables.

</aside>

<aside>
💡 Can we Instantiate Abstract Class?

An abstract class is a class that cannot be instantiated.

We have to extend and implement abstract method in concrete class, and we can create objects of concrete class.

</aside>

<aside>
💡 Can we define private or protected as abstract method type?

We can define public, protected, and private concrete methods.

abstract method cannot be private.

we can declare an abstract method protected.

</aside>

<aside>
💡 Can we add static methods in Abstract class?

Yes We can.

</aside>

<aside>
💡 Can we add default keyword on methods in Abstract class?

The default keyword only applies to interfaces default methods

</aside>

<aside>
💡 Can abstract class extend a concrete class?

An abstract class always extends a concrete class (java.lang.Object at the very least). So it works the same as it always does

</aside>

<aside>
💡 Can we have final concrete methods in abstract class?

Yes, there may be "final" methods in "abstract" class. But, any "abstract" method in the class can't be declared final

</aside>

<aside>
💡 Can we define abstract class as final?

The class can be either abstract or final, not both

</aside>

***Difference between Abstract class and interfaces***

- Abstract classes are similar to interfaces. You cannot instantiate them, and they may contain a mix of methods declared with or without an implementation. However, with abstract classes, you can declare fields that are not static and final, and define public, protected, and private concrete methods. With interfaces, all fields are automatically public, static, and final, and all methods that you declare or define (as default methods) are public.
- From a design point of view, an abstract class provides an IS-A relationship, which needs to meet the Li-type replacement principle, that is, subclass objects must be able to replace all parent class objects. The interface is more like a LIKE-A relationship. It just provides a method to realize the contract, and does not require the interface and the class implementing the interface to have an IS-A relationship.
- From the point of view of use, a class can implement multiple interfaces, but cannot inherit multiple abstract classes.
- Fields of interfaces can only be of static and final types, while fields of abstract classes have no such restrictions.
- Members of an interface can only be public, while members of an abstract class can have multiple access rights.

***Where to use which one?***

Use the interface:

- All unrelated classes need to implement a method, for example, all unrelated classes can implement the compareTo() method in the Comparable interface;
- Need to use multiple inheritance.

Use an abstract class:

- Code needs to be shared among several related classes.
- Need to be able to control the access permissions of inherited members, not all public.
- Non-static and non-const fields need to be inherited.

In many cases, interfaces are preferred over abstract classes. Because interfaces do not have the strict class hierarchy requirements of abstract classes, you can flexibly add behavior to a class. And starting from Java 8, interfaces can also have default method implementations, making the cost of modifying interfaces very low.

Example of Abstract class use case is AbstractMap which is parent to HashMap,TreeMap.

### ***Keywords***

**final**

1. **Data**
    
    Declare data as constants, which can be compile-time constants or constants that cannot be changed after being initialized at runtime.
    
    For primitive types, final makes the value unchanged;
    
    For reference types, final makes the reference unchanged, so other objects cannot be referenced, but the referenced object itself can be modified.
    
    ```java
    final int x = 1;
    // x = 2;  // cannot assign value to final variable 'x'
    final A y = new A();
    y.a = 1;
    ```
    
2. **Method**
    
    The declared method cannot be overridden by subclasses.
    
    The private method is implicitly designated as final. If the method defined in the subclass has the same signature as a private method in the base class, the subclass method does not override the base class method, but defines it in the subclass. a new approach.
    

1. C**lass**
    
    Declaring classes are not allowed to be inherited.
    
    Extending a final Class?
    
    a final class cannot be extended.
    
    Overriding a final method?
    
    a final method cannot be overridden.
    
    Overloading a final method?
    
    we can overload a final method.
    

### **static**

1. **Static variables**
    - Static variable: Also known as class variable, that is to say, this variable belongs to the class, and all instances of the class share the static variable, which can be accessed directly through the class name. There is only one copy of static variables in memory.
    - Instance variable: Every time an instance is created, an instance variable is generated, which lives and dies with the instance.
2. **Static methods**
    
    A static method exists when the class is loaded, and it does not depend on any instance. So a static method must have an implementation, that is to say it cannot be an abstract method.
    
    It can only access the static fields and static methods of the class to which it belongs, and the methods cannot have this and super keywords, because these two keywords are associated with specific objects.
    
3. **Static block**
    
    Static statement blocks are run once when the class is initialized.
    
4. **Static inner class**
    
    The non-static inner class depends on the instance of the outer class, that is to say, you need to create an instance of the outer class before you can use this instance to create the non-static inner class. Static inner classes do not.
    
    Static inner classes cannot access non-static variables and methods of outer classes.
    
5. **Static package import**
    
    When using static variables and methods, there is no need to specify the ClassName, which simplifies the code, but the readability is greatly reduced.
    
6. **Initialization sequence**
    
    Static variables and static statement blocks take precedence over instance variables and ordinary statement blocks, and the initialization order of static variables and static statement blocks depends on their order in the code.
    
    The last is the initialization of the constructor.
    

In the case of inheritance, the initialization order is:

- Parent class (static variable, static statement block)
- Subclasses (static variables, static statement blocks)
- Parent class (instance variables, normal statement blocks)
- parent class (constructor)
- Subclasses (instance variables, ordinary statement blocks)
- subclass (constructor)

**[Message Passing](https://www.geeksforgeeks.org/message-passing-in-java/):** Objects communicate with one another by sending and receiving information to each other. A message for an object is a request for execution of a procedure and therefore will invoke a function in the receiving object that generates the desired results. Message passing involves specifying the name of the object, the name of the function and the information to be sent.

**Dynamic and Static Binding**

### Reflection API

Reference

- **[Trail: The Reflection API(opens new window)](https://docs.oracle.com/javase/tutorial/reflect/index.html)**
- **[In-depth analysis of Java reflection (1) - basics](http://www.sczyh30.com/posts/Java/java-reflection-1/)**
- References
    - [https://docs.oracle.com/javase/tutorial/reallybigindex.html](https://docs.oracle.com/javase/tutorial/reallybigindex.html)
    - [https://www.baeldung.com/java-tutorial](https://www.baeldung.com/java-tutorial)
    - [https://www.baeldung.com/java-classes-initialization-questions](https://www.baeldung.com/java-classes-initialization-questions)
    - [https://www.baeldung.com/category/java](https://www.baeldung.com/category/java)
    
- Topics
    
    Abstract
    
    Interface
    
    Inheritance 
    
    Association 
    
    Assertation
    
    Composition
    
    Access Modifier
    
    Instantiation
    
    Parent class
    
    Child class
    
    default class
    
    Compile time and runtime polymorphism
    
    final