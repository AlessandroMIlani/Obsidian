## Interfaccia
 - è un tipo che si presenta come una lista di metodi astratti, <u>senza nessnuna implementazione</u> (ma può contenere metodi statici)
 - non può avere metodi concreti
 - per definirla si sua la parola chiave "inteface" e la si estende con "implements"
      - per implementare uninterfaccia, dobbiamo sovvrascrivere tutti i suoi metodi sstratti
      - possiamo implementare più interfaccie "C implements I, J" (*impossibilie con le classi*, si crerebbero conflitti di ereditarietà)
          - Sè B estende A, ed A implementa J --> B implementa J
     
**Interfaccia Comparable\<T>**

è essenziale epr definire alberi di ricerca su classe generica T
Ha un unico metodo *compareTo(T y)* || x.compareTo(y)
   - Viene visto come un confronto con i seguenti return (Se y è di tipo T):
      - x < y --> return negativo
      - x == y --> return 0
      - x  > y --> return positivo
   
 Quando una classe C implementa Comparable\<C> dobbiamo anche fornire un implementazione di int *ompareTo(C y)*
 
 **Classe astratta Tree\<T extends Comparable\<T>> degli alberi di ricerca sulla classe T**
 
 Per costruire la classe gli alberi su una classe generica T, dobbiamo vincolare T.
 imponiamo "T implements I" --> I = Comparable\<T>, quindi imponiamo una relazione d'ordine a T, così da poter sfruttare compareTo
 
 *Esempio albero di ricerca*
 - albero di ricerca t={1,2,3} (tipo = Tree\<T>, con instanziamento T=Integer)
    - ha radice di t contiene elem 2 e gli indirizzi t.left e t.right  

Versione semplificata --> ![[Pasted image 20210508161843.png]]

Memoria Java --> ![[Pasted image 20210508161958.png]]

Codice d'esempio:
```java
//Tree.Java
// alberi di ricerca su una classe T
// vincolata a estendere l’interfaccia Comparable<T>
public abstract class Tree<T extends Comparable<T>>{
//alberi di ricerca su T con relazione di ordine x.compareTo(y)
	public abstract boolean empty();
	public abstract boolean contains(T x);
	public abstract T max();
//insert e remove restituiscono l’indirizzo dell’albero modificato
	public abstract Tree<T> insert(T x);
	public abstract Tree<T> remove(T x);
	protected abstract String toStringAux
	(String prefix, String root, String left, String right);
//Metodo che gestisce la parte NON pubblica della stampa.
//Non forniamo spiegazioni sul suo funzionamento, non e' essenziale
	public String toString(){
		return toStringAux("","___"," "," ");
	}
/* Trascrizione albero --> stringa. Ogni albero viene trascritto in
stringa dall’alto verso il basso, con i sottoalberi disegnati piu' a
destra dell’albero di cui fan parte */
}
```
---
```java
//Leaf.Java
//ALBERI VUOTI” con unico elemento (diverso da null): "leaf"
//non definisco nessun costruttore: di default ho new Leaf()
public class Leaf<T extends Comparable<T>> extends Tree<T>{
//contiene albero vuoto e null, qui this = albero vuoto sempre
	public boolean empty(){return true;}
	public boolean contains(T x){return false;}
	public T max(){assert false; return null;}
//insert e remove restituiscono l’indirizzo dell’albero modificato
	public Tree<T> insert(T x){return new Branch<T>(x, this, this);}
	public Tree<T> remove(T x){return this;}
	protected String toStringAux
	(String prefix, String root, String left, String right)
	{return prefix + root + "leaf";}
}// end class
```
---
```java
//Branch.java
//alberi di ricerca generici e non vuoti
public class Branch<T extends Comparable<T>> extends Tree<T>{
	private T elem; Tree<T> left; Tree<T> right;
	public Branch(T elem, Tree<T> left, Tree<T> right){
		this.elem=elem; this.left=left; this.right=right;}
	public boolean empty(){return false;}
	public boolean contains(T x){
		int c=x.compareTo(elem);
		if (c==0) //x=elem
			return true;
		else if (c<0) //x<elem
			return left.contains(x);
		else //c>0, x>elem
			return right.contains(x);
	}
	public T max(){
		if (right.empty())
			return elem;
		else //right non vuoto
				return right.max();
	}
//insert e remove restituiscono l’indirizzo dell’albero modificato
	public Tree<T> insert(T x){
		int c=x.compareTo(elem);
		if (c<0) //x<elem
			{left=left.insert(x);}
		else if (c>0) //x>elem
			{right=right.insert(x);}
//se c=0 allora x=elem e non inserisco x
		return this; // restituisco l’indirizzo dell’albero modificato
	}
	public Tree<T> remove(T x){
		int c=x.compareTo(elem);
		if (c<0) //x<elem
			{left=left.remove(x); return this;}
		else if (c>0) //x>elem
			{right=right.remove(x); return this;}
		else /* x=elem */
			if (left.empty())return right;
//cancello elem, se left=leaf resta right
			else if (right.empty())return left;
//cancello elem, se right=leaf resta left
			else{
//cancello elem, left e right non sono vuoti:
				elem=left.max(); //sost. elem con il max a sx
				left.remove(elem); //per evitare ripetizioni
				return this; // restituisco l’albero modificato
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
}// end class
```
---
```java
//Contatto.java Forniamo una classe C che implementa Comparable<C>
public class Contatto implements Comparable<Contatto>{
	private String nome; private String email;
	public Contatto(String nome, String email)
		{this.nome=nome;this.email=email;}
	public String getNome(){return nome;}
	public void setNome(String nome){this.nome=nome;}
	public String getEmail(){return email;}
	public void setEmail(String nome){this.email=email;}
	public String toString(){return nome + "<" + email + ">";}
//Implemento un metodo compareTo nella classe Contatto
	public int compareTo(Contatto x){return nome.compareTo(x.nome);
	}
}// end class Contatto
```
---
```java
//TestTree.java. Instanzio Tree su diverse classi che implementano
//l’interfaccia Comparable<T>
import java.util.*; //per la classe Random
//Provo l'implementazione degli alberi binari di ricerca
public class TestTree {
	public static void Title(String s){ //Stampa di un titolo
	System.out.println( "--------------------------------------"
	+ "\n" + s + "\n" +
	"--------------------------------------");}
public static void main(String[] args){
	Random r = new Random(); //r = un generatore di numeri casuali
//Creo un albero t con n reali casuali tra 0 e 1
	int n = 8;
	Tree<Double> t = new Leaf<>(); //L'albero t nasce vuoto
	for (int i = 0; i < n; i++)
		t = t.insert(r.nextDouble()); //Accresco t un elem. alla volta
//Provo il metodo di stampa e il calcolo del massimo
	Title( "Stampa albero casuale t di " + n + " elementi");
	System.out.println(t + "\n\n t.max() = " + t.max());
//Creo un albero u di interi inserendo sempre elementi piu' grandi
//quindi sempre a destra
	Tree<Integer> u = new Leaf<>();
	for (int i = 0; i < n; i++) u = u.insert(i);
		Title( "Stampa albero u di " + n + " elementi, tutti figli destri");
	System.out.println(u);
//Creo un albero u di stringhe inserendo sempre elementi piu' piccoli
//quindi sempre a sinistra
	Tree<String> v = new Leaf<>();
	for (int i = n-1; i >=0; i--) v = v.insert( "numero " + i);
		Title("Stampa albero v di "+n+" elementi, tutti figli sinistri");
	System.out.println(v);
//Provo il metodo di cancellazione per un albero di contatti
	Tree<Contatto> w = new Leaf<>();
	Contatto c = new Contatto( "Cafasso", "cafasso@ristorante");
	Contatto a = new Contatto( "Anfossi", "anfossi@scuola");
	Contatto d = new Contatto( "Davanzo", "davanzo@comune");
	Contatto b = new Contatto( "Borghi", "borghi@ditta");
	w=w.insert(c);w=w.insert(a);w=w.insert(d);w=w.insert(b);
	Title("Stampa albero w di contatti {a,b,c,d}");
	System.out.println(w);
	Title("w senza il contatto c"); w.remove(c);
	System.out.println(w);
}	}
```
 [[Interfacce Comparable, Iterator e Iterable]]