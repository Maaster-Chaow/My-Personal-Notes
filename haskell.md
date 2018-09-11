---
papersize: a4
mainfont: Times New Roman
---

# Haskell Notes

## Abstract Data Types

* Data constructors can take arguments.  
  Example:

  ```haskell
  data FailableDouble = Failure
                      | OK Double
                      deriving Show
  
  -- data constructors can accept more arguments.
  data Person = Person String Int String
    deriving Show
  ```

* Type and data constructors names must start with a capital letter,
  variables (including names of functions) must always start with a
  lowercase letter.

### Enumeration types

  Haskell allows programmmers to create their own _enumeration types_.  
  Example:

  ```haskell
  data Thing = Shoe       -- data constructors
             | Ship
             | SealingWax
             | Cabbage
             | King
    deriving Show
  ```

  This declares a new type `Thing`{haskell} with five _data constructors_
  `Shoe`{.haskell}, `Ship`{haskell}, etc. which are the (only) values of
  type `Thing`{haskell}.

### Recursive data types

* data types defined in term of themselves.

  ```haskell
  data IntList = Empty | Cons Int IntList

  data Tree = Leaf Char
            | Node Tree Int Tree
            deriving Show
  ```

* goes along with recursive functions.

  ```haskell
  intListProd :: IntList -> Int
  intListProd Empty      = 1
  intListProd (Cons x l) = x * intListProd l
  ```
<div style="page-break-after: always"></div>

## Pattern-matching
  
* Pattern matching is about taking apart a value by _finding out which
  constructor_ it was built with. This information can be used as the basis
  fpr deciding what to do.
* Few things to note when using pattern matching:  
  1. An underscore _ can be used as a wildcard pattern which matches
    anything.
  2. A pattern of the form `x@pat`{haskell} can be used to match a value
    against the pattern `pat`, but also give the name `x` to the entire
    value being matched.
    ```haskell
    baz :: Person -> String
    baz p@( Person n _ _ ) = "The name field of (" ++ show p ++ ") is " ++ n
    ```
  3. Patterns can be nested.
     ```haskell
     checkFav :: Person -> String
     checkFav (Person n _ SealingWax) = n ++ ", you're my kind of person!"
     checkFav (Person n _ _)          = n ++ ", your favorite thing is lame."
     ```
* In general, the grammar for a pattern is as:

  ```haskell
  pat ::= _
       |  var
       |  var @ ( par )
       |  ( Constructor pat1 pat2 ... patn )
  ```

## Case expressions

* The fundamental construct for doing pattern-matching.
* General form of case expression looks like:

  ```haskell
  case exp of
    pat1 -> exp1
    pat2 -> exp2
    ...
  ```

* When evaluated, the expression `exp` is matched against each of the
  patterns `pat1`, `pat2`, ... in turn. The first matching pattern is chosen,
  and the entire `case` expression evaluates to the expression corresponding
  to the matching pattern. For example,  

  ```haskell
  ex03 = case "Hello" of
            []        -> 3
            ('H':s)   -> length s
            _         -> 7
  ```

## Polymorphism

* Haskell supports polymorphism for both data types and functions.
  * _Polymorphic data types_  
  Example:

  ```haskell
  // This means List type is paramterized by a type t.
  data List t = E | C t (List t)
  ```

  The `t` here is a type variable which can stand for any type.
* Type variable must start with a lowecase letter whereas types
  must start with uppercase.

## Functions

* Functions which are well-defined on all possible inputs are 
  known as _total functions_.
* Functions which are proved to fail or recurse infinitely on 
  some input are called _partial functions_.
* To avoid writing partial functions there are two approaches:
  1. Change the output of the function to indicate possible
    failure(eg. Maybe values).
  2. if some condition is really guaranteed, then the types
    ought to reflect the guarantee! Then the compiler can enforce
    your guarantees for you.

## Short tips

* `words` : splits strings on spaces.
* `unwords` : joins a list of strings into a single string.
* `read` : converts a string to the value of given type.  
  Example:

  ```haskell
  print (read "1234" :: Int)
  ```

* `map` : apply a given function to every element of a list.
* `filter` : get only those element of a list which satisfy the
  given predicate.
* `fold` :
* `mapM_` : like map but allows sideeffects. Unlike `mapM` it discards
  the results.
* `Prelude` is a module with a bunch of standard definitions that 
  gets implicitly imported into every Haskell program.
* `Data.List` module contains many more list functions still.
* `Data.Maybe` module has functions for working with Maybe values.
