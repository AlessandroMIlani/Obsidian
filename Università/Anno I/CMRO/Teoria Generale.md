## TEOREMA FONDAMENTALE
Il teorema fondamentale della programmazione lineare afferma che: 
- Il massimo ed il minimo di una funzione lineare di un numero qualsiasi di variabili soggetta a vincoli espressi da equazioni e/o da disequazioni lineari, se esistono, si trovano sul contorno o sui vertici della regione ammissibile, e non al suo interno. 
- Un sistema lineare ha soluzioni infinite quando si ha lo stesso valore della funzione obiettivo su due vertici, mentre ha un' unica soluzione ottima quando si trova solo su uno dei vertici. 
## RETTA DI ISOPROFITTO 
Data una regione ammissibile illimitata, per verificare se questa ha soluzioni ottime, bisogna usare il metodo delle retta di isoprofitto ovvero si mette la funzione obbiettivo uguale ad una costante K e bisogna tracciare la retta dando dei volori a x1 e x2, sostituendoli successivamente nella funzione obiettivo ugualizzata a K. Per vedere la direzione in cui i valori di questa retta crescono bisogna tracciare un vettore con le coordinate date dai coefficienti della funzione obiettivo. 
## INDIPENDENZA LINEARE 
Dato un insieme di $k > 0$ vettori $S = {v1, v2, . . . , vk} ⊆ Rn$, si dice che un vettore w è una combinazione lineare dei vettori di S se esistono k coefficienti $x1, x2, . . . , xk ∈ R$ per cui risulta $w = x1v1 + x2v2 + · · · + xkvk$ . I vettori di un insieme $S = {v1, . . . , vk} ⊆ Rn$ (con k > 0) sono detti tra loro linearmente indipendenti se, data la loro sommatoria questa è uguale a 0. In questo caso l’insieme S è anche chiamato un insieme libero. 
## INSIEME LIBERO 
Un insieme è libero se: 
- Se S e un insieme libero, allora 0 non appartiene a S; 
-  Se S e un insieme libero e S′ è un sottinsieme di S e S′ non è vuoto, allora S′ è un insieme libero; 
-   Se S1, S2 sono insiemi liberi e S1 ∩ S2 non è vuota questo è un insieme libero.

## GAUSS JORDAN 
 - Ammette infinite soluzioni quando non abbiamo più un elemento di pivot prima che questo termini e ciò comporta che oltre alla matrice ridotta abbiamo delle altre variabili libere che sono diverse da 0 (ex pillole. la terza riga tutta nulla); 
 -  Il sistema non ammette soluzioni quando, per esempio, data una riga composta da soli zero, il valore (nella stessa riga) nella colonna dei termini noti è diverso da zero stesso; 
 -   Il sistema ammette un unica soluzione quando, avendo tutte le colonne ridotte, abbiamo un' unica variabile x con valore >= 0. 
 ## VERTICE ZONA AMMISSIBILE 
 Per qualunque punto della zona ammissibile, x è un vertice se e solo se, prese le colonne della matrice A, queste sono linearmente indipendenti. 
##  TEOREMA DI FARKAS (1920) 
 Dati $A ∈ Rp×q, b ∈ Rp$, esattamente una delle seguenti condizioni è soddisfatta. 
 - esiste $x = (x1, . . . , xq)T ∈ Rq+$ tale che $Ax = b;$ 
 - esiste $v = (v1, . . . , vp)T ∈ Rp$ tale che $vTA ≥ 0$ e $vTb < 0$.
 
 Il Lemma di Farkas assicura che quando un tale sistema è privo di soluzioni esistono sempre gli opportuni coefficienti con cui combinare le equazioni in modo da ottenerne una assurda. 
 ## CRITERIO DI ILLIMITATEZZA 
 Il criterio di illimitatezza è soddisfatto quando tutti i coefficenti della x che deve entrare in base sono negativi. 
 ## CRITERIO DI OTTIMALITA' 
 Tutti i coefficenti della funzione obbiettivo sono negativi e quando ciò accade il simplesso si arresta. Se facciamo entrare una variabile fuori base con valore negativo la soluzione decresce. 
 Data una base ammissibile B della matrice A del problema, se il vettore dei costi ridotti è non negativo allora la soluzione della base ammissibile associata alla base B è ottima per il problema. 
 ## POLIEDRO E POLITOPO 
 La regione ammissibile di un programma lineare è in generale l’intersezione di un numero finito di semispazi e iperpiani. 
 E' chiamato poliedro convesso la regione ammissibile che è illimitata (e quindi S∗ = ∅); se inoltre il poliedro è limitato viene anche chiamato politopo.