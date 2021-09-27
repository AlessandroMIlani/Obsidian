## Incremento Velocità
Per incrementare la velocità del MIC1 ci sono vari approcci:
 - *Ridurre numero di cicli di clock* necessari per l'esecuzione delle istruzioni 
 - *Semplificare l'organizzazione* cicli più brevi
 - *Sovrapporre l'esecuzione* delle istruzioni
 
 (Tenere sempre presente l'equilibrio tra costo e beneficio)
 
 ### Riduzione del numero di microistruzioni
 - Fusione del ciclo di esecuzione dell'interprete (goto Main1) con il microcodice
 - introduzione terzo bus
 - introduzione unità per il fetch delle sitruzioni

**Fusione cicli di esecuzione**: ![[Pasted image 20210603144436.png]]

**Architettura a 3 bus**

Con un bus che va a collegare tutti i registri all'ingresso sinistro dell'ALU, si evitano tutte le scritture extra su H

**Istruction Fetch Unit**
- Per istruzione:
  - il PC viene passato attraverso l'ALU e incrementato
  - Il PC viene usato per leggere il byte seguente nel programma
  - gli operandi vengono letti in memoria
  - l'ALU esegue il calcolo e i risultati vengono memorizzati
 -    La lettura e la decodifica dei campi delle istruzioni è un operazione comune a tutte le istruzioni
 -    Per sgravare l'ALU da parte del carico, si può creare un unità indipendente per il fetch delle istruzioni (detta IFU -> *Instruction Fetch Unit*)
 -    l'IFU può incrementare il PC indipendentemente, e leggere byte dal flusso dei byte di programma prima che siano necessari
 -    Preferibile ad una $2^a$ ALU (più semplice come struttura)
 -    