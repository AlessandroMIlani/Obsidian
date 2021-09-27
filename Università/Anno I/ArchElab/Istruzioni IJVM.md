### Istruzioni IJVM
Istruzioni della **IJVM** e relative descrizioni

- Scrive un Byte in cima allo *Stack* 
```java
BIPUSH byte
```

- Legge la parola in cima allo stack e la inserisce in cima allo Stack 
```java
DUP
```

 - Diramazione incondizionata
 ```java
 GOTO offset
 ```
 
 - Sostituisce le 2 parole in cima allo stack con la loro somma
```java
IADD
```
  
  - Sostituisce le 2 parole in cima allo stack con in loro **AND**
```java
IAND
```
  
  - Estrae una parola dalla cima dello stack ed esegue la diramazione se vale zero
```java
IFEQ offset
```
  
  - Estrae una parola dalla cima dello stack ed esegue la diramazione se ha valore negativo
  ```java
  IFLT offset
  ```
  
  - Estrate 2 parole dalla cima dello stack ed esegue una diramazione se sono uguali 
```java
IF_ICMPEQ offset
```
  
  - Aggiunge una costante ad una variabile locale
```java
IINC varnum const
```
  
  - Scrive una variabile locale in cima allo Stack
```java
ILOAD varnum
```
  
  - Invoca un metodo
```java
INVOKEVIRTUAL disp
```
  
  - Sostituisce 2 parole in cima allo stack con il loro **OR**
```java
IOR
```
  
  - termina un metodo restituendo un valore intero
```java
IRETURN
```
  
  - Preleva una parola in cima allo stack e la memorizza in una variabile locale
```java
ISTORE varnum
```
  
  - Sostituisce 2 parole in cima allo stack con la loro differenza
```java
ISUB
```
  
  - Scrive in cima allo stack una costante proveniente dalla porzione costante di memoria
```java
LDC_W index
```

- Non eseguen nulla
```java
NOP
```

- Rimuove la cima dello Stack
```java
POP
```

- Scambia le 2 parole in cima allo stack
```java
SWAP
```

- Istruzione prefisso: l'istruzione successiva ha un indice a 16 bit
```java
WIDE
```

- Interrompe l'esecuzione del file
```java
HALT
```

- Restituisce in output l'ultimo valore nello stack
```java
OUT
```

[[Tips IJVM]]