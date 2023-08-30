# Java Revision Notes

---

Java does not provide low-level programming functionalities like pointers. 

Also, Java codes are always written in the form of classes and objects.

[https://docs.oracle.com/javase/tutorial/reallybigindex.html](https://docs.oracle.com/javase/tutorial/reallybigindex.html)

[https://www.baeldung.com/java-tutorial](https://www.baeldung.com/java-tutorial)

- To-Add
    
    Abstract
    
        Can we define constructor in Abstract Class ?
        
        Can we define variables in Abstract Class?
        
        Can we Instantiate Abstract Class?
        
        Can we define private or protected as abstract method type?
        
        Can we add static methods in Abstract class?
        
        Can we add default methods in Abstract class?
        
        Can abstract class extend a concrete class?
    
    Interface
    
        Can we define static and default methods in interface?
        
        Can we define variables in Abstract Class?
        
        Can we Instantiate Abstract Class?
        
        Can we define private or protected as method type in Interface?
    
    Inheritance 
    
        Does Private member of parent class get inherited?
        
        Can we assign a child object to parent variable and vice versa?
    
    Is-a, Has-a, Part-of
    
    Association 
    
    Assertation
    
    Composition
    
    Access Modifier
    
    Static Method
    
        Is Static Method Inherited?
        
        Hiding parent Static Method?
        
        Can we make a class static?
    
    Constructor
    
        Overloading a Constructor
        
        Overriding a Constructor
        
        Is Constructor Inherited?
        
        Private, Protected , Public and Default Constructors.
    
    static constructor
    
    final constructor
    
    Instantiation
    
    Parent class
    
    Child class
    
    default class
    
    Overload
    
        How methods differentiate on Overloading?
        
        What is Method Signature and how it differentiate ?
        
        Can we Overload  Constructor?
        
        Can we overload static method?
        
        Can we overload default and static method in interface?
    
    Override
    
        Calling a Overridden Method from parent and child type variables.
        
        Compile time and runtime polymorphism
        
        final
        
        Extending a final Class?
        
        Overriding a final method?
        
        Overloading a final method?

    - Nested Classes.
        How static and Non-static classes differ?
        Working of Access Modifier in Nested classes.
        Extending of Nested classes.
        How private and protected members of nested classes inherit.
        Making a nested class final
        can it exist without the object of enclosing class
        can we create only nested class object

    - Package
        Importing package will import all subpackage as well?
        accessing classes and methods defined in subpackage from top level package and vice versa.
        Access Modifer effects on subpackage and top level package
        moving things from a package using cli
        compiling a package
        exporting a package

    - Inheritance
        Does Private members get inherited?
        Does Default and Protected members get inherited if we extend a class outside a package?
        Can we assing a child object to parent variable and vice versa?
        Does Static Methods get Inherited?
        Does Constructor get Inherited?
        Does the child class make calls to parent class constructor Implicitly?
        How will the child class call super class constructor before or after it's constructor instructions?
        Can Constructor be Overloaded or Overridding?
        How static methods get Overloaded and overridden in child class?
        Does initalizer blocks get inherited?
        Does static variable / members gets inherited?
        Making calls to instance method and static method of child class using parent type variable vice versa?

    - Interface
        Can we define variables, constants, static and non-static methods in Interface?
        what are default methods in interface and how it get inherited to classes implementing it.
        what if two interface have same methods and constants and a class implementing both?
        What will happen if we extend a interface, what will get inherited?
        Defining private or protected members in interface.
        assing a class with child interface implementation to parent interface.


    - Dynamic and Static Binding.
    - Message Passing in java methods.
    

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

Everything in Java should be in class and every class should be in independent file unless it’s inner class

Todo: [https://docs.oracle.com/javase/tutorial/java/data/index.html](https://docs.oracle.com/javase/tutorial/java/data/index.html) 

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

The name of class file should be exactly same as public class, however The name of the file can be a different name if it does not have any public class.

Java is Case sensitive

**Naming Convention in Java**

To do
Class Name is advice to be like : MyClass, Student, MyAnotherClass

*Execution point of each java program is main method*

Todo Tricks and Tips for Java Main Method

**Access Modifiers**

| Access Modifier | Within Class | Within Package | Outside Package by subclass only | Outside Package |
| --- | --- | --- | --- | --- |
| Private | Y | N | N | N |
| Default | Y | Y | N | N |
| Protected | Y | Y | Y | N |
| Public | Y | Y | Y | Y |

the default, also known as *package-private*

Identifiers used to identify data/instructions points.
Keywords define functionalities and literals define a value.

**Wrapper Classes** are those which can wrap or contain a primitive data type.
Autoboxing is conversion of a primitive datatype to wrapper class of it
Unboxing is reverse of it

The Java platform stores **character values using Unicode conventions.**

### **Strings**

String are immutable in Java.

*Why String is Immutable in Java*

It is made immutable for security purpose and memory usage enhancements.

Since strings are immutable whenever we create a new same string, the JVM will first look into string constant pool a memory are that stores string literals. if any string literal matches it will create a new reference to same object thus saving heap memory.

Strings are consider thread-safe implicitly. and can be used in multiple threads without synchronization.

If we don’t make the String immutable, it will pose a serious security threat to the application. For example, database usernames, passwords are passed as strings to receive database connections. The socket programming host and port descriptions are also passed as strings. The String is immutable, so its value cannot be changed. If the String doesn’t remain immutable, any hacker can cause a security issue in the application by changing the reference value. 

*String Buffer and String Builder*

String Builder and String Buffer both provides alternative for String Class and provides a mutable sequence of characters.
String Builder is preferred where performance is required, but it is not considered thread safe.
String Buffer is considered thread safe.

***String.intern [more here….](https://www.baeldung.com/string/intern)***

*String joiner and String tokenizer*

A **Jagged Array** is an array of arrays such that member arrays can be of different sizes, i.e., we can create a 2-D array but with a variable number of columns in each row. These types of arrays are also known as Jagged arrays.

**Final arrays ,** we can not make the final array refer to some other array but the data within an array that is made final can be changed/manipulated.

[util.Arrays vs reflect.Array](https://www.geeksforgeeks.org/util-arrays-vs-reflect-array-in-java-with-examples/)

reflect.array class cannot be is immutable and provides method to work with arrays and is considered thread safe.

util array can be extended and are not thread safe

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

*Volatile Variables*

[A Strategy for Defining Immutable Objects](https://docs.oracle.com/javase/tutorial/essential/concurrency/imstrat.html)

### **Is It Possible?**

***Can we Overload Static Methods?***

Yes we can have more than one definition of static methods with different signature in a class.

***Can we have a static method and a non static method with same name and same signature?***

No we cannot it will throw already defined error

We can have with different signature, with different parameters

**Private Constructor**

If we declare a class constructor private, we cannot subclass it also cannot create it’s object outside the class. it follows singleton design pattern.

Yes. Constructors in Java can be private. All classes including abstract classes can have private constructors. Using private constructors we can prevent the class from being instantiated or we can limit the number of objects of that class.

**Static Constructor**

We cannot have static constructor

We cannot use `this` , `super`on static context

We cannot extend a class having no default constructor, to extend such class we need to call the base class parametrized constructor in base class constructor.

private static fields can be accessed through private static methods of the class.

### **Constructors in Java**

Constructor cannot be final, static or abstract. it will throw modifier not allowed here error.

A constructor is not inherited by child class, and cannot be overridden.

We can overload constructor but we need to define default constructor also, Java only define constructor when we don’t define any by our self.

**Final Constructors**

When there is no chance of constructor overriding, there is no chance of modification also. When there is no chance of modification, then no sense of restricting modification there. We know that the final keyword restricts further modification.

**Final Methods**

# OOP Concepts

## **Encapsulation**

**Todo : Defination**

We can create a fully encapsulated class in Java by making all the data members of the class private

Read-Only Class : Private members with getter methods only

Write-Only Class : Private members with setter methods only

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

Variable Arguments in Java

```java
public class methodname(dataype... parametername){
    // parametername will be an array of datatype
}
```

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

*A class that is declared final cannot be subclassed. This is particularly useful, for example, when creating an immutable class like the String class.*

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

### Package

**Todo: Defination**

Advantage of Java Package

1. Java package is used to categorize the classes and interfaces so that they can be easily maintained.
2. Java package provides access protection.
3. Java package removes naming collision.

If you import a package, all the classes and interface of that package will be imported excluding the classes and interfaces of the subpackages. Hence, you need to import the subpackage as well.

## **Inheritance**

- A subclass inherits all of the public and protected members of its parent, no matter what package the subclass is in. If the subclass is in the same package as its parent, it also inherits the package-private members of the parent.
- A subclass does not inherit the private members of its parent class.
- A nested class has access to all the private members of its enclosing class—both fields and methods. Therefore, a public or protected nested class inherited by a subclass has indirect access to all of the private members of the superclass.

*5 Types of Inheritance*

- Single Inheritance
- Multi-Level Inheritance
- Multiple Inheritance ( Through Interfaces)
- Hybrid Inheritance (many to one)
- Hierarchical Inheritance ( one to many )

**Instance Methods in Subclass**

- Instance methods can be override with same name, same method signature and same return type.
- Instance methods in subclass can return subtype of parent method return type this is called *covariant return type*
- when overriding a class we use @override annotation, if superclass doesn’t have it it will raise compile time error

**Static Methods in Subclass**

If a subclass defines a static method with the same signature as a static method in the superclass, then the method in the subclass hides the one in the superclass.

The distinction between hiding a static method and overriding an instance method has important implications:

- The version of the overridden instance method that gets invoked is the one in the subclass.
- The version of the hidden static method that gets invoked depends on whether it is invoked from the superclass or the subclass.

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

### ***Association***

Association is relation of a class with another which establishes through their Objects.

Association can be one-to-one, one-to-many, many-to-one, many-to-many.

Two types of Association

Aggregation (Has-A): It’s Unidirectional, one class can have object of other class.

Composition (Is-A): one class is a type of another class or part of another class

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

A class can have multiple methods of the same name, and each method can be differentiated either by bypassing different types of parameters or bypassing a different number of parameters.

## Abstraction

## **Interface**

- An Interface in Java programming language is defined as an abstract type used to specify the behaviour of a class.
- It is used to achieve abstraction and multiple inheritance in Java.
- It can contain *only* constants, method signatures, default methods, static methods, and nested types.
- It can contain only interface type variables

Method bodies exist only for default methods and static methods. Interfaces cannot be instantiated—they can only be implemented by classes or extended by other interfaces.

*You cannot declare an interface inside a block; interfaces are inherently static.*

Methods in an interface that are not declared as default or static are implicitly abstract.

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

- All abstract, default, and static methods in an interface are implicitly public.

- All constant values defined in an interface are implicitly public, static, and final.

- If we Design an Interface and later modify it the users code may break as they will need to re-code and do new implementations. To Overcame this we will extend the older interface with a new interface as per our need or we can use default methods.

- Default methods and abstract methods in interfaces are inherited like instance methods.

### **Abstract Methods and Classes**

- Abstract methods are those which have only declaration

```java
abstract void methodname(int param1,String param2);
```

- Abstract classes are declared with abstract keyword
- It may or may not include abstract methods.
- It can be sub classed. subclass should implement abstract methods or should be abstract itself
- Abstract Class can have both constructor and main methods.

**Difference between Abstract class and interfaces**

Abstract classes are similar to interfaces. You cannot instantiate them, and they may contain a mix of methods declared with or without an implementation. However, with abstract classes, you can declare fields that are not static and final, and define public, protected, and private concrete methods. With interfaces, all fields are automatically public, static, and final, and all methods that you declare or define (as default methods) are public.

Example of Abstract class use case is AbstractMap which is parent to HashMap,TreeMap.

**[Message Passing](https://www.geeksforgeeks.org/message-passing-in-java/):** Objects communicate with one another by sending and receiving information to each other. A message for an object is a request for execution of a procedure and therefore will invoke a function in the receiving object that generates the desired results. Message passing involves specifying the name of the object, the name of the function and the information to be sent.

**Dynamic and Static Binding**