# Lisp Notes

## Facts about Lisp

* Automatic memory management, manifest typing, closures, etc.
* Designed to be extensible; lets you define new operators yourself.
* The language is made out the same functions and macros as the programs.
* Operators can take varying number of arguments and hence parentheses
  are needed to show where an expression begins and ends.
  ```lisp
  (+)                 ;> 0
  (+ 2)               ;> 2
  (+ 2 3)             ;> 5
  (+ 2 3 4)           ;> 9
  (+ 2 3 4 5)         ;> 14
  ```
