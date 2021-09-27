**nuovi esempi di dynamic binding**
In [[Graphics]] abbiamo usato class Figura di figure, con metodi in base al tipo esatto della figura.
Ora creiamo class Persona con 2 metodi di stampa uguali:
- *void scriviOutput()* e *void scriviNome()*
   - Riscriviamo scriviOutput() in ogni sottoclasse ma non scriviNome()
  
  [[Diagramma UML]] della classe Persona  ![[Pasted image 20210426152347.png]]
  
```java
//Persona.java
public class Persona{
	private String nome;
	public Persona(String nome){this.nome=nome;}
	public String getNome(){return nome;}
	public void setNome(String nome){this.nome=nome;}
//Metodo di scrittura di cui faccio OVERRIDE in ogni sottoclasse:
//si arricchisce man mano che ci sono piu' informazioni su un oggetto
	public void scriviOutput(){System.out.println( " nome = " + nome);}
//Metodo di scrittura di cui NON intendo fare OVERRIDE
//resta uguale anche se quando sono informazioni in piu'
	public void scriviNome(){System.out.println( " nome = " + nome);}
//Ma per ora i due metodi di scrittura sono uguali!
}
//Docente.java
	public class Docente extends Persona{
//Su un docente abbiamo delle informazioni in piu' che su una
//persona
	private int stipendio;
	public Docente(String nome, int stipendio)
	{super(nome); this.stipendio = stipendio;}
	public int getStipendio(){return stipendio;}
	public void setStipendio(int stipendio){this.stipendio=stipendio;}
//OVERRIDE di scriviOutput(): stampo le informazioni in piu'
	public void scriviOutput(){
		super.scriviOutput();
		System.out.println( " stipendio = " + stipendio);
	}
//NON faccio override di scriviNome():
//questo metodo viene semplicemente ereditato
}
//Studente.java
public class Studente extends Persona{
//Su uno studente abbiamo informazioni in piu' che su una persona
	private int matricola;
	public Studente(String nome, int matricola)
	{super(nome); this.matricola = matricola;}
	public int getMatricola(){return matricola;}
	public void setMatricola(int matricola){this.matricola=matricola;}
//OVERRIDE del metodo scriviOutput(): stampo le informazioni in piu'
	public void scriviOutput(){
		super.scriviOutput();
		System.out.println( " matricola = " + matricola);
	}
//NON faccio override di scriviNome(): questo metodo
//viene semplicemente ereditato
}
```

Quando usiamo void scriviOutput() e void scriviNome() ad oggetti studenti e docenti, viene usato il metodo definito nel tipo più vicino.
- scriviOutput() --> quello di studenti e docenti
- scriviNome()  --> quello della classe persona

```java
//PersonaDemo.java
public class PersonaDemo{public static void main(String[] args){
//Definisco delle persone appartenenti a sottoclassi
	Studente a = new Studente( "Rossi",111); //111=matricola
	Docente b = new Docente( "Ferrero",1000); //1000= stipendio
//Definisco un array con le persone appena introdotte
	int n=2; Persona[] c = new Persona[n]; c[0]=a;c[1]=b;
//tipo apparente c[0],c[1]: Persona, tipo esatto: Studente, Docente
//Stampo c usando il metodo scriviOutput() (CON override): Java
//utilizza il tipo "esatto" (il tipo originario) di ogni oggetto
//il metodo scriviOutput() per il tipo esatto
	System.out.println( "\nEsempio di scriviOutput()");
	for(int i=0;i<n;i++){System.out.println(i + " "); c[i].scriviOutput();}
//Stampo c usando il metodo scriviNome() (SENZA override):
//Java utilizza il tipo esatto di ogni oggetto e il metodo
//scriviNome() per il tipo esatto. IN QUESTO CASO IL METODO E'
//EREDITATO E RESTA SEMPRE LO STESSO (no override)
	System.out.println( "\nEsempio di scriviNome()");
	for(int i=0;i<n;i++){System.out.println(i + " "); c[i].scriviNome();}
	}
}
```

**MiniLinkedList e Iterator**
Definiamo le classi *MiniLinkedList* e *Iterator* necessarie per le liste e le loro interazioni

- **MiniLinkedList**
    - classe delle liste concatenate V con nodi V_0,...,V_(size-1), ogni nodo punta al successio ed ha attributo *size*
	- I metodi pubblici di MiniLinkedList sono:
	  int get(int i) || void set(int, int x) || void add(int i, int x) || int remove(int i)
	 [i = posizione, x = valore]
	 - assomiglia ad un array, con il vantaggio di una dimensiose dinamica, ma lo svantaggio di dover ripercorrere la lista per recuperare un valore

Per consentire una scansione più veloce (senza rendere le variabili pubbliche) andiamo a dichiarare la classe **MiniIterator**, con metodo *int next()* il quale legge il contenuto di un puntatore e sposta il puntatore al nodo dopo, <ins>senza modificare i puntatori dei nodi</ins>.
In questo modo, si può iterare lo stesso metodo su tutti gli elementi di una lista, senza modificarla.

```java
//Node.java Riutilizziamo la classe Node della Lezione 08
//MiniLinkedList.java
public class MiniLinkedList{
	private Node first; private int size;
// INVARIANTE DI CLASSE:(first=elemento n.0 della lista concatenata)
// e (size = numero nodi accessibili da first)
/** Costruttore della lista vuota con 0 elementi */
	public MiniLinkedList(){first = null; size = 0;}
	public int size() {return this.size;}
/** Metodo privato node(i) = indirizzo del nodo V_i della lista V.
Viene usato dalla classe per definire gli altri metodi*/
	private Node node(int i){//controllo che V_i sia un nodo della lista
		assert 0 <= i && i < size;
//creo una copia di first per non modificare l'originale
		Node p = this.first;
		while (i > 0){ //rimpiazzo per i volte: p con il nodo dopo
			assert p != null; //se vale l'invariante questo assert e' vero
			p = p.getNext(); i--;
		}
//Dopo aver applicato p = p.getNext() per i volte abbiamo p=node(i)
		assert p != null; //se vale l'invariante questo assert e' vero
		return p;
	}
/** DEFINIZIONE get(i), set(i,x), add(i,x), remove(i) usando node(i)
get(i) = contenuto node(i) */
	public int get(int i){return node(i).getElem();}
/** set(i,x) assegna node(i) ad x */
	public void set(int i, int x){node(i).setElem(x);}
/** add(i,x) aggiunge un nodo che contiene x in posizione i */
	public void add(int i, int x) {
		assert 0 <= i && i <= size;
		if (i == 0) {first = new Node(x, first);}
//aggiungo un nodo all'inizio
		else{ //calcolo il nodo precedente al nodo da aggiungere
			Node prev = node(i - 1);
//aggiungo un nodo tra prev e prev.getNext()
			prev.setNext(new Node(x, prev.getNext()));
		}
//l'invariante di classe e` temporaneamente non valido: size
//vale uno meno il numero di elementi della lista. Quindi
//aggiungiamo 1:
		size++;
	}
/** remove(i) elimina il nodo n. i e ne restituisce il contenuto x */
	public int remove(int i) {
		assert 0 <= i && i < size; int x;
		if (i == 0) {
//Elimino first. Nuovo first = Vecchio first.getNext()
			x = first.getElem();
			first = first.getNext();}
		else { //i>0
//Nodo prev precedente il nodo da eliminare = node(i-1)
			Node prev = node(i - 1);
//Nodo el da eliminare = nodo che viene dopo prev
			Node el = prev.getNext();
			x = el.getElem();
//Per eliminare el, collego prev al nodo che viene dopo el
			prev.setNext(el.getNext());
		}
// L'invariante di classe e` temporaneamente non valido: size vale
// 1 piu' il numero di elementi della lista. Dobbiamo sottrarre 1:
		size--;
		return x;
	}
/** Definiamo un metodo che ridenomina una MiniLinkedList in un
elemento della classe MiniIterator. MiniIterator consente di
eseguire un ciclo for senza rendere pubblici gli indirizzi dei nodi */
	public MiniIterator iterator(){
		return new MiniIterator(first);
	}
// Per visitare la lista l scrivo i = l.iterator() e faccio muovere
// i, si veda sotto nella classe Test
}
```

```java
/* MiniIterator.java. Classe che consente di traversare una volta sola una lista con un numero "size" di applicazioni di getNext() senza rendere pubblici gli indirizzi dei nodi */
public class MiniIterator {
	private Node next; // next = prossimo nodo da "visitare"
	public MiniIterator(Node first) {next = first;}
	public boolean hasNext(){return next != null;}
/* next() cancella il valore originale di next: la visita della lista l viene fatta una volta sola. Per fare un’altra visita devo creare un'altra volta un oggetto i = l.iterator() */
	public int next() {
		assert hasNext();
		int x = next.getElem();
		next = next.getNext();
		return x;
	}
}
```

```java
/** TestMiniIterator.java (controlliamo MiniLinkedList e MiniIterator)*/
public class TestMiniIterator {
	public static void main(String[] args) {
	MiniLinkedList l = new MiniLinkedList();
	for (int i = 0; i < 10; i++) l.add(0, i);
	System.out.println( "l.size() = " + l.size());
	System.out.println( "Cancello l_7 = 2");
	System.out.println( "l.remove(7) = " + l.remove(7));
	System.out.println( "l.size() = " + l.size());
	MiniIterator i = l.iterator();
	while (i.hasNext())
	System.out.println(i.next());
	}
}
```

[[Classi astratte di figure]]