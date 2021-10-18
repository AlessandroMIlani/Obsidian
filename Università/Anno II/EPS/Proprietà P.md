# Proprietà della P dedotte dagli assiomi
### Prop.
- Dati A,B e C eventi (= sottoinsiemi di $\Omega$) abbiamo
	1. se $A ⊆ B$ => $P(A) \leq P(B)$  -> monotonia di P
	2. $P(A \cup B)$ = $P(A) + P(B) - P(A \cap B)$
	3. $P(A \cup B) \leq P(A) + P(B)$
	4. $P(A \cup B \cup C)$ =  $P(A) + P(B) + P(C) - P(A \cap B) - P(A \cap C) - P(B \cap C) + P(A \cap B \cap C)$

##### Osservazioni
1. se $A ⊆ B$ => $P(A) \leq P(B)$
	- Stesso significato di monotonia delle funzioni da R in R 
		- Il compreso  ⊆ è una relazione d'ordine paragonabile ad un $\leq$ 
	- Formale:
		-  B  =   $A  \cup (B \cap A^C)$
			$P(B) = P(A  \cup (B \cap A^C))$  -> unisco oggetti disgiunti -> posso usare 		l'additività
			= $P(A)+P(B \cap  A^C$)  -> P è positiva $\geq$ 0
			$P(B) = P(A) + qualcsoa \geq 0$ -> $P(B) \geq P(A)$
		
1. $P(A \cup B)$ = $P(A) + P(B) - P(A \cap B)$
	- P è additiva  $P(A \cup B)$ = $P(A) + P(B)$ se $A \cap B = \emptyset$
		- se  $A \cap B \neq \emptyset$ devo togliere le parti incomune $P(A \cap B)$
		- Formale:

1. $P(A \cup B) \leq P(A) + P(B)$
	- da 2. so che  $P(A \cup B)$ = $P(A) + P(B) - P(A \cap B)$ 
		-  $P(A \cap B) \geq 0$ -> P è positiva  
2. $P(A \cup B \cup C)$ =  $P(A) + P(B) + P(C) - P(A \cap B) - P(A \cap C) - P(B \cap C) + P(A \cap B \cap C)$
	-  ![[Pasted image 20210930114638.png]]

## Probabilità Condizionata
Nota. il $\cdot$ è un segnaposto, si può mettere quasiasi evento
Includere finformazioni parziali 
- ex. lacio un dado a 6 faccie
	- A = "esce il numero 2" = {2} | P(A)= 1/6
	- P(A) sapendo che è uscito un nuemro pari ?
		- B= "è uscito un nuemro pari" = {2,4,6} $\leq \Omega$ P(B) =1/3
	- Come indico P(A) sapendo che è avveuto P(B)?
	  -  $P(\ \cdot\ |\ B\ )$ -> "P dato B"
	  	-  P( A| B )= 1/3 
	  - C = " l'esito è > 2"
	  	- P($\ \cdot\ |\ C)$ nuova situazione
	  		- P( A | C ) = 0  

### DEF
P(A|B) si dice:
-  P di A condizionata a B
- P di A dato B

$P(A|B)=\frac{P(A\cap B)}{P(B)}\ \\  se \ \ \ P(B) \neq 0$

B viene detto evento condizionante, A evento condizionato

- ex precedente. P(A|B)= $\frac{P(A\cap B)}{P(B)} = \frac{1/6}{3/6}= \frac13$

$P(\ \cdot\ |\ B)$ è una misura di probabilità su  $(\Omega,p)$

oss:
 - $\forall\ \ A \leq \Omega\ \ \ \  \ \ \ \ P(A | B)=\frac{P(A\cap B)}{P(B)}$
 - P($\ \ \cdot$|B) : P$(\Omega)$

- Dobbiamo controllare 
1. P(A|B) >= 0
	 -  $P(A|B)=\frac{P(A\cap B)}{P(B)} \geq 0$ 
2. P($\Omega | B$) = 1
 	-  $\frac{P(\Omega \cap B)}{P(B)} = \frac{P(B)}{P(B)}=1$
3. Additività 
   -  Si, credetemi. 


OSS sulle intersezioni: 
	 $P(A|B) = \frac{P(A \cap B)}{P(B)}$
	$P(A \cap B) = P(A|B)P(B)$

### Alcuni risultati alle P condizionante

 Reogla della moltiplicazione
-  $P(A_1 \cap ... \cap A_n) = P(A_n | A_1 \cap ... \cap A_n-1) *  P(A_{n-1} | A_1 \cap ... \cap A_{n-2})* .....* P(A_2|a_1) * P(A_1)$ 

Formula delle probabilià totali:
 - prendi ($A_i)_{i=1}^n$ partizione di $\Omega$
 $B \supseteq \Omega$
$P(B) = \sum_{i=1}^nP(B|Ai)P(Ai) = \sum_{i=1}^nP(B \cap Ai)$
   - Il secondo = è possibile grazie alla definizione di P condizionata
 
  Teorema di bayes
 - $P(A|B) = \frac{P(B|A)*P(A)}{P(B)}$ <- permette di invertire

[[indipendenz coll.event.]]