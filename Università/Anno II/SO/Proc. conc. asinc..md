## Processi concorrenti Asincroni
 Abbiamo un Buffer (array condiviso in Ram) con capienza D, variabile free (indice cella vuota)

- Ipotiziamo 2 processi (P1 e P2) che volgiono sfruttare il buffer
	- P1 esegue la sua istruzione e salva nella cella indicata da free
	- P2 esegue e sovvrascrive la cella di free (perchè P1 non ha fatto in tempo ad aggiornare free a free+1) 
	- P1 aggiorna free lasciando una cella corrotta
	- P2 aggiorna free, lasciando free+1 vuota (ma pesnado che sia piena)
	- Bisongna eseguire tutti e 2 i passaggi (calcolo + aggiornamento free) senza che il processo in questione venga interrotto
```
1) buffer[free]= dato;        <-- Sezione critica
2) free = (free +1) % D;	  <-- //        //
```
Una sezione critica è una sezione di codice che vine eeseguita con variabili condivise
 - L'obbittivo è che le sezioni critiche che operano sulle stesse variabili Devono eseguire con mutua esclusione

PROGRAMMA: 
```
Codcie non cirtico;
Inizio SC;
<S.C.>;
FIne SC;
Codice non critico;
```
 - Inizio SC -> dichiara l'utilizzio della variabile condivisa ("prende le chiavi e si chiude dietro la porta")
 - Fine SC -> lascia la variabile ad altri programmi

#### Buone proprietà soluzioni al prob. della SC
1) mutua esclusione
2) Progresso
	- Un processo che non deve usare una variabile condivisa, non deve impedire ad altri di usarla
1) Attesa Limitata
	- Non ci deve essere Starvation

##### Soluzioni SW ed HW
[[Soluzioni SW]]
[[Soluzioni HW]]

## Semaforo
Consentono qualsiasi tipo di sincronizzazione tra processi
Si basa su 2 operazioni:
- P (Proberen = verificare)
- V (Verhoren = incrementare)
##### Tipologie di semafori
- **Semafori Mutua Esclusione** - inizializzato a 1
- **Semafori Contatori** - inizializzato a n. | n. = numero risorse libere


### Implementazione
Semaforo S = variabile intera condivisa
- pseudocodice
```C
P(s){
	while(s <= 0) no_op;
	S=s-1;
}

V(s){
	s = s+1;
}
```

*Accesso in mutua esclusione*
- inizializzo il semaforo Mutex = 1
- P che deve eseguire S.C. paretesizza la sc:
pseudocodice
```C
P(s)
	<S.C.>
V(s)
```
- P decrementa mutex e poi V lo incrementa

Non presenta un attesa attiva
Oltre il valore del semaforo, ci sono molte altre informazioni ( principalmetne una coda d'attesa)
- Implementazione un po' più realistica (ma sempre pseudocodice)
```C
P(s){
	S -> valore--;
	if(s-> valore < 0)
		block();  <- sys call per cambiare stato
}
```
S può raggiungre valori negativi lontani da 0
- Se ne prendo il valore assoutlo, posso sapere quanti processi sono in attesa
```C
V(S){
	S->valore++;
	if(s->vlaore<0)
		wakeup;  <- sys call
}
```
Se S incrementa da -2 a -1, si accorge che c'è qualche processo in coda, e lo risveglia

#### Semafori Contatori
1. Ho un buffer da 6 "slot"
1. inizializzo S a 6
2. ad ogni Processo che entra in coda, sottraggo 1 ad S

### Attesa dello 0
"si usa il semaforo al contrario"
- Z(s) parte quando s è = 0
	- es. S=n con c. = nuemro rpocessi
	- Z parte quando tutti i processi n sono finiti 
