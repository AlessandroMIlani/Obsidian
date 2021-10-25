## Soluzioni SW
 Abbiamo Pi e Pj
 Soluzione 1) 
```
<Sezione non critica>
while(turno != i) do no_op;  <-- sezione d'ingresso
<Sezione critica>
turno = j;                   <-- sezione d'uscita

```
- La variabile turno sereve per decidere chi deve struttare la variabile condivisa:
   -  Può avere solo valori i/j (in questo caso) ed è inizializzata a caso
 -   L'attuale sezione d'ingresso fa eseguire un operazione vuota a P, fichè il la condizione non è falsa (quindi fich'è non è il suo turno)
 		- è detta Attesa Attiva / Busy Waiting -> non una buona idea, perchè fa lavorare la cpu mentre aaspetta   

Ipotiziamo che Pi produre 10 dati mentre Pj 3, dopo che si sono alternati 3 volte, Pi porta turno  a j, ma dato che j è andato avanti non lo riporterà più a i.
 - Quindi Pj blocca Pi, violando la propietà di progresso

Soluzione 2)
```
flag[i]=true;
while(flag[j]) do no_op;	<-- sezione d'ingresso
<S.C.>
Fleg[i]=false;				<-- sezione d'uscita
```

- implode tutto, perchè già dopo l'esecuzione della prima istruzione si bloccano.
	- impostano entrambi il soro flag a true, ma finch'è l'atro flag è a true non possono andare avanti... 


Soluzione 3 - Algortmo di Peterson)
```
1)flag[i]=true;
2)turno = j;
3)while(flag[j] && turno == j) do no_op; <-- sezione d'ingresso da 1 a 3
<S.C.>
Fleg[i]=false;				<-- sezione d'uscita
```

Fonde i 2 metodi precendenti per risolverne i problemi

![[Pasted image 20211015175040 1.png]]

[[Proc. conc. asinc.]]