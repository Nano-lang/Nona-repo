![Build Status](https://github.com/Comcx/Nona/blob/master/icon/icon.svg)
# Nona the Programming Language 
***-- Experimental Nano with dependent types***  
***-- Latest version: Nona-0.5***  

```
   _____  _______  ____   ___ 
  / _  | / __   /~/ _  | / _ |___
 / / | |/ /_ / /~/ / | |/ __ |_____
/_/  |_|\_____/~/_/  |_/_/ |_|_______        by Comcx 

```

***NOTE!***
**Codes in `/src` are out-of-date**  
**EXE file which is fresh can be used directly**  
<br><br>

### >> Usage(Only support Win platform right now)

Jump to the directory where Nona-x.x.exe lies,  
input command: `.\Nona-0.5.exe` or just double click the EXE file

<img width="700" height="450" src="https://github.com/Comcx/Nona/blob/master/repl.jpg"/>

<br><br>
### >> Incomplete Intro  

* #### Expression :=
  - ***Const***  
  - ***Variable***  
  - ***(Fun params)***  
  - ***(: Expression type)***  
  - ***(= (bindings) Expression)***  
  - ***(if Expression Expression Expression)***
  - ***(\ (params) Expression)***  
  - ***(-> (: a t) a) -- for dependent function types***  
  <br>
  
* #### Declaration :=
  - ***(= var Expression)***  
  <br>
 
* #### Preluded terms:
  - ***(+ - * /) for Integers***  
  - ***(Int Bool String) which is Set***  
  - ***(, :0 :1) for tuples***  
  - ***:: for lists***  
  ...  
<br><br><br>

### >> Example
**
```
-- Example of function composition

(= (: . (-> (: a Set) (-> (: b Set) (-> (: c Set) (-> (-> b c) (-> (-> a b) (-> a c))))))) 
  (\ (a b c f g x) (f (g x))))

(= +1 (\ ((: x Int)) (+ x 1)))
(= *2 (\ ((: x Int)) (* x 2)))

(. Int Int Int +1 *2)


```
**








