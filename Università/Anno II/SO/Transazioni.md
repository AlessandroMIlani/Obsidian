## Transazioni
**Introduzione**
- CC-cliente = 100
- CC-venditore = 1000

Transazione
- CC-cliente = 50
- CC-venditore = 1050

Che succede le la transizione si interrompe a metà? (tolgo 50 al cliente, ma il venditore rimane a 1000)?
- Il sistema rimane in uno stato inconsistente
	- Bisogna riportare il tutto ad uno stato consistente precedente (riportare CC-cliente = 100)
	- quanto si completano tutti i passi, si dice che si esegue un "*commit*", se qualcosa va storto e si torna indietro, si fa un "*abort*"

**Memorie Volatili**
- Si può utilizzare un logfile $\in$ filesystem (rimane in una memoria persistente)
	- Serve un formalismo da usare nel log "<T, start> / <write, var, prec, new> .... <T, end>"
	- Nel caso perda i dati nella memoria volatile, recupero il log e verifico le transazioni.
		- Per quelle con start e end, sono a posto e concluse
		-   Per quelle con start ma non end, posso esseguirene il rollback 
	- Ogni tot. ci possono essere dei checkpoint (tutto il precedente è ok, quinid posso non leggerlo)
	- Scrivendo in memoria secondaria, più lenta, vado a rallentare l'esecuzione   

#### Transizioni su variabili condivise
> per comodità riduciamo tuttle le istruzioni a solo quelle di Read / Write

Se voglio sfuttare una variabile condivisa, senza l'uso dei semafori, mi ritrovo ad avere delle transazioni atomiche(solo R/W) concorrenti (quindi con interleaving)

- ES. T1 e T2 volgiono accedere alla var A
	- Si alternano con le R/W... ma come sapppiamo se A rimane consistente
	- Imponiamo la condizione che il risultato della loro esecuzione alternata, corrisponda  al risultato di *eseguire prima tutta una T e poi l'altra*(\*)
		- (*)**Sequenzalizzazione delle istruzione** 

Partendo da A=3 e B=5:

| T1       | T2       |
| -------- | -------- |
| Read(A)  | Read(A)  |
| Write(A) //A+2 | Write(A) //A+2 |
| Read(B)  | Read(B)  |
| Write(B) //B+3 |Write(B) //B+3  |

Se seguo in ordine T1 e T2, ottendo => A=7 e B=11

Una loro esecuzione con interliving può essere:

| T1       | T2       |
| -------- | -------- |
| Read(A)  |          |
| Write(A) |          |
|          | Read(A)  |
| Read(B)  |          |
|          | Write(A) |
| Write(B) |          |
|          | Read(B)  |
|          | Write(B) |

> Non in tutti i casi, l'esecuzione con interleaving porta ad una soluzione accettabile (rimando a T1 e T2, se seguo subito entrame le read(A) e poi le write(A), mi ritorvo con A=5 e non A=7)

### Protocolli di esecuzione

L'obbiettivo è manenere consistenti i dati durante l'esecuzione di operazioni conflittuali

Delle operazioni, per essere definite conflittuali, devono:
1. Appartenere a procesi divesi
2. usare la stessa variabile condivisa
3. almeno una esegue un Write

#### Protocollo TimeStamp
Qunado viene reato il processo T, gli si assegna un TimeStamp (marcatura temporale), indicata con TS(Tx)
- L'esecuzione con interleaving deve garantire un risultato uguale a quello che si otterrebbe eseguendo i processi per ordine crescente di timestamp

Nomenclatura:
- D = dato condiviso
- R(D): esecuzione delle read, deve avere un TS più alto di una trans. che ha letto
- W(D): esecuzione della write, deve avere un timestamp più altro di una trans. che ha scritto

**Protocollo**
1. T esegue *Read(D)*
	- 1.a TS(T)< W(D) -> T abort, bisogna disfare i passi di T già eseguiti
	- 1.b Altrimenti, si esegue la lettua -> si aggiornano i TS, R(D) = MAX(R(D),TS(T))

1. T esegue *Write(D)*:
    - 2.a TS(T) < R(D) -> T Abort
	- 2.b TS(T) < W(D) -> T Abort
	- 2.c write consensita  -> aggiorno TimeStamp W(D) = TS(T)

- Tutto ciò appesantisce l'esecuzione, ma conpensa la mancanza di meccanismi di mutua esclusione
- Le T abortite vengono riavviate con un TS(T) nuovo, più alto

### Protocollo a 2 fasi -> Lock
1. fase di aquisizione del lock (fase di crescita)
2. utilizzo dato
3. fase di rilascio dle lock (fase di decresita)

Protocollo che porta spesso al DeadLock

## Dedlock
Può avvenire solo qunado ci sono in gioco risorse ondivise in mutua esclusione.

ES:
Cuochi/Processi -> C1 C2 C3
Risorse condivise -> Olio 1 / aceto 1 / sale 1

C1 prende sale->olio->aceto / C2 prende olio->aceto->sale / C3 prende aceto->sale->olio
- Se devono prendere 1 risorsa alla volta, tutto funziona.
- Se servono tutte le risorse insieme, si bloccano perchè ognuno deve rpendere una risorsa in possesso di qualcun altro -> **DeadLock**

** Condizioni necessarie al Deadlock**
1. mutua esclusione
2. Possesso e attesa
1. Attesa Circolare
2. Assenza di prelazione

Non si verifica a tutte le esecuzioni. Il codice è corretto, ma poi dipende dalla sincronizzazione dei processi durante la singola esecuzione

[[Rilevare DeadLock]]