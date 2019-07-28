# Kotlin Map

## Variables

### Keywords

- `val`
- `var`

### Type

- Statically
- Type inference
- Primitive types
  - Numeric types
    - `Byte`
    - `Short`
    - `Int`
    - `Long`
    - `Float`
    - `Double`
    - Number conversions
  - `Boolean`
  - `Char`
  - `String`
    - String templates
    - Triple-quoted string
      - Avoid escaping characters
      - Multiline
    - Regular expression
      - `toRegex`
- Non-null
- Nullable
  - Safe call `?.`
  - Elvis operator `?:`
  - Non-null assertion `!!`
- Function types
- Platform types

## Functions

### Keyword

- `fun`

### Return type

- [Type](#Type)
- `Unit`
- `Nothing`

### Single expression

### Default parameter values

### Named arguments

### `vararg`

- `*` (spread operator)

### `infix`

### `tailrec`

### Local function

## Control structures

- `if...else...`
- `while`
- `do...while`
- `for...in`
- `when`
- Range
  - `1..10`
  - `1 until 10`
  - `10 downTo 1 step 2`
  - `IntRange`
  - `LongRange`
  - `CharRange`

## Packages

### Import

- Classes/functions/properties renaming `as`

### Files

- Top level
  - Properties
  - Functions

- Classes
  - Keyword `class`
  - Visibility modifier
    - `public`
    - `protected`
    - `internal`
    - `private`
  - Constructors
    - Primary
    - Secondary
    - `init` block
  - [Functions](#Functions)
  - Properties
    - Decorator
      - `const`
        - Primitive type only
      - `lateinit`
    - Custom accessors
      - Getter
      - Setter
      - Visibility modifier
  - `object`
    - `companion object`
    - Expression
    - Singleton
    - Anonymous inner class object
  - Inner class
    - `this@Class`
    - reference to outer class
  - Nested class
    - `static`
  - Extensions
    - Properties
      - No backing field
      - getter required
      - Initializer prohibited
      - `var` for mutable receiver
    - Functions
    - Companion object
    - Import
    - No overriding

## Inheritance

### Any

- `equals()`
- `hashCode()`
- `toString()`

### data class

- Equality
- Destructure
- Copy
- Properties in primary constructor

### Hierachy

- Declaration `:`
- `open`
- `abstract`
- `override`
- `final`
- `is`
  - Smart cast
- `as`
  - Safe cast `as?`
- `super`

### Abstract classes

- Property
  - Abstract
  - Concrete

- Function
  - Abstract
  - Concrete

### Interfaces

- Property
  - Abstract
  - Accessors
    - No backing field

- Functions
  - Abstract
  - Concrete

### Enums

- Keyword `enum class`
- Constructors
- Functions
- Common properties
  - `name`
  - `ordinal`
- Common functions
  - `valueOf`
  - `values`
- Exhaustive when

### Sealed classes

- Keyword `sealed class`
- Inheritance
- Restricted
  - Exhaustive when
- Subclass
  - Nested
  - The same file

## Generics

- Nullability of type parameters
- `in`
- `out`

## Delegations

- Keyword `by`

### Interface implementation by delegation

### Delegated properties

- `val`
  - `lazy`
  - `Map`
- `var`
  - `MutableMap`
  - `Delegates.observable`

## Collections

### Array

- `arrayOf`
- `arrayOfNulls`
- Array constructors
- Primitive type
  - `IntArray`
  - `CharArray`
  - ...

### List

### Set

- Equality

### Map

### Conversion functions

- `toList`
- `toSet`
- `toTypedArray`

### Mutable

- `MutableIterator`

### Sequence

- Creation
  - `asSequence`
  - `generateSequence`
- Sequence operations
  - Intermediate
    - `filter`
    - ...
  - Terminal
    - `toList`
    - ...

## Functional

### Philosophy

- First-class functions
- Immutability
- No side effects
- Safe multi threading
- Easier testing

### Function types

- Basic pattern
  - `(parameters) -> return_type`
- Receiver function type
  - `Receiver.(parameters) -> return_type`
- Suspending function type
  - `suspend (parameters) -> return_type`
  - `suspend Receiver.(parameters) -> return_type`
- Nullable
- Combinable
  - `(Int) -> ((Int) -> Unit)`
- `typealias`
- Instantiating
  - Lambda expression
  - Anonymous function
  - Callable reference to existing declaration
  - Instance of classes implemented function type interface
- `invoke`

### Lambda

- Expression
  - `run`
- `it`
- `_`
- As last parameter
- Variables capturing
- `inline` functions
- return
  - `return@`
  - `fun`
- *SAM* constructors
- Scope functions (lambdas with receivers)
  - `let`
  - `apply`
  - `with`
  - `also`
  - `run`

### Higher-order functions

- Built-in functions
  - Aggregate operations
    - `all`
    - `any`
    - `none`
    - `count`
    - `fold(Right)`
    - `forEach(Indexed)`
    - `max(By)`
    - `min(By)`
    - `reduce(Right)`
    - `sum(By)`
  - Filtering operations
    - `drop`
    - `dropWhile`
    - `dropLastWhile`
    - `filter`
    - `filterNot`
    - `filterNotNull`
    - `slice`
    - `take`
    - `takeLast`
    - `takeWhile`
  - Mapping operations
    - `map`
    - `mapIndexed`
    - `mapNotNull`
    - `flatMap`
    - `groupBy`
  - Elements operations
    - `contains`
    - `elementAt`
    - `elementAtOrElse`
    - `elementAtOrNull`
    - `find`
    - `first`
    - `firstOrNull`
    - `indexOf`
    - `indexOfFirst`
    - `indexOfLast`
    - `last`
    - `lastIndexOf`
    - `lastOrNull`
    - `single`
    - `singleOrNull`
  - Generation operations
    - `merge`
    - `partition`
    - `plus`
    - `zip`
    - `unzip`
  - Ordering operations
    - `reverse`
    - `sort`
    - `sortBy`
    - `sortDescending`
    - `sortByDescending`

## Operator overloading

- Keyword `operator`
- Operators
  - `plus`
  - `minus`
  - `times`
  - `div`
  - `mod`
  - `rangeTo`
  - `contains`
  - `get`
  - `equals`
  - …

## Exceptions

### Unchecked

## Coroutines

### Scope

- `launch`
- `async`
- `await`
- `suspend`

### Context

- `Dispatcher`
- `Job`

## Interoperate

- `@JvmStatic`
- `@JvmOverloads`
- `@JvmName`
- `@JvmField`
