### **Alberi di ricerca**
 Classe importaten per definire una strutturan dati dinamica e che consenta un accesso veloce

***Alberi binari interi***: 
- sono alberi vuoti, rappresentati con oggetti *Leaf* o con una *radice* con valore intero seguita da un sottoalbero sinistro ed uno destro
- Le radici dei sottoalberi sono detti nodi, le radici del sottoalbero sono dette figli sinistro e destro
- Un albero binario è "di ricerca" se la radice è maggiore di ogni nodo del sottoalbero sinistro e minore di ogni nodo del sottoalber destro (non ci sono nodi ripetuti)
 
esempio --> ![[Pasted image 20210506135352.png]] --> è un albero di ricerca


Ciò che conta in un albero sono icollegamenti, ma possono essere rappresentati in vari modi: ![[Pasted image 20210506135648.png]]

**Costruzione classe Tree per gli alberi di ricerca di interi**
- classe astratta ricorsiva *Tree*, ha 2 sottoclassi:
   - *Leaf*: alberi vuoti
   - *Branch*: alberi non vuoti
        - Branch può contenere elementi di Leaf e altri Branch
- Gli elementi di Tree sono dinamici e consentono di ricercare/inserire/eliminare un nodo in un tempo proporizionale al Log del numero di nodi (purchè siano bilanciati)
   - Come metodi di Tree definiamo:
      - *Boolean empty()* per dedicere se l'albero è vuoto
      - *int max()* calcolare il nodo massimo
      - *boolean contains(int x)* controllare se x è presente o meno
      - *Tree insert(int x)* || *Tree remove(int x)* per aggiungere e rimuovere un nodo
   -----
- Non è semplice rimuovere un nodo. Bisogna riconnettere i nodi in modo da mantenere lo stato di albero di ricerca (più complesso quando si rimuove la root)
- Quando scegliamo di modificare l'albero originale, scriviamo per sempio t.remove(x), ma t può cambiare e la variabile "t" può contenere un indirizzo errato. PEr questo di scrive t=t.remove(x), così da mantenere aggiornato l'indirizzo di t
   ---
 ```java
   //Tree.java classe astratta alberi binari di ricerca
// INVARIANTE DI CLASSE: ogni oggetto e' un albero di ricerca
// La classe astratta contiene il nome della classe, "Tree", e il
// minimo di metodi che richiediamo per formare una classe concreta
// di alberi.
public abstract class Tree {
//Test se l'albero e' vuoto
	public abstract boolean empty();
//Massimo elemento dell'albero, se non vuoto:
//in un albero binario e' il nodo piu' a destra
	public abstract int max();
//Test di appartenenza
	public abstract boolean contains(int x);
// Aggiunta di un elemento a un albero. Modifica l'albero
// precedente, la cui forma originaria va persa.
	public abstract Tree insert(int x);
// Si usa con t = t.insert(x), per salvare le modifiche fatte a t
// Rimozione di un elemento da un albero (se c'e'). Modifica
// l'albero precedente, che va perso.
	public abstract Tree remove(int x);
// Si usa con t = t.remove(x), per salvare le modifiche fatte a t
	protected abstract String toStringAux
	(String prefix, String root, String left, String right);
//Metodo che gestisce la parte NON pubblica della stampa.
//Non forniamo spiegazioni sul suo funzionamento, non e' essenziale
	public String toString(){
		return toStringAux("","___"," "," ");}
/* Trascrizione albero --> stringa. Ogni albero viene trascritto in
stringa dall’alto verso il basso, con i sottoalberi disegnati piu' a
destra dell’albero di cui fan parte */
} 
```
---
```java
//Leaf.java: i suoi oggetti (diversi da null) rappresentano alberi vuoti
// I metodi definiti in Leaf restituiscono risultati costanti indipententi.
public class Leaf extends Tree {
	public Leaf() { }
/** Il costruttore new Leaf() non assegna nulla e si puo' anche lasciare implicito. Un albero viene inizializzato da new Leaf() e poi esteso un elemento alla volta. Qui this = oggetto istanziato = albero vuoto (sempre). */
	public boolean empty(){return true;} //l'albero vuoto e' vuoto
	public int max(){assert false; return 0;} /** l'albero vuoto non ha
massimo, e' sbagliato chiederlo. **/
	public boolean contains(int x) {return false;}
//l'albero vuoto non contiene nulla
	public Tree insert(int x) {return new Branch(x, this, this);}
//se inserisco x ottengo l'albero di radice x e nessun figlio
//qui this è un oggetto di tipo Leaf: lo riuso, quindi non creo alberi vuoti nuovi.
//Nella classe Leaf abbiamo sempre: this = albero vuoto
	public Tree remove(int x) {return this;} //non c'e' nulla da cancellare nell'albero vuoto
//Metodo che gestisce la parte NON pubblica della stampa.
//Non forniamo spiegazioni sul suo funzionamento.
	protected String toStringAux (String prefix, String root, String left, String right)
	{return prefix + root + "leaf"; }
}
```
---
```java
/** Branch.java Sotto-classe di Tree degli alberi non vuoti:
    elem
   /    \
left    right
Gli elementi a sinistra sono minori di elem, quelli a destra sono maggiori */
public class Branch extends Tree {
	private int elem; //radice
	private Tree left; //nodi a sinistra: piu' piccoli della radice
	private Tree right; //nodi a destra: piu' grandi della radice
	public Branch(int elem, Tree left, Tree right){
		this.elem = elem; this.left = left; this.right = right;}
	public boolean empty(){ return false; }
// Un albero non vuoto non e' vuoto
	public int max(){ return right.empty() ? elem : right.max(); }
// se la parte destra e' vuota il nodo piu' grande e' la radice.
// Altrimenti il nodo piu' grande si trova a destra
	public boolean contains(int x){ /* Usa la RICERCA BINARIA, in media richiede tempo log_2(n) dove n = numero dei nodi. */
		if (x == elem) // abbiamo trovato l'elemento
			return true;
		else if (x < elem)
// x se c'e' si trova tra i nodi piu' piccoli a sinistra
			return left.contains(x);
		else //x>elem
// x se c'e' si trova tra i nodi piu' grandi a destra
			return right.contains(x);
	}
	public Tree insert(int x){ /** Inseriamo x preservando l'invariante "albero di ricerca": dunque x va inserito a sinistra se e' piu' piccolo della radice e a destra se e' piu' grande */
		if (x < elem)
			left = left.insert(x);
//e' essenziale aggiornare il valore di left
		else if (x > elem)
			right = right.insert(x);
//e' essenziale aggiornare il valore right
//altrimenti x=elem, x gia' presente nell'albero, non lo
//inseriamo
		return this;
/** Devo ricordarmi di restituire il valore aggiornato
dell'albero, altrimenti la modifica fatta va persa */
	}
	public Tree remove(int x){
		if (x == elem) // trovato elemento da eliminare
			if (left.empty())
// il sottoalbero sinistro e` vuoto, dunque resta il
// sottoalbero destro
				return right;
			else if (right.empty())
