## Introduzione

### A cosa servono i compilatori
 anni 40/50, programmazione senza compilatori 
- Utilizzo del linguaggio macchina (basso livello)
	- programmazione difficile e noisia 

Programmazione con compilatori
- utilizzo linguaggio a più alto livello
	- programmazione più facile e "divertente"
	- il compilatore pensa alla traduzione in linguaggio macchina così da renderlo eseguibile dalla macchina 
		- il processo non è banale e bisogna "insegnare" tutto al compilatore

## Fasi di un compilatore

1) Analisi lessicale
2) Analisi sintattica
3) analisi semantica
4) Generazione del condice intermedio
5) Ottimizzazione -- non studiato
6) Generazione dle codice oggetto -- non studiato


## Alfabeti
Un alfabeto è un insieme finito e non vuoto di simboli

- usiamo $\sum$ per indicare un alfabeto generico
- usaimo $a,b,c ...$ per indicare simboli generici di un alfabeto

#### Esempi
- $\sum_1 = \{0,1\}$ alfabato cifre decimali
- $\sum_2 = \{\_,., *,'\}$ alfabeto di siboli punteggiatura

## Stringhe
una **Stringa** su un alfabeto $\sum$ è una sequenza finita di simboli in $\sum$

- usaimo $u,v,w...$ per indicare stringhe generiche
- usami $\epsilon$ per indicare una stringa vuota, composta da zero simboli

### Operazioni sulle stringhe
La **lunghezza** di una stringa $u$ e' il numero di simboli di cui e' costituita e si indica con $|u|$ .

La **concatenazione** di $u$ e $v$ e' indicata con $uv$, attacando la sequenza di $u$ dopo la sequenza di $v$. 

La **lunghezza** della concatenzione sara' uguale alla somma della lunghezza delle sue stringhe.

Un **suffiso** di una stringa se la concatenazione di essa con un'altra stringa e' uguale ad un'altra.

L'**inverso** ($w^{R}$)di una stringa e' una stringa che ne constiene gli stessi suffissi ma in ordine inverso.

Una stringa e' **palindroma** se una stringa e' uguale al suo inverso ($w=w^{R}$)

La **potenza** di una stringa ($u^{n}$)e' la stringa che otteniamo concatenando la stessa $n$ volte.

## Linguaggio
Un linguaggio L su un alfabeto $\epsilon$ su un alfabeto $\sum$ è un qualunque insieme di stringhe su $\sum$

- usaimo $\sum^*$ per indicare l'ineme di tutte le stringhe su $\sum$, inclusa quella vuota
- usamo $\sum^+$ per indicare l'insime di tutte le stringhe non vuote su $\sum$

### Linguaggi particolati
- $L = \emptyset$ = linguaggio vuoto
- $L = \{\epsilon\}$ = linguaggio composto dalla stringa vuota
- $L=\sum$ = linguaggio costituito dai simboli dell'alfatebo
- $L = \sum^n=\{w | w \in \sum^* \wedge \ |w| = n\}$ = è l'insieme delle stringhe lunghe $n$

## Operazioni sui linguaggi
| Operazione | Definizone |
|---|---|
|Unione| $L_1 \cup L_2$ |
|Intersezione|$L_1 \cap L_2$|
|Completamento (rispetto a $\sum$)|$L\ = \sum^*-L$|
|Concatazione|$L_1L_2=\{uv \| u \in L_1 \in L_2\}$|
|Potenza|$L^0=\{\emptyset\} \ \ \ L^{n+1}=LL^n$|
|Chiusura di Kleene|$L^*=L^0 \cup L^1 \cup L^2 ... = \cup_{i \in N}L^i$|
|Chiusura Transitiva|$L^+=L^1 \cup L^2 ... = \cup_{i \in N - \{0\}}L^i$|


### Esercizi
- dimostrare oerchè le relazioni non sono valide:
	1. $L \emptyset = \emptyset L = L$  -> Il risultato giusto è $\emptyset$ (linguaggio vuoto)
		 - la si può considerare come una moltiplicazione per 0
	2. $L\{\epsilon\}=\{\epsilon\}L=\{\epsilon\}$ -> il risulato giusto è L
		-  aggiungere una striga vuota non influneza
	3.  $L_1L_2=L_2L_1$ -> Falso la concatenazoine considera la posizione, non è commutativa
	4.  $L^+=L^*-\{\epsilon\}$ -> Falso se L contiene la stringa vuota 


[[DFA]]