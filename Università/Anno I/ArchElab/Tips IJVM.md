## Tips random per la IJVM 
- $x>y$  --->  $x-y>0$   **usare IFLT**  vero $x<y$  / falso $x>y$ 
	(ragionamento inverso per $x<y$)

- $x≥y$  --->  $x-y≥0$   **usare IFLT**  vero $x<y$  / falso $x≥y$

- $x<=y$    
 ```java
 ILOAD X 
 ILOAD Y 
 ISUB 
 DUP //DUP per il secondo controllo ( IFLT ) 
 IFEQ XèY //Controllo se X-Y == 0 ovvero se X==Y
 XèY: //codice se x==y
 GOTO ... 
 //Se X-Y != 0 significa che X<Y o X>Y
 XdiversoY: IFLT XMinoreY 
 XMaggioreY: //codice se X>Y 
 GOTO ... 
 XMinoreY: //codice se X<Y 
 GOTO ...
 ```

