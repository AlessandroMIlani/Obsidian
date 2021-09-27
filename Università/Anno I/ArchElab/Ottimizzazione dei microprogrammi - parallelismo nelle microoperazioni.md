1. **Condizioni per la parallelizzazione**
	Generalmente, una microoperazioni consta di più elementi eseguiti in parallelo (nello stesso ciclo)
	   -  es: A+B -> A, C+1 -> C

   
   A + B -> A e C +1 -> C sono computazioni completamente indipendenti, nessuna delle 2 dipende dal risultato dell'altra, dunque posso eseguirle contemporaneamente.
    - Ciò è possibile solo se la PO contenga risorse sufficenti, nel nostro caso specifico necessitiamo di 2 differenti reti di calcolo (1 ALU ed 1 incrementatore). &nbsp
    Se forzassimo le 2 op sulla stessa ALU, il parallelismo sarebbe impossibile
	
	![[Pasted image 20210617213656.png]]
	
	Formalmente, l'operazione in parallelo ha luogo durante l'intervallo $T_{\sigma PO}$ del ciclo di clock. 
	Le reti della PO utilizzare per le operazioni elementari eseguite in parallelo si stabilizzano contemporaneamente
	
	Occorre rispettare delle precise condizioni per far si che le stesse computanzioni eseguite in parallelo o sequenzale siano equivalenti.
	- indichiamo con ";" le op in sequenza ed "," quelle in paralleo
	1. &nbsp&nbspA+B->A;C->D &nbsp&nbsp $=$ &nbsp&nbspA+B,C->D
	2. &nbsp&nbspA+B->A;C->A  &nbsp &nbsp$\neq$ &nbsp&nbspA+B->A,C->A (modifica stesso registro)
	3.  &nbsp&nbspA+B->A;B->D &nbsp&nbsp $=$  &nbsp&nbspA+B->A,B->D (permessa uscita in contemporanea, "si ricordi il significato di segnali a livelli")
	4.  &nbsp&nbspA+B->A;B+C->D &nbsp&nbsp $=$ &nbsp&nbspA+B->A;B+C->D (purchè presenti 2 reti di calcolo)
	5.  &nbsp&nbspA+B->A;C->B &nbsp&nbsp$=$ &nbsp&nbspA+B->A;C->B (il riferimento a B rimane stabile per tutto il ciclo di clock)
	6.  &nbsp&nbspA+B->A;A->B &nbsp&nbsp$\neq$ &nbsp&nbspA+B->A,A->B (il valore di A in A->B è il risultato di A+B nel sequenziale, ma non nel paralleno)
	7.  &nbsp&nbspA->TEMP;B->A;TEMP->B &nbsp&nbsp$=$ A->&nbsp&nbspTEMP,B->A,TEMP->B

    Più formalmente, valogono le **Condizioni di Bernstein** per la trasf. da sequenziale a parallela
	- Data la computazione sequenziale:
	&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp $f_1:D_1 \to R_1 ; f_2 D_2 \to R_2$
	- dove $f_i$ sono funz. di dominio $D_i$ e rango $R_i$, la computazione parallela:
	&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp $f_1 : D_1 \to R_1,f_2:D_2\to R_2$
	
	- è equivalente se:
	&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp $R_1 \cap D_2 = Ø$ e $R_1 \cap R_2 = Ø$
	
	
   In un modello *asincrono* di computazione, esente di ipotesi sulla durata temporale delle operazioni e sui loro istanti di inizio, deve valere anche la condizione: &nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp$R_2 \cap D_1 = Ø$
   
   Occorre ribadire che Bernstein serve solo per strasformare una descrizione sequenziale in parallela. 
   È possibile scrivere direttamente in paralleo saltando la descrizione sequenziale.
   
  1. **Parallelismo nelle microoperazioni e nelle condizioni logiche**
  Partendo dalla descrizione sequenziale, o dal microprogramma ad alto livello, 
  possiamo ora semplificare, riordinando le operazioni di trasferimento tra registri, così da:
     1. Da sostituire condizioni logiche di tipo *if then else* con condizioni logiche *case* ; per generalizzare,  sostituire condizioni logiche *case* con altre condizioni logiche *case* con più variabili di condizionamento
	 1. In modo da aumentare il parallelismo di micooperazioni
	 
	 Entrambe le tecniche devono rispettare le condizioni di Bernstein per i microprogrammi.
	 es tecnica 2: &nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspA+B->A; **if** $M_0$ = 0 **then** C+1->C **else** C-1->C
	 
	 Può essere adattata in:
	 &nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspi. ($M_0$ = 0)A+B->A, C+1->C,i+1;($M_0$=1)A+B->A,C-1->C,i+1
	 