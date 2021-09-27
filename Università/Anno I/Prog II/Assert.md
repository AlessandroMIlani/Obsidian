## Assert
L’assert indica una condizione che il programmatore ritiene vera in una determinata riga del programma, e che vuole controllare.
Fa terminare il programma, nel caso non sia vera.
```java
	public static int sqrt(int x) {
		assert (x >= 0):" sqrt(" + x + ") ";
		return (int) Math.sqrt((double) x);
	}
```
in qeusto caso, se x<0, termina il programma.