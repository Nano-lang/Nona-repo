# Nona : Lazy Programming Language with Dependent Types
![Build Status](https://github.com/Comcx/Nona/blob/master/icon/icon.svg)
![Documentation Status](https://github.com/Comcx/Nona/blob/master/icon/doc-passing.svg)  
  
***Experimental Nano with dependent types***  
***Latest version: Nona-0.8.6***  

```
   __________________________
  / ___  / ___  / ___  / _  |
 / /  / / /__/ / /  / / __  |
/_/  /_/______/_/  /_/_/ |__|     by Comcx

```

***NOTE!***
**Codes in `/src` are out-of-date**  
**EXE file which is fresh can be used directly**  
<br><br>

## Getting Started!

Nona only support `Windows 64bits` and `Linux 64bits` platform right now.  

```
Jump to the directory where Nona-x.x.exe lies,  
(cond 
    (use-windows 
      (input command: '.\Nona-0.8.6.exe' or just double click the EXE file))
    (use-linux
      (input command: '.\Nona-0.8.6-linux')))
```

<img width="740" height="500" src="https://github.com/Comcx/Nona/blob/master/repl-0.8.5.JPG"/>

<br><br>
## Incomplete Intro  

* #### Expression :=
  |Format                               | Explanation|
  |-------------------------------------|-------------|
  |***Variable***                       | Single variable|
  |***(Fun params)***                   | Lambda application|
  |***(: Expr type)***                  | Type signature|
  |***(= (bindings) Expr)***            | Bindings|
  |***(=o (pattern) Expr)***            | Recursive bindings|
  |***(=: (bindings) Expr)***           | Inductive families|
  |***(if Expr Expr Expr)***            | Conditional|
  |***(\ (params) Expr)***              | Lambda abstraction|
  |***(-> (: a t) b)***                 | Dependent function space|
  <br>
  
* ### Declaration :=
  - ***(= pattern Expression)***  
  - ***(=o pattern Expression)***  
  - ***(=: var Type)***
  - ***(: Expr Type)***
  <br>
 
* ### Preluded terms:
  |Terms                              |Explanation|
  |-----------------------------------|-----------|
  |***(0 1 2 ..)***                   |with type `Int`| 
  |***(+ - * /)***                    |for Integers|  
  |***"_"***                          |with type `String`|  
  |***(true false)***                 |with type `Bool`|  
  |***(Int Bool String Symbol IO)***  |which is Set|  
  |***(, fst snd)***                  |for tuples !note moved to lib right now!!|  
  |***:: () list***                   |for lists|
  |***print***                        |to print|
  ...  
<br><br><br>

* ### REPL use  
  
  - **Global environment:**  
    You can:  
      type in `(=  <pattern>  <expression>)` to add definition to global environment;  
      type in `(=o <pattern>  <expression>)` to add recursive definition to global environment;  
      type in `(=: <variable> <type>)` to construct new types to global environment.  
    
  - **Commands:**  
    `version` to show current version  
    `(quit)` to quit repl  
    `(help)` to ask for help  
    `(type <expr>)` to show type info  
    `(na <file>)` to load defs  
    `(no <file>)` to load *.no files  
    ...  
    
## Features  
   - Lexical scope mangement  
   - Purely functional  
   - Inductive family  
   - Dependent type system  
   - Type inference with unification  
   - Church numeral can be built(refer to lib/Prelude.na)  
   - First class record and typeclass  
   - String == (List Symbol)  
   ...  
   
     
## Examples

```scala
(Module Test ( -- The test file


-- Ploymorphism & Dependent types
(= (: id (-> (: a Set) a a)) (\ (a x) x))
(= (: .  (-> (: a Set) (: b Set) (: c Set) (-> b c) (-> a b) (-> a c))) 
    (\ (a b c f g x) (f (g x))))
(= (: weird (-> (: x Int) (if (== x 0) Int Bool) String))
    (\ (x a) "OK"))


-- Boolean functions
(= (not b)   (if b false true))
(= (and (: a Bool) (: b Bool)) (if a b false))
(= (or  a b) (if a true b))
(= (xor a b) (if (and (or a b) (not (and a b))) true false))


-- Inductive dependent sum pair
(=: Sum (-> (: A Set) (: B (-> A Set)) Set))
(=: ,   (-> (: A Set) (: B (-> A Set)) (: a A) (: b (B a)) (Sum A B)))

-- Recursion
(=o ((: fact (-> Int Int)) n)
  (if (== n 0) 1 (* n (fact (- n 1)))))

(: foldl-Int (-> (: b Set) (-> b Int b) b (List Int) b))
(=o (foldl-Int b h x xs)
    (if (== (head Int xs) 0) x
      (foldl-Int b h (h x (head Int xs)) (tail Int xs))))

(: circle (-> (: a Set) a Int (List a)))
(=o (circle a x n)
  (if (== n 0) (() a) (:: a x (circle a x (- n 1)))))

(=o ((: ^ (-> Int Int Int)) x n)
  (if (== n 0) 1 (* x (^ x (- n 1)))))


))--------- end of Test ---------((



```

## Drawbacks

* Not support weak normal head form(WNHF), not completely lazy...
* Lack support of pattern matching for dependent types
* ...








