### Some facts about Scala
  * Classes cannot have static members.
  * A synthetic class is generated automtically by the compiler rather
  than written by hand by the programmer.
  * `require` method is used to implement contraints on values passed
  into a method or constructor. It is defined in standalone object
  `Predef`.
  * The keyword `this` refers to the object instace on which the currently
  executing method was invoked, or if used in a constructor, the object
  instance being constructed.
  * Constructors other than the primary constructor are called
  _auxiliary constructors_. Defined as follows;
  ```scala
  class Something( a: T1, b: T2 ){
    //....
    def this( c: T3 ) { /* ... */ } // auxiliary constructor

    //....
  }
  ```
  * In Scala, every auxiliary constructor must invoke another constructor
  of the same class as its first action. In other words, the first
  statement in every auxiliary constructor in every Scala class will
  have the form "this(...)".
  * In a Scala class, only the primary constructor can invoke a
  superclass constructor.
  * _implicit conversions_ automatically converts one type to another when
  needed. This requirement can be specified for a type as follows;
  ```scala
  implicit def intToRational( x: Int ) = new Rational( x )
  ```
  This defined a conversion method from `Int` to `Rational`. The implicit
  modifier in front of the method tells the compiler to apply it automatically
  in a number of situations.
### Basic types
  * _Integral types_ : Byte, Short, Int, Long and Char are collectively 
  called integral types.
  * _Numeric types_ : integral types alongwith Float and Double are called
  numeric types.
  * _Byte_ : 8-bit signed two's complement integer.
  * _Short_ : 16-bit signed two's complement integer.
  * _Int_ : 32-bit signed two's complement integer.
  * _Long_ : 64-bit signed two's complement integer.
  * _Char_ : 16-bit unsigned Unicode character.
  * _String_ : a sequence of Chars. Resides in package `java.lang`.
  * _Double_ : 64-bit IEEE 754-single-precision float.
  * _Boolean_ : true or false.
  * Apart from String, all other types reside in package `scala`.
  * In addition to providing an explicit character between the single 
  quotes, you can provide an octal or hex number for the character code 
  point preceded by a backslash.
  ```scala
  scala> val c = '\101' // Unicode character code for A is 101 octal.
  c: Char = A 
  ```
  *  Scala includes a special syntax for raw strings. You start and end 
  a raw string with three double quotation marks in a row ("""). The 
  interior of a raw string may contain any characters whatsoever, 
  including newlines, quotation marks, and special characters, except 
  of course three quotes in a row
  ```scala
  println("""Welcome to Ultamix 3000.
             Type "HELP" for help.""")
  ```
  * The issue is that the leading spaces before the second line are 
  included in the string! To help with this common situation, you can 
  call stripMargin on strings. To use this method, put a pipe 
  character (|) at the front of each line, and then call stripMargin 
  on the whole string.
  ```scala
  println("""|Welcome to Ultamix 3000.
             |Type "HELP" for help.""".stripMargin)
  ```
  * A symbol literal is written 'ident, where ident can be any 
  alphanumeric identifier. Such literals are mapped to instances of 
  the predefined class scala.Symbol. Specifically, the literal 'cymbal 
  will be expanded by the compiler to a factory method invocation: 
  Symbol("cymbal"). Symbol literals are typically used in situations 
  where you would use just an identifier in a dynamically typed language
### Operators
  * Operators are just a nice syntax for ordinary methods calls.
  * In Scala operators are not special language syntax: any method 
  can be an operator.
  * As with the infix operators, these prefix operators are a shorthand 
  way of invoking methods. In this case, however, the name of the 
  method has "unary\_" prepended to the operator character.  
  Example:
  ```scala
    scala> -2.0                  // Scala invokes (2.0).unary_-
    res2: Double = -2.0
    
    scala> (2.0).unary_-
    res3: Double = -2.0
  ```
  * The only identifiers that can be used as prefix operators are +, -, !, 
  and ~. Thus, if you define a method named unary\_!, you could invoke 
  that method on a value or variable of the appropriate type using prefix 
  operator notation, such as !p. But if you define a method named unary\_\*, 
  you wouldn't be able to use prefix operator notation, because \* isn't 
  one of the four identifiers that can be used as prefix operators. You 
  could invoke the method normally, as in p.unary\_\*, but if you 
  attempted to invoke it via \*p, Scala will parse it as if you'd written 
  \*.p, which is probably not what you had in mind
  * The logical-and and logical-or operations are short-circuited as 
  in Java: expressions built from these operators are only evaluated 
  as far as needed to determine the result.
  * The bitwise methods are: bitwise-and (&), bitwise-or (|), and 
  bitwise-xor (^). The unary bitwise complement operator (~, the method 
  unary\_~), inverts each bit in its operand.
### Operator precedence
  * Scala decides precedence based on the first character of the methods 
  used in operator notation (there's one exception to this rule, which 
  will be discussed below). If the method name starts with a \*, for example, 
  it will have a higher precedence than a method that starts with a +. 
  Thus 2 + 2 \* 7 will be evaluated as 2 + (2 \* 7), and a +++ b \*\*\* c 
  (in which a, b, and c are variables, and +++ and \*\*\* are methods) 
  will be evaluated a +++ (b \*\*\* c), because the \*\*\* method has a 
  higher precedence than the +++ method.
  * precedence order:  
        (all other special characters)  
        \* / %  
        \+ -  
        :  
        = !  
        < >  
        &  
        ^  
        |  
        (all letters)  
        (all assignment operators)
  * The associativity of an operator in Scala is determined by its last 
  character.
  * any method that ends in a `:` character is invoked on its right 
  operand, passing in the left operand. Methods that end in any other 
  character are the other way around. They are invoked on their left 
  operand, passing in the right operand. So `a \* b` yields `a.\*(b)`, 
  but `a ::: b` yields `b.:::(a)`.
### Singleton Objects
  * Scala has _singleton objects_, definition for which looks like a class
  definition, except instead of the keyword `class`{.scala} `object`{.scala}
  is used.
  * When as singleton object shares the same name with a class, it is called
  the class's _companion object_. Both the class and the companion object
  must be defined in the same source file.
  * A class and it's companion object can access each other's private members.
  * We can invoke methods on singleton objects same as we invoke static 
  methods in java.
  * Singleton objects cannot take parameters whereas classes can.
  * Cannot instantiate singleton object.
  * Implemented as an instance of a synthetic class referenced from a static
  variable and hence have the same initialisation sematics as java statics.
  * A singleton object is initialized the first time some code accesses it.
### Standalone Objects
  * A singleton object that does not share the same name with a companion
  class is called a _standalone object_.
  * Standalone objects can be used for collecting related utility methods
  together, or defining an entry point in a scala application.  
  Example:
    ```scala
    // In file Summer.scala
    import ChecksumAccumulator.calculate

    // Entry point using standalone object
    object Summer {
      def main( args: Array[String] ){
        for( args<-args ) println(arg + ": " + calculate(arg))
      }
    }
    ```
### Scala application
  * To run a scala program, you must supply the name of a standalone singleton
  object with a main method that takes one parameter, an `Array[String]`{.scala}
  and has a result type of `Unit`{.scala}.
  * Any standalone object with a main method of the proper signature can be
  used as the entry point into an application
  * A script in scala must end in a result expression.
  * To run non-script scala files, it has to be compiled with the scala
  compiler _scalac_.
  * For fast compilation used _fsc_, which keeps a daemon running with various
  jars filed already loaded.
  * After compilation, the program can be run with _scala_ using the name
  of the standalone object containing the main method.
### The Application trait
  * The trait `Application`{.scala} declares a main method of the appropriate
  signature. So any singleton object inheriting the trait will be able to
  use the method.
  * When a singleton object inherits this trait, the code between the curly
  braces is collected into a _primary constructor_ of the singleton object,
  and is executed when the class is initialized.
  * Cannot use this trait if accessing command-line arguments. Also due to
  JVM threading model, we need and explicit main method if our program is
  multithreaded.  
  Example:
    ```scala
    import ChecksumAccumulator.calculate

    object FallWinterSpringSummer extends Application {
      
      for( season <- List("fall", "winter", "spring") )
        println( season +": "+ calculate(season) )
    }
    ```
### Functions
  - Method parameters are vals not vars.  
  Example: the following won't compile.
    ```scala
    def add(b: Byte): Unit = {
      b = 1   // This won't compile, because b is a val.
      sum += b
    }
    ```
  - Methods with a result type of `Unit`{.scala} can be expressed by leaving
  off the the result type and the equals sign, and enclose the body
  of the method in curly braces.  
  Example:
    ```scala
    def add( b: Byte ) { sum += b }
    ```
