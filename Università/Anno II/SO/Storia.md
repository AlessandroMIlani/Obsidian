### anni 50
Il primo SO nasce negli anni 50 -> prodotto da IBM
 - base simile (1 cpi, mem principale), ma non aveva monitor, tastiera ..
 - lavorava a Job ---> venivano caricati ed eseguiti 1 alla volta nelle memoria dell'elaboratore ed eseguito
 	- il successivo viene caricato al completamento del precendete

dati --> **istruzione** --> risultato -> da salvare, richiede *tempo*
|
da trovare nella ram
|
da caricare -> richiede _tempo_

 anni 50 --- J3 -- J2 --J1 --> Elaboratore  **Single Stream** | *Batch Processing* 

**Molti tempi morti durante l'esecuzione**

Ci sono tempi di esecuzione alternati a tempi di attesa
- Carico più job in memoria, così da sfruttare i tempi morti (alterno l'esecuzione di più job)
	- prende il nome di **Interleaving** delle istruzioni 
	- La situazione di alternanza di job predne il nome di **Parallelismo virtuale** ( i vari utenti credono che il proprio job sia eseguito in maniera continua, ma nop)

Per gestire tutta quasta situazione di alternanza, serve un S.O.

1. esecuzione -> CPU Burst
2. I/O -> I/O Burst

### anni 60
Passimo a gli anni 60
 - nascono i primi terminali
 - elaboratori enormi (mainframe) collegato a più terminali (tastiera per input, telescrivente "stampante" per output su carta)
  $-------------------------------$
- Bisogna di aggiungere livelli di astrazione
	- Nasce il concetto di **Time Sharing** 
		- Bisogna distribuire il tempo di carico in modo equo considerando che ci sono persone che aspettano il risultato

- Nasce l'idea di **File**
- nasce l'idea di **directory**

### anni 70
- Nasce l'idea di personal computer
- Si semplificano i SO
	- Vengono rimosse molte features (es. sicurezza, gestione di più utenti in contemporanea ecc...)