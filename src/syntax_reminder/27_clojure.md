<!-- markdownlint-disable MD001 -->

# Clojure

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Error handling](#error-handling)

### Print

``` clojure
(println "Hello World")
```

### Variables

``` clojure
(def x 4)
(def x "hello")
(def x true)
```

### Data types

``` clojure
;; Integer
(def x 4)

;; Float
(def x 4.5)

;; String
(def x "hello")

;; List
(list 1 2 3)

;; Set
(set '(1 2 3))

;; Vector
(vector 1 2 3)

;; Map
(hash-map "a" 1 "b" 2 "a" 3)
```

### Operators

``` clojure
;; Arithmetic operators
(+ 1 2) ;; addition
rem ;; modulo (remainder)

;; Logical operators
= ;; equal
not= ;; not equal
and ;; AND
or ;; OR
not ;; NOT

;; Bitwise operators
bit-and ;; AND
bit-or ;; OR
bit-xor ;; XOR
bit-not ;; NOT
```

### Control flow

``` clojure
;; if-else
(if (= a b)
    (println "equal")
    (println "not equal"))
```

### Functions

``` clojure
(defn my_function [x y] (+ x y))

;; Call function
(my_function)

;; Anonymous function
(fn [x y] (+ x y))
```

### Error handling

``` clojure
(try
    (def content (slurp "my_file.txt"))
    (println content)
    (catch Exception e (println (str "Can't open file: " (.getMessage e)))))
```
