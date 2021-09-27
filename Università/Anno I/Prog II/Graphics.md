Java contiene la classe **Graphics** per gli oggetti grafici (aree rettangolari in cui si può disegnar con dei metodi)
Per Disegnare, è necessario sfruttare l'ereditarietà delle classi
[[Ereditarierà]]

1. definiamo una classe *Figura* di figure, ognuna con metodo *draw(Graphics g)* che disegna in un oggetto grafico g.  
<ins> Draw è vuoto per la figura generica </ins> e verrà di-definito in ogni sottoclasse
1. Da *Figura* definiamo la classe *Disegno* delle finestre (obj della classe *Jframe*) con un array di figure.
Forniamo un metodo *void Paint(Graphics g)* che prende l'oggetto grafico e ne disegna le figure usando *draw*
1. Alla fine richiamiamo da libreria *setVisible(true)* che fornisce l'oggetto g a paint e genera il disegno.
**non possiamo definire g** perchè in costruttore della classe Graphics è *protected*
```java
// Figura.java
import java.awt.*; //Abstract Window Toolkit (finestre grafiche)
import javax.swing.*; //estensione di awt per interfacce grafiche
public class Figura{
// Dichiariamo il metodo di disegno draw ma lo definiamo vuoto:
// serve solo per ricordarci di definire un metodo draw in ogni
// sottoclasse della classe Figura.
	public void draw(Graphics g){ /* vuoto */ }
}
```

Per la sottoclasse “Quadrato” di “Figura”, il metodo draw disegna in g un quadrato di lato dato, orizzontale e centrato con gli assi. Usiamo i metodi della classe Graphics: setColor, drawLine, drawOval.

```java
// Quadrato.java quadrato=una possibile forma di una Figura
// Definiamo Quadrato come una sottoclasse di Figura
import java.awt.*; //Abstract Window Toolkit
import javax.swing.*; //estensione di awt per interfacce grafiche

public class Quadrato extends Figura {
//Un quadrato e' definito dal suo lato
	private int lato;
// COSTRUTTORE di un quadrato
	public Quadrato(int lato){ this.lato = lato; }
// OVERRIDE: RI-definiamo il metodo draw (per ora vuoto)
// per disegnare una figura nel caso di un quadrato.
// Scegliamo il quadrato centrato nell'origine e orizzontale.
// Scegliamo il colore arancio per le prossime linee in g.
	public void draw(Graphics g) {
		g.setColor(Color.orange);
		int m = lato / 2;
		g.drawLine( m, m, -m, m); //disegno primo lato in g
		g.drawLine(-m, m, -m, -m); //disegno secondo lato in g
		g.drawLine(-m, -m, m, -m); //disegno terzo lato in g
		g.drawLine( m, -m, m, m); //disegno quarto lato in g
	}
}
```
Per la sottoclasse “Cerchio” di “Figura”, il metodo draw disegna un cerchio di raggio dato e centrato con gli assi.

```java
// Cerchio.java cerchio = una possibile forma di una Figura:
// definiamo Cerchio come una sotto-classe di Figura.
import java.awt.*; //Abstract Window Toolkit
import javax.swing.*; //estensione di awt per interfacce grafiche
public class Cerchio extends Figura{
//Un cerchio e' definito dal suo raggio r
	private int raggio;
// COSTRUTTORE di un quadrato
	public Cerchio(int raggio){ this.raggio = raggio; }
//OVERRIDE: RI-definiamo il metodo draw per disegnare una figura
//in un oggetto grafico g, nel caso la figura sia un cerchio.
//Disegnamo il cerchio nel rettangolo di angolo in basso a sinistra
//(-r, -r) e di dimensioni 2r x 2r.
//Scegliamo il colore rosso per le prossime linee in g
	public void draw(Graphics g) {
		g.setColor(Color.red);
		g.drawOval(-raggio,-raggio, 2*raggio,2*raggio);
	}
}
```
```java
//Disegno.java
import java.awt.*; //Abstract Window Toolkit (finestre grafiche)
import javax.swing.*; //estensione di awt per interfacce grafiche
public class Disegno extends JFrame{ /* Un "disegno" e' un JFrame con
parte grafica = tutte le figure di un array di figure */
	private Figura[] figure;
//COSTRUTTORE basato sul costruttore della classe superiore JFrame
	public Disegno(Figura[] figure){
		super(); //Assegnamo tutti i parametri di un JFrame
		this.figure = figure; //Aggiungiamo un array di figure
}
// OVERRIDE: ridefiniamo il metodo paint di JFrame
// chiedendo di inizializzare una finestra grafica, poi
// di disegnare tutte le figure dell’array figure di g
	public void paint(Graphics g) { //INIZIALIZZO g
		int w = getSize().width; // base di g
		int h = getSize().height; // altezza di g
		g.clearRect(0, 0, w, h); // azzero il contenuto di g
		g.translate(w/2,h/2); //traslo sistema di riferimento al centro di g
//DISEGNO tutte le figure dell’array figure
		for(int i=0;i<figure.length;++i) figure[i].draw(g);
	}
//BINDING per il metodo draw. Quale metodo draw viene scelto? //Dipende dal tipo esatto di figura[i]. Se figura[i] ha tipo esatto
//Quadrato, allora viene scelto il metodo draw per i quadrati e non
//il metodo draw per le figure (che sarebbe un metodo vuoto)
	public static void main(String[] args){
		int m=70,n=90; Figura[] figure = new Figura[n];
//Array di n figure: all’inizio ogni figura vale null
//Assegnamo le n figure: scegliamo m quadrati e (n-m) cerchi
//Possiamo farlo perche' quadrati e cerchi sono particolari figure
		for(int i = 0; i<m; i++) figure[i] = new Quadrato(i*7);
		for(int i = m; i<n; i++) figure[i] = new Cerchio(i*3);
//Definiamo un disegno con array di figure proprio “figure"
		Disegno frame = new Disegno(figure);//Jframe con array di figure
//ESEMPI DI EREDITARIETA' (SENZA OVERRIDE) DALLA CLASSE JFRAME
//Scegliamo di terminare la figura quando ne chiudiamo la finestra
//(il metodo setDefaultCloseOperation viene ereditato da JFrame)
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
//Scegliamo la dimensione della finestra grafica:
//(il metodo setSize viene ereditato da JFrame)
		frame.setSize(600,600);
// setVisible(true) rende il disegno visibile, inviando un oggetto
// il metodo paint all’oggetto frame insieme con un parametro g:
//(il metodo setVisible viene ereditato da JFrame)
		frame.setVisible(true);
	}
}

```
![[Pasted image 20210426150820.png]] ![[Pasted image 20210426150853.png]]

[[Classi astratte di figure]]