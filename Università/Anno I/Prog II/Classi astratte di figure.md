Definiamo delle classi per calcolare area e perimetro delle figure geometriche.
- **Primo esempio di soluzione**
     - scriviamo un metodo statico per figura; ciò impedisce di crearne un array perchè non hanno tipi in comune.
     - Dobbiamo creare un calsse Figura avente le relative sottoclassi e che non contenga oggetti (oltre quelli delle sottoclassi)
     -  Non esistendo metodi univoci, dobbiamo crearne di vuoti e sovrasscriverli per ogni classe

- **Soluzione migliorata**
   - Dichiariamo una classe  ed alcuni suoi metodi come astratti
   - I metodi astratti fanno da segnaposto per quelli delle sottoclassi e non si possono usare
   - L'unico oggetto che apprartiene ad una classe astratta è **null**
   - Il vantagggio è che java controlla che il metodo astratto sia statto sovrascritto dalle sottoclassi, e che non siano dichiarati oggetti nella classe astratta
 
 - **Regole classi astratte**
     - Gli attributi sono astratti
     - Un metodo astratto può essere solo in una classe atratta, mentre la classe astratta può avere metodi concreti
     - una classe astratta non definiscre costruttori
     - per non essere a sua volta astratta, la sottoclasse deve sovrascrivere tutti i metodi astratti ereditati
   
   ![[Pasted image 20210502182631.png]]
 ```java
/** LA CLASSE ASTRATTA FIGURA */
public abstract class Figura {
	public abstract double area();
	public abstract double perimetro();
	public static void main(String[] args){
		Figura P; 
	}
}
```

```java
// Cerchio.java Sottoclasse non astratta di Figura:
public class Cerchio extends Figura{
	private double raggio;
	public Cerchio(double raggio){
		assert raggio >= 0; this.raggio = raggio;}
	public double getRaggio(){return raggio;}
	public void setRaggio(double raggio)
		{assert raggio >= 0; this.raggio = raggio;}
	public double area(){
		return Math.PI * raggio * raggio;}
	public double perimetro(){return 2 * Math.PI * raggio;}
}
```