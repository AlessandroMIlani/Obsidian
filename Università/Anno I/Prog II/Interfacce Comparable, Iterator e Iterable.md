**Interfaccia Comparable\<Bottiglia>**
Dobbiamo aggiungere alla classe Bottiglia un implementazioen del metodo astratto compareTo(Bottiglia b).
 - Possiamo sfruttare *void Array.stort()* e *void Arrays.binarysearch()* per ordniare l'array ed eseguire ricerche.
 Li posso usare in una classe T generica , ma T deve implementare Comparable\<T>
 
 
Decidiamo di confrontare le bottiglie solo sul loro livello, ignorando la capacità:
 ```java
 //aggiungendo un confronto tra bottiglie basato sul solo livello
public class Bottiglia implements Comparable<Bottiglia>{
	private int capacita, livello; // 0 <= livello <= capacita'
	public Bottiglia(int capacita){
		this.capacita = capacita;
		livello = 0;
		assert (0<=livello) && (livello <= capacita);
	}
// Restituiamo la quantita' effettivamente aggiunta
	public int aggiungi(int quantita){
		assert quantita >= 0: "la quantita' doveva essere >=0 invece vale " + quantita;
		int aggiunta = Math.min(quantita, capacita-livello);
		livello = livello + aggiunta;
		assert (0<=livello) && (livello <= capacita);
		return aggiunta;
	}
// Restituiamo la quantita' effettivamente rimossa
	public int rimuovi(int quantita){
		assert quantita >= 0: "la quantita' doveva essere >=0 invece vale " + quantita;
		int rimossa = Math.min(quantita, livello);
		livello = livello - rimossa;
		assert (0<=livello) && (livello <= capacita);
		return rimossa;
	}
	public int getCapacita(){return this.capacita;}
	public int getLivello() {return this.livello;}
// Non consentiamo di cambiare la capacita'
	public void setLivello(int livello){
		this.livello = livello;
		assert (0<=livello) && (livello <= capacita);
	}
	public String toString(){
		return livello + "/" + capacita;
	}
	public int compareTo(Bottiglia b){return livello - b .livello;}
// La differenza di livello e' 0 se le bottiglie hanno lo stesso
// livello, e' >0 se this ha livello maggiore, e' <0 altrimenti
}// end class Bottiglia
```
---
```java
// ComparaBottiglie.java. Classe di test
import java.util.*; //Per la classe Arrays
public class ComparaBottiglie {
	public static void main(String[] args) {
		Bottiglia b1 = new Bottiglia(10); //bottiglia vuota di capacita' 10
		Bottiglia b2 = new Bottiglia(20); //bottiglia vuota di capacita' 20
		Bottiglia b3 = new Bottiglia(5); //bottiglia vuota di capacita' 5
		Bottiglia b4 = new Bottiglia(15); //bottiglia vuota di capacita' 15
//Riempo le prime 3 bottiglie, poi le confronto in base al livello
		b1.aggiungi(3); // b1 e' la piu' piena (la capacita' e'irrilevante)
		b2.aggiungi(2); // b2 e' intermedia
		b3.aggiungi(1); // b3 e' la meno piena
//b4 resta vuota || confronto in base al livello
		System.out.println( " confronto b1 (3 litri) con b2 (2 litri): " + b1.compareTo(b2));
		System.out.println( " confronto opposto: " + b2.compareTo(b1));
		System.out.println( " confronto b1 con b1: " + b1.compareTo(b1));
//ordinamento di un array di bottiglie in base al livello
		Bottiglia[] bottiglie = {b1, b2, b3}; //non aggiungo b4
// posso ordinare le bottiglie in questo array perche'
// Bottiglia implementa l'interfaccia Comparable
	System.out.println(" Ordino e stampo {b1, b2, b3}");
	Arrays.sort(bottiglie);
// Dato che "bottiglie" e' un array posso usare il "foreach"
	for (Bottiglia b : bottiglie) System.out.println(b);
//Posso eseguire la ricerca binaria della posizione di una bottiglia
//in questo array ordinato perche' Bottiglia implementa l'interfaccia
//Comparable<Bottiglia>. binarySearch(b) restituisce un numero
//negativo se b non e' presente
	System.out.println( " cerco posizione di b1 (3 litri) nell'array:
	" + Arrays.binarySearch(bottiglie, b1));
	System.out.println( " cerco posizione di b2 (2 litri) nell'array:
	" + Arrays.binarySearch(bottiglie, b2));
	System.out.println( " cerco posizione di b3 (1 litro) nell'array:
	" + Arrays.binarySearch(bottiglie, b3));
	System.out.println( " cerco posizione di b4 (0 litri) nell'array:
	" + Arrays.binarySearch(bottiglie, b4));
}	}
 ```
 
 **Interfaccia Iterable\<E>**
 Supponiamo di voler scorrere una lista, ma senza rendere pubblici gli indirizzi dei nodi, per impedirne una modifica dall'esterno.
 Riprendiamo quanto visto in [[Esempi di ereditarietà e array come liste]], ma struttiamo le interfacce: *Iterable\<E> e Iterator\<E>*:
 
 Consideriamo la classe ListExt di liste di oggetti di tipo int con attributo size a cui non volgiamo consentire modifiche.
 Per impedirlo implementiamo l'interfaccia *Iterable\<Integer>*, il che richiede la dichiarazione di *public ListIterator iterator()* che ri-etichetta una lista l come un oggetto ListIterator
 
 Per eseguire il tutto in modo sicuro, dobbimao implementare anche l'interfaccia Iterator\<E> (E = Integer), la quale contiene i metodi *boolena hasNext() e Integer next()* per conoscere sè si ci sono altri elemtenti ed il loro valore.
 
 A questo punto possiamo usare in ListExt il costrutto foreach: for (Integer e:l){...e...}, dove l è tipo ListExt.
 - Rietichetta l in ListIteretor ed esegue i metodi hasNext() e next()

Bisogna importare java.util dove si trovano le interfacce Iterator\<E> e Iterable\<E>

Codice d'esempio:

 ```java
// successivo (null se non c’è un nodo successivo)
public class Node {
	private int elem; private Node next;
	public Node(int elem, Node next){this.elem = elem;this.next = next;}
	public void setElem(int elem){this.elem = elem;}
	public int getElem(){return elem;}
	public Node getNext(){return next;}
	public void setNext(Node node){next = node;}
}
```
---
```java
// ListExt.java modifichiamo MiniLinkedList della Lezione 14
// cambiando il nome della classe e aggiungendo le implementazioni richieste.
import java.util.*; //per le interfacce Iterable<T>, Comparable<T>
/* Dichiariamo che ListExt implementa le interfacce Iterable e
 Comparable. Questo consentira' da un lato di usare il costrutto
 iterativo for-each di Java per iterare sugli elementi di una
 struttura e dall'altro di confrontare istanze della classe secondo l'ordine lessicografico */
public class ListExt implements Iterable<Integer>, Comparable<ListExt> {
	private Node first; private int size;
	public ListExt() {first = null;size = 0;}
	public int size(){return size;}
	private Node node(int i) {
		assert i >= 0 && i < size;
		Node p = first;
		while (p != null && i > 0) {p = p.getNext();i--;}
			assert p != null;
			return p;
		}
		public int get(int i){return node(i).getElem();}
		public void set(int i, int x){node(i).setElem(x);}
		public void add(int i, int x) {
		assert 0 <= i && i <= size;
		size++;
		if (i == 0)
			first = new Node(x, first);
		else {
			Node prev = node(i - 1);
			prev.setNext(new Node(x, prev.getNext()));
		}
	}
	public int remove(int i) {
		assert 0 <= i && i < size;
		size--;
		if (i == 0) {
		int x = first.getElem();
		first = first.getNext();
		return x;
	}
	else {
		Node prev = node(i - 1);
		Node p = prev.getNext();
		prev.setNext(p.getNext());
		return p.getElem();
	}
	}
// Implementazione di Iterator<Integer>: ridenomiamo un
// elemento di ListExt come un elemento di ListIterator
// e implementiamo Iterator<Integer> in ListIterator
	public ListIterator iterator() {return new ListIterator(first);}
// Implementazione di Comparable<ListExt>: confrontiamo due liste
// rispetto all’ordine lessicografico
	public int compareTo(ListExt lista) {
		Node p = this.first, q = lista.first;
//p, q = puntatori ai nodi delle due liste, scorro le due liste un passo alla volta
		while ((p != null) && (q != null)){
			if (p.getElem() != q.getElem()) //le due liste sono diverse
				return p.getElem() - q.getElem();
//valore positivo se la prima lista e' piu' grande, negativo se e' piu' piccola
			else //vado avanti in entrambe le liste
				{p = p.getNext(); q = q.getNext();}
		}
// quando il while finisce ho esaurito almeno una delle due liste
// trovando solo elementi uguali. La lista finita prima e' minore
	if (p == null) { // la prima lista e' finita
		if (q == null) // entrambe le liste sono finite
			return 0; // quindi sono uguali
		else //prima lista finita ma seconda lista no
			return -1;} //prima lista minore
	else //prima lista NON finita, dunque seconda lista e' finita
			return +1; // seconda lista minore
}	} 
```
---
```java
//ListIterator.java Questa classe deve implementare Iterator<Integer>
import java.util.*;
// ListIterator e' un semplice indirizzo di un nodo
public class ListIterator implements Iterator<Integer>{
	private Node next; //All’inizio = inizio lista
	public ListIterator(Node next){this.next = next;}
/* per implementare Iterator<Integer> occorre fornire:
1. un metodo boolean hasNext() che ci dica se esiste un prossimo
oggetto della lista da visitare
2. un metodo Integer next() che sposti next sul prossimo oggetto da
visitare nella collezione e ne restituisca il valore, un intero.
Notiamo che il valore originario di next viene perso, quindi la visita si fa una volta sola, per una seconda visita bisogna ricalcolare l.iterator() */
	public boolean hasNext(){return next != null;}
	public Integer next(){
		int x = next.getElem(); //contenuto del prossimo nodo
		next = next.getNext(); //indirizzo del nodo dopo ancora
		return x;
//x viene automaticamente trasformato da int a Integer (via auto-boxing)
	}
}
```
---
```java
//TestList.java. Sperimentiamo foreach e compareTo
//Se usiamo foreach non dobbiamo esplicitamente usare iterator()
public class TestList {
	public static void main(String[] args) {
	ListExt a = new ListExt();
	for (int i = 20; i >= 0; i--) a.add(0, i);
		System.out.println( " Lista a={0,...,20}");
	for (Integer o : a) System.out.println(o);
		ListExt b = new ListExt();
	for (int i = 10; i >= 0; i--) b.add(0, i);
		System.out.println( " Lista b={0,...,10} ");
	for (Integer o : b) System.out.println(o);
		System.out.println( " a.compareTo(b) = " + a.compareTo(b));
	System.out.println( " b.compareTo(a) = " + b.compareTo(a));
	System.out.println( " b.set(7,100): ora b maggiore"); b.set(7,100);
	System.out.println( " Nuova Lista b: ora b_7=100");
	for (Integer o : b) System.out.println(o);
		System.out.println( " a.compareTo(b) = " + a.compareTo(b));
	System.out.println( " b.compareTo(a) = " + b.compareTo(a));
	}
} 
 ```
 	
 
 
 