Vediamo cosa succede quando estendiamo ripetutamente una classe in Java

 - partiamo dalla classe DynamicStack
   1) aggiungiamo un attributo *max*
   2) aggiungiamo un attributo *size*
 
 ---
 Classe A ("originale")
 ```java
public class DynamicStack{
	protected Node top;
	public DynamicStack(){top = null;}
	public boolean empty(){return top==null;}
	public void push(int x) {top = new Node(x,top);
}

public int pop(){
	assert !empty();
	int x = top.getElem();
	top = top.getNext();
	return x;
}

public int top(){
	assert !empty();
	int x = top.getElem();
	return x;
}

public String toString(){
	Node temp = top; String s = "";
	while (temp!=null){
		s = s + " || " + temp.getElem() + "\n";
		temp = temp.getNext();
	}
	return s;
}

public DynamicStack(int n){
	top = null;
	int i = 1;
	while (i<=n) {
		top = new Node(i,top);
		i++;
	}
}
}
```
---
Classe B (sottoclasse di A)
```java
//DynamicStackMax.java
public class DynamicStackMax extends DynamicStack {
// Manteniamo il costruttore top di tipo Node e aggiungiamo
	private int max;
/* INVARIANTE di classe di DynamicStack: top punta alla cima della
pila. Aggiungiamo: SE lo stack non e` vuoto, allora max contiene il
massimo valore dello stack, se lo stack e' vuoto il valore di max e' arbitrario */
/* COSTRUTTORE. Dobbiamo spesso fornire un costruttore per le classi
estese: raramente il costruttore di default fornito da Java per una
estensione e' sensato */
public DynamicStackMax(){
	super();
//Invoco il costruttore della classe superiore con 0 argomenti
	max = 0;
// inizializziamo il nuovo attributo, max, anche se il suo valore
// non ha senso quando lo stack e' vuoto. Quando lo stack e' vuoto
// non consentiremo l'uso di max.
}
// NUOVO metodo get per il nuovo campo max
public int getMax(){
	assert !empty(); // se pila vuota: non corretto chiedere il massimo
	return max;
}
// OVERRIDE del metodo push(int n): inseriamo di un elemento in cima
// alla pila aggiornando il valore del massimo
public void push(int n){
	if (empty())
		max=n;
//se la pila e' vuota il massimo e' l'elemento n appena inserito
	else
//altrimenti e' il massimo tra elemento inserito e il max. precedente
		max = Math.max(max, n);
	super.push(n); //invoco il push della classe superiore
}
// NUOVO metodo per ricalcolare max, se abbiamo motivo per
// dubitare che max sia davvero il massimo della pila
// Nota: possiamo usare il nodo "top" della pila perche' abbiamo
// dichiarato top "protected" e quindi accessibile nelle classi che
// estendono DynamicStack oppure si trovano nella stessa cartella
private void resetMax(){
	if (!empty()){ //se la pila e' vuota ogni valore di max va bene
// altrimenti ricalcolo il massimo della pila
		max = top.getElem();
// calcolo il max tra il primo elemento della pila e gli altri
// per evitare di modificare l’indirizzo top della pila introduco
// una nuova variabile p di tipo nodo con valore subito dopo top
		for (Node p = top.getNext(); p != null; p = p.getNext())
			max = Math.max(max, p.getElem());
	}
}
// OVERRIDE di pop(): rimozione di un elemento dalla cima della pila
// Attenzione: puo' richiedere il ricalcolo del massimo
public int pop(){
	assert !empty();
	int n = super.pop(); //invoco il pop() della classe superiore
//Se l'elemento tolto e' il massimo allora il massimo puo' cambiare
// e quindi va ricalcolato
	if (n == max) resetMax();
		return n;
}
//EREDITA' Il metodo top() e' ereditato, non deve essere riscritto:
//leggere l'elemento in cima alla pila non cambia il max della pila
//OVERRIDE del metodo di conversione in stringa
public String toString()
{return super.toString() + " || max= " + max + "\n";}
}
```
---
Classe C(Sottoclasse di B\)
```java

//Ora estendiamo la classe estesa DynamicStackMax aggiungendo un attributo con il conto degli elementi della pila. Chiamiamo il risultato DynamicStackSize.
//DynamicStackSize.java
public class DynamicStackSize extends DynamicStackMax {
	private int size; // Aggiunta all’INVARIANTE di classe:
// "size" = numero elementi sullo stack
//COSTRUTTORE Dobbiamo quasi sempre definire un costruttore per le
// estensioni il costruttore di default in genere non e' affidabile
public DynamicStackSize(){
	super();
//Invoco il costruttore della classe superiore:0 argomenti
	size = 0;
}
// NUOVO metodo get per il nuovo campo size
public int getSize() { return size; }
// OVERRIDE del metodo push: inserimento elemento in cima alla pila
	public void push(int n) {
	super.push(n); //invoco il metodo push(n) della classe superiore
	size++; //aggiorno il numero degli elementi
}
// OVERRIDE del metodo pop: rimozione elemento dalla cima della pila
public int pop(){
	assert !empty();
	size--; //aggiorno il numero degli elementi
	return super.pop(); //invoco il metodo pop() della classe superiore
}
//EREDITA' top() viene ereditato e non deve essere riscritto: leggere
//l'elemento in cima alla pila non cambia il size della pila
//OVERRIDE del metodo di conversione in stringa
public String toString(){
	return super.toString() + " || size = " + size + "\n";
}
}

 ```
 
 **Diagramma UML per Stack dinamici e le loro estensioni**
 
 ![[Pasted image 20210420110418.png]]
 
 [[Diagramma UML]]