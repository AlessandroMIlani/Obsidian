[[Estensioni ripetute di classi]]

Se supponiamo "class C extends D" --> ogni oggetto di tipo C è nache un oggetto di tipo D (in quanto ne possiede tutti gli attributi)
Questa operazione è detta **Upcasting**
- Viene detto **tipo esatto**, il tipo con cui è stato costruto l'oggetto (tramite new())
    - Un oggetto può avere come *tipo*, tutti quelli che quelli che includono il suo tipo esatto

L'opposto dell'Upcast è detto **Downcasting**
- Se "obj" ha tipo apparente D allora:
	-   ((C) obj) indica "obj con tipo C" se "obj" è tipo esatto C o incluso in C
	-  Altrimenti calcolare ((C) obj) solleva l'eccezione **ClassCastException** e termina
	
*((C) obj)* andrebbe utilizzato solo se si è assolutamente certi che "obj ha tipo esatto C o inlcuso in C

Si chiama **tipo apparente** di un espressione, il tipo con cui la variabile è dichiarata

- Durante l'esecuzione Java riconosce il tipo esatto dai valori delle variabili dell'espressione
- Il tipo esatto è utilizzato per decidere quale vertsione di un metodo applicare all'oggetto questo meccanismo è detto:
  -  **Dynamic binding** se avviene a *run time*
  -  **Late binding** se avviene *dopo la compilazione*
 
 Esempio:
 ```java
 //Bottiglia.java. Riutilizziamo il programma della Lezione 05
//BottigliaConTappo.java. Riutilizziamo il programma della Lezione 11
// TestCast.java ESPERIMENTI SUL TIPO ESATTO DI UN OGGETTO
// tipo esatto di un oggetto = tipo C con cui l’oggetto x nasce
// x ha anche tipo (non esatto) ogni classe D che contiene C
public class TestCast {public static void main(String[] args){
// ESEMPIO. A seconda se la circostanza "oggi_piove" e' vera o
// falsa, il tipo esatto di b e' la sottoclasse oppure la classe.
	boolean oggi_piove = true; // Provate entrambe le possibilita’.
// UPCAST: il passaggio a una classe superiore. E' sempre corretto.
	Bottiglia b;
	if (oggi_piove) b = new BottigliaConTappo(10);
// upcast: b proviene da BottigliaConTappo e' spostato in Bottiglia
		else b = new Bottiglia(10);
// Se oggi_piove=true allora b si trova in BottigliaConTappo
// Se oggi_piove=true allora b non si trova in BottigliaConTappo
// DOWNCAST: passaggio a una classe inferiore. Funziona SOLO
// nel caso in cui l'oggetto apparteneva GIA' alla classe
// inferiore ed e' stato spostato nella superiore da un upcast.
// ESEMPIO. Il prossimo downcast appare corretto al compilatore
// Java, il quale non ha modo di sapere se il tipo esatto di b e`
// Bottiglia o BottigliaConTappo. A tempo di esecuzione viene
// fatto un controllo sul tipo esatto di b e il downcast
// fallisce (causando la terminazione anticipata del programma) se b
// risulta avere tipo esatto Bottiglia
	BottigliaConTappo t = (BottigliaConTappo) b;
// SE b si trovava gia' in BottigliaConTappo ed e' stato spostato in
// Bottiglia allora il donwcast ha successo e scrivo:
	System.out.println( "Downcast avvenuto con successo");
// ALTRIMENTI il programma termina con una ClassCastException
// Dopo il downcast possiamo applicare a t un metodo aperta()
// che esiste solo nella sottoclasse BottigliaConTappo
	System.out.println( "t.aperta() = " + t.aperta());
// Non possiamo scrivere b.aperta(), anche se nell’esecuzione b=t:
// System.out.println( "b.aperta() = " + b.aperta());
// Il controllo di tipo del programma usa il tipo apparente
// Bottiglia
// di b, e nel tipo Bottiglia il metodo aperta non c'e'.
	}
}
 ```
 
Per evitare di imbatterci in un **ClassCastException**, durante il downcast dobbiamo fare un test (obj instanceof C)
  - se è true, possiamo eseguire ((C) obj)

 ```java
// t instanceof T = true se e solo se
// t = oggetto istanziato (non null) di tipo T
public class InstanceOfDemo {
	public static void main(String[] args){
	Bottiglia s = new BottigliaConTappo(10), t = new Bottiglia(10);
//s,t definiti da costruttore quindi !=null
	BottigliaConTappo u = null;
	System.out.println( "s instanceof BottigliaConTappo = " + (s instanceof BottigliaConTappo)); // true
	System.out.println( "t instanceof BottigliaConTappo = " + (t instanceof BottigliaConTappo)); // false
	System.out.println( "u instanceof BottigliaConTappo = " + (u instanceof BottigliaConTappo)); // false
	}
}
 ```
 
 [[Graphics]]