// il sottoalbero destro e` vuoto, dunque resta il
// sottoalbero sinistro
			return left;
		else{
			elem = left.max();
//rimpiazziamo elem con il massimo sin.
// per evitare ripetizioni,eliminiamo
// il massimo dal sottoalbero sin.
		left = left.remove(elem); //aggiorno left
		return this;
		}
	else if (x < elem) {
// se c'e', l'elemento da eliminare e` nel sottoalbero sinistro
		left = left.remove(x); //aggiorno left
		return this;
	}
	else {
// se c'e', l'elemento da eliminare e' nel sottoalbero destro
		right = right.remove(x); //aggiorno right
		return this;
	}
	}
//Metodo che gestisce la parte NON pubblica della stampa.
//Non forniamo spiegazioni sul suo funzionamento, non e' essenziale.
protected String toStringAux
(String prefix, String root, String left, String right){
return this.left.toStringAux(prefix+left, " /", " ", " ¦")
+ "\n" + prefix + root + "[" + elem + "]" + "\n" +
this.right.toStringAux(prefix+right, " \\", " ¦", " ");
	}
} 
```
----
```java
//TestTree.java. Per sperimentare la classe Tree degli alberi di ricerca
/* Per stampare un albero t, trascrivo t nella stringa t.toString(), con toString() ridefinito. Il comando e': System.out.println(t), abbreviazione di System.out.println(t.toString()) */
import java.util.*;
public class TestTree {
	public static void main(String[] args){
		Random r = new Random(); //r e' un generatore di numeri casuali
		int n = 8;
		Tree t = new Leaf(); //L'albero t nasce vuoto
		for (int i = 0; i < n; i++)
			t = t.insert(r.nextInt(n)); //Accresco t un elemento alla volta
//Provo il metodo di stampa e il calcolo del massimo
		System.out.println( "Stampa albero casuale t di al piu' " + n + " elementi \n\n" + t + "\n\n t.max() = " + t.max());
//Creo un albero u inserendo sempre elementi piu' grandi
//quindi sempre nella parte destra dell’albero
		Tree u = new Leaf();
		for (int i = 0; i < n; i++) u = u.insert(i);
			System.out.println( "\n Stampa albero u di " + n + " elementi, tutti figli destri \n\n" + u);
//Creo un albero u inserendo sempre elementi piu' piccoli
//quindi sempre nella parte sinistra dell’albero
		Tree v = new Leaf();
		for (int i = n-1; i >=0; i--) v = v.insert(i);
			System.out.println( "\n Stampa albero v di " + n + " elementi, elementi, tutti figli sinistri \n\n" + v);
		Tree w = new Leaf (); w=w.insert(3); w=w.insert(1); w=w.insert(4);
		w=w.insert(2); System.out.println( "\n Stampa albero w con insieme nodi = {1,2,3,4} \n\n" + w);
		w.remove(3); System.out.println( "\n w senza il nodo 3\n\n" + w);
	}
}
   ```
   
   
   