## Primo esempio di un estensione di classe
Vediamo come definire una classe D, da una classe C data, aggiungendo metodi/attributi.
Utile per ridurre il lavoro ed evitare moltiplicazione degli errori.
#### D è detta estensione o sottoclasse di C
Partiamo dalla classe Bottiglia
```java
// Bottiglia.java

public class Bottiglia{

 // quantita' intere espresse in litri
 private int capacita; // 0 <= capacita
 private int livello; // 0 <= livello <= capacita
 public Bottiglia(int capacita){
 this.capacita = capacita;
 livello = 0;
 assert (0<=livello) && (livello <= capacita);
 }
 
 /* Aggiungiamo tutta la parte di una quantita' data che trova posto
 nella bottiglia e restituiamo la quantita effettivamente aggiunta */
 public int aggiungi(int quantita){
 	assert quantita >= 0;
 	int aggiunta = Math.min(quantita, capacita-livello);
 	livello = livello + aggiunta;
 	assert (0<=livello) && (livello <= capacita);
 	return aggiunta;
 }

 /* Rimuoviamo la quantita' richiesta se c'e', altrimenti togliamo
 tutto, restituiamo la quantita' effettivamente rimossa */
 public int rimuovi(int quantita){
 	int rimossa = Math.min(quantita, livello);
 	livello = livello - rimossa;
 	assert (0<=livello) && (livello <= capacita);
 	return rimossa;
 }

 public int getCapacita(){ return this.capacita; }
 public int getLivello() { return this.livello; }
 
 public void setLivello(int livello){
 	this.livello = livello;
 	assert (0<=livello) && (livello <= capacita);
 }

 public String toString() //conversione bottiglia --> stringa
 {return " " + livello + "/" + capacita;}
 }
```

### Estensione di una classe
Aggiungiamo l'attributo (booleano) Tappo alla classe bottiglia.
Ci conviene immaginare una classe D estensione di una classe C come una **sottoclasse di C**.

## Vantaggi estensione
- aggiungere attributi/metodi
- riutilizzare att/met pubblici
- rendere pub. att/met privati
- fare Override di un metodo

L'aggiunta del tappo comporrta un Override delle classi "aggiungi" e "rimuovi"

**Sinstassi classe estesa**: 
- "Class D extends C"
- All'interno di D, per rifarci ali metodi e attributi di C usiamo "super" Es:
  - super(capacita);
  - super.aggiungi(quantita);

```java
// BottigliaConTappo.java
public class BottigliaConTappo extends Bottiglia {
/* NUOVO attributo privato per memorizzare lo stato della bottiglia (true = bottiglia aperta, false = bottiglia chiusa) */
	private boolean aperta;
/* NUOVO costruttore. Spesso dobbiamo definire un costruttore per le classi estese: raramente il costruttore di default fornito da Java per una estensione e' sensato */
	public BottigliaConTappo(int capacita){
/* invochiamo il costruttore della classe base per fare le
inizializzazioni della capacita' */
	super(capacita);
// supponiamo che la bottiglia sia inizialmente chiusa
	aperta = false;
}

// NUOVO metodo get per sapere se la bottiglia e` aperta o chiusa
public boolean aperta(){ return aperta; }
// NUOVO metodo per aprire la bottiglia
public void apri() { aperta = true; }
// NUOVO metodo per chiudere la bottiglia
public void chiudi() { aperta = false; }

// Ereditiamo i metodi get, set e toString() da Bottiglia
/* OVERRIDE del metodo "aggiungi" per versare liquido nella bottiglia: richiediamo che la bottiglia sia aperta. Dal momento che "aggiungi" deve restituire la quantita` di liquido aggiunto anche nel caso in cui la bottiglia sia chiusa, dobbiamo restituire un valore sensato (0 in questo caso) */
public int aggiungi(int quantita){
	if (aperta)
		return super.aggiungi(quantita); /*super.aggiungi() indica il metodo "aggiungi" 	nella classe Bottiglia che stiamo estendendo */
	else return 0;
}

/* OVERRIDE del metodo "rimuovi" per versare liquido dalla bottiglia: stesse osservazioni */
public int rimuovi(int quantita){
	if (aperta)
		return super.rimuovi(quantita);//super.rimuovi() indica il metodo "rimuovi" 
									//nella classe Bottiglia che stiamo estendendo 
	else return 0;
	}
}
/* Controlliamo che lo stato "bottiglia aperta" lascia invariati i
travasi, e che lo stato "bottiglia chiusa" li azzera. */
// BottigliaConTappoDemo.java
public class BottigliaConTappoDemo {
	public static void main(String[] args){
		System.out.println( "Definisco b da 100 litri vuota e la apro");
		BottigliaConTappo b = new BottigliaConTappo(100); b.apri();
		System.out.println(b);
		System.out.println( " b.aperta() = " + b.aperta());
		System.out.println( "Aggiungo 50 litri in b poi chiudo b");
		System.out.println( " b.aggiungi(50) = " + b.aggiungi(50));
		b.chiudi();
		System.out.println( " b.aperta() = " + b.aperta());
		System.out.println( "Chiedo di rimuovere 20 litri da b: zero");
		System.out.println( " b.rimuovi(20) = " + b.rimuovi(20));
		System.out.println( " b.getLivello() = " + b.getLivello());
		System.out.println( "Apro b: ora riesco a togliere 20 litri");
		b.apri();
		System.out.println( " b.aperta() = " + b.aperta());
		System.out.println( " b.rimuovi(20) = " + b.rimuovi(20));
		System.out.println( " b.getLivello() = " + b.getLivello());
	}
}
```

[[Estensioni ripetute di classi]]