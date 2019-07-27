# Hello Kt

## Basics

* Use `fun` to define a function.
* Every application needs a function named `main`.
* Use `//` to denote a single-line comment.
* A `String` is a string of characters. You denote a `String` value by enclosing its characters in double quotes.
* Code blocks are defined by a pair of curly braces `{}`.
* The assignment operator is *one* equals sign `=`.
* The equals operator uses *two* equals signs `==`.
* Use `var` to define a variable whose value may change.
* Use `val` to define a variable whose value stay the same.
* A `while` loop runs everything within its block so long as the conditional test is *`true`*.
* If the conditional test is *`false`*, the while loop code block won't run, and execution will move down to code immediately after the loop block.
* Put a conditional test inside parentheses `()`.
* Add conditional branches to your code using `if` and `else`. The `else` clause is optional.
* You can use `if` as an expression so that it returns a value. In this case, the `else` clause is mandatory.

## Types and variables

* In order to create a variable, the compiler needs to know its name, its type, and whether it can be reused.
* If the variable's type isn't explicitly defined, the compiler infers it from its value.
* A variable holds a reference to an object.
* An object has state and behavior. Its behavior is exposed through its functions.
* Defining the variable with `var` means the variable's object reference can be replaced. Defining the variable with `val` means the variable holds a reference to the same object forever.
* Kotlin has a number of basic types: `Byte`, `Short`, `Int`, `Long`, `Float`, `Double`, `Boolean`, `Char` and `String`.
* Explicitly define a variable's type by putting a colon after the variable's name, followed by the type: `var tinyNum: Byte`.
* You can only assign a value to a variable that has a compatible type.
* You can convert one numeric type to another. If the value won't fit into the new type, some precision is lost.
* Create an array using the `arrayOf` function: `var myArray = arrayOf(1, 2, 3)`.
* Access an array's items using, for example, `myArray[0]`. The first item in an array has an index of *`0`*.
* Getting an array's size using `myArray.size`.
* The compiler infers the array's type from its items. You can explicitly define an array's type like this: `var myArray = Array<Byte>`.
* If you define an array using `val`, you can still update the items in the array.
* `String` templates provide a quick and easy way of referring to variable or evaluating an expression from inside a `String`.

## Functions

* Use functions to organize your code and make it more reusable.
* A function can have parameters, so you can pass more than one value to it.
* The number and type of values you pass to the function must match the order and type of the parameters declared by the function.
* A function can return a value. You must define the type of value (if any) it returns.
* A `Unit` return type means that the function doesn't return anything.
* Choose `for` loops over `while` loops when you know how many times you want to repeat your loop code.
* The `readLine()` function reads a line of input from the standard input stream. It returns a `String` value, the text entered by the user.
* If the input stream has been redirected to a file and the end of the file has been reached, the `readLine()` function returns `null`. `null` means it has no value, or it's missing.
* `&&` means "and". `||` means "or". `!` means "not".

## Classes and objects

* Classes let you define your own types.
* A class is a template for an object. One class can create many objects.
* The things an object knows about itself are its properties. The things an object can do are its functions.
* A property is a variable that's local to the class.
* The `class` keyword define a class.
* Use dot operator `.` to access an object's properties and functions.
* A constructor runs when you initialize an object.
* You can define a property in the primary constructor by prefixing a parameter with `val` or `var`. You can define a property outside the constructor by adding it to the class body.
* Initializer blocks run when an object is initialized.
* You must initialize each property before you use its value.
* Getters and setters let you get and set property values.
* Behind the scenes, the compiler adds a default getter and setter to every property.

## Subclasses and superclasses

* A superclass contains common properties and functions that are inherited by one or more subclasses.
* A subclass can include extra properties and functions that aren't in the superclass, and can override the things it inherits.
* Use the IS-A test to verify that your inheritance is valid. If `X` is a *subclass* of `Y`, then `X` IS-A `Y` must make sense.
* The IS-A relationship works in only one direction. A `Hippo` is an `Animal`, but not all animals are Hippos.
* If class `B` is a subclass of class `A`, and class `C` is a subclass of class `B`, class `C` passes the IS-A test for both `B` and `A`.
* Before you can use a class as a superclass, you must declare it `open`. You must also declare any properties and functions you want to override as `open`.
* Use `:` to specify a subclass's superclass.
* If the superclass has a primary constructor, then you must call it in the subclass header.
* Override properties and functions in the subclass by prefixing them with `override`. When you override a property, its type must be compatible with that of the superclass property. When you override a function, its parameter list must stay the same, and its return type must be compatible with that of the superclass.
* Overridden functions and properties stay open until they are declared `final`.
* When a function is overridden in a subclass, and that function is invoked on an instance of the subclass, the overridden version of the function is called.
* Inheritance guarantees that all subclasses have the functions and properties defined in the superclass.
* You can use a subclass in any place where the superclass type is expected.
* Polymorphism means "many forms". It allows different subclasses to have different implementations of the same function.

## Abstract classes and interfaces

* An abstract class can't be instantiated. It can contain both abstract and non-abstract properties and functions.
* Any class that contains an abstract property or function must be declared abstract.
* A class that's not abstract is called concrete.
* You implement abstract properties and functions by overriding them.
* All abstract properties and functions must be overridden in any concrete subclasses.
* An interface lets you define common behavior outside a superclass hierarchy, so that independent classes can still benefit from polymorphism.
* Interface can have abstract or non-abstract functions.
* Interfaces properties can be abstract, or they can have getters and setters. They can't be initialized, and they don't have access to backing field.
* A class can implement multiple interfaces.
* If a subclass inherits from a superclass (or implements an interface) named `A`, you can use the code: `super<A>.myFunction` to call the implementation of `myFunction` that's defined in `A`.
* If a variable holds a reference to an object, you can use the `is` operator to check the type of the underlying object.
* The `is` operator performs a smart cast when the complier can guarantee that the underlying object can't have changed between the type check and its usage.
* The `as` operator lets you perform an explicit cast.
* A `when` expression lets you compare a variable against an exhaustive set of different options.

## Data class

* The behavior of the `==` operator is determined by the implementation of the `equals` function.
* Every class inherits an `equals`, `hashCode` and `toString` function from the `Any` class because every class is a subclass of `Any`. These functions can be overridden.
* The `equals` function tells you if two objects are considered "equal". By default, it returns `true` if it's used to test the same underlying object, and `false` if it's used to test separate objects.
* The `===` operator lets you check whether two variables refer to the same underlying object irrespective of the object's type.
* A data class lets you create objects whose main purpose is to store data. It automatically overrides the `equals`, `hashCode` and `toString` functions, and includes `copy` and `componentN` functions.
* The data class `equals` function checks for equality by looking at each object's property values. If two data objects hold the same data, the `equals` function returns `true`.
* The `copy` function lets you create a new copy of a data object, altering some of its properties. The original object remains intact.
* `componentN` functions let you destructure data objects into their component property values.
* A data class generates its functions by considering the properties defined in its primary constructor.
* Constructors and functions can have default parameter values. You can call a constructor or function by passing parameter values in order of declaration or by using named arguments.
* Classes can have secondary constructors.
* An overloaded function is a different function that happens to have the same function name. An overloaded function must have different arguments, but may have a different return type.
* **RULES FOR DATA CLASSES**
  * There must be primary constructor.
  * The primary constructor must define one or more parameters.
  * Each parameter must be marked as `val` or `var`.
  * Data classes must not be open or abstract.

## Nulls and exceptions

* `null` is a value that means a variable doesn't hold a reference to an object. The variable exists, but it doesn't refer to anything.
* A nullable type can hold null values in addition to its base type. You define a type as nullable by adding a `?` to the end of it.
* To access a nullable variable's properties and functions, you must first check that it's not `null`.
* If the complier can't guarantee that a variable is not `null` in between a null-check and its usage, you must access properties and functions using safe call operator (`?.`).
* You can chain safe call together.
* To execute code if (and only if) a value is not `null`, use `?.let`.
* The Elvis operator (`?:`) is a safe alternative to an if expression.
* The non-null assertion operator (`!!`) throws a `NullPointerException` if the subject of your assertion is `null`.
* An exception is a warning that occurs in exceptional situations. It's an object of type `Exception`.
* Use `throw` to throw an exception.
* Catch an exception using `try/catch/finally`.
* `try` and `throw` are expressions.
* Use a safe cast (`as?`) to avoid getting a `ClassCastException`.

## Collections

* Create an array initialized with `null` values using the `arrayOfNulls` function.
* Useful array functions includes: `sort`, `reverse`, `contains`, `min`, `max`, `sum`, `average`.
* The Kotlin Standard Library contains pre-built classes and functions grouped into packages.
* A `List` is a collection that knows and cares about index position. It can contain duplicate values.
* A `Set` is an unordered collection that doesn't allow duplicate values.
* A `Map` is a collection that uses key/value pairs. It can contain duplicate values, but not duplicate keys.
* `List`, `Set` and `Map` are immutable. `MutableList`, `MutableSet` and `MutableMap` are mutable subtypes of these collections.
* Create a `List` using the `listOf` function.
* Create a `MutableList` using `mutableListOf`.
* Create a `Set` using the `setOf` function.
* Create a `MutableSet` using `mutableSetOf`.
* A `Set` checks for duplicates by first looking for matching hash code values, It then uses the `===` and `==` operators to check for referential or object equality.
* Create a `Map` using the `mapOf` function, passing in key/value pairs.
* Create a `MutableMap` using `mutableMapOf`.

## Generics

* Generics let you write consistent code that's type-safe. Collections such as `MutableList` use generics.
* The generic type is defined inside angle brackets `<>`, for example:

```kotlin
    class Contest<T>.
```

* You can restrict the generic type to a specific super-type, for example:

```kotlin
    class Contest<T: Pet>.
```

* You create an instance of a class with a generic type by specifying the "real" type in angle brackets, for example:

```kotlin
    Contest<Cat>.
```

* Where possible, the complier will infer the generic type.
* You can define a function that uses a generic type outside a class declaration, or one that uses a different generic type, for example:

```kotlin
    fun <T> listPet(): List<T> {
        ...
    }
```

* A generic type is invariant if it can only accept references of that specific type. Generic types are invariant by default.
* A generic type is covariant if you can use a subtype in place of super-type. You specify that a type is covariant by prefixing it with `out`.
* A generic type is contra variant if you can use a super-type in place of a subtype. You specify that a type is contra variant by prefixing it with `in`.

## Lambdas and higher-order functions

* A lambda expression, or lambda, takes the form: `{ x: Int -> x + 5 }`. The lambda is defined within curly braces, and can include parameters and a body.
* A lambda can have multiple lines. The last evaluated expression in the body is used as the lambda's return value.
* You can assign a lambda to a variable. The variable's type must be compatible with the type of the lambda.
* A lambda's type has the format: `(parameters) -> return_type`.
* Where possible, the compiler can infer the lambda's parameter types.
* If the lambda has a single parameter, you can replace it with `it`.
* You execute a lambda by invoking it. You do this by passing the lambda any parameters in parentheses, or by calling its `invoke` function.
* You can pass a lambda to a function as a parameter, or use one as a function's return value. A function that uses a lambda in this way is known as a higher-order function.
* If the final parameter of a function is a lambda, you can move the lambda outside the function's parentheses when you call the function.
* If a function has a single parameter that's a lambda, you can omit the parentheses when you call the function.
* A type alias let you provide an alternative name for an existing type. You define a type alias using `typealias`.

## Built-in higher-order functions

* Use `minBy` and `maxBy` to find the lowest or highest value in a collection. These functions take one parameter, a lambda whose body specifies the function criteria. The return type matches the type of items in the collection.
* Use `sumBy` or `sumByDouble` to return the sum of items in a collection. Its parameter, a lambda, specifies the thing you want to sum. If this is an `Int`, use `sumBy`, and if it's a `Double`, use `sumDouble`.
* The `filter` lets you search, or filter, a collection according to some criteria. You specify this criteria using a lambda, whose lambda body must return a `Boolean`. `filter` usually returns a `List`. If the function is being used with a `Map`, however, it returns a `Map` instead.
* The `map` function transforms the items in a collection according to some criteria that you specify using a lambda. It returns a `List`.
* `forEach` works like a `for` loop. It allows you to perform one or more actions for each item in a collection.
* Use `groupBy` to divide a collection into groups. It takes one parameter, a lambda, which defines how the function should group the items. The function returns a `Map`, which uses the lambda criteria for the keys, and a `List` for each value.
* The `fold` function lets you specify an initial value, and perform some operation for each item in a collection. It takes two parameters: the initial value and a lambda that specifies the operation you want to perform.

## Coroutines

* Coroutines let you run code asynchronously. They are useful for running background tasks.
* A coroutine is like a lightweight thread. Coroutines run on a shared pool of threads by default, and the same thread can run many coroutines.
* Use the `launch` function to launch a new coroutine.
* The `runBlocking` function blocks the current thread until the code it contains has finished running.
* The `delay` function suspends the code for a specified length of time. It can be used inside a coroutine, or inside a function that's marked using `suspend`.
