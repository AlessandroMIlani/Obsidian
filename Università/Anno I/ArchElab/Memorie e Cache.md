# Memoria Principale
la **memoria** è quella parte del calcolatore in cui sono depositati i programmi e dati

- ## Bit
E' l'unità base della memoria; può avere valore 1 / 0 

- ## Inidirizzi di memoria
  - Sono costruite da un certo numero di **celle**, ciascuna delle quali può memorizzare informazioni
  - Ogni cella ha un **indirizzo** utile al programma per riferirsi ad una cella specifica
  Per ogni *n* celle, gli indirizzi vanno da 0 a *n-1* 
  - Tutte le celle contengono lo stesso numero di Bit. -> Se sono costituite da *k* bit, può contenere $2^k$ combinazioni di bit.
  - I calolatori che sfruttano un sistema di numerico binario, se hanno indirizzi da *m* bit, posso avere al massimo $2^m$ celle indirizzabili
  - Il numero di bit nell'indirizzo (che determina il max n. di celle) è indipendente dal numero di bit per cella.
       - sia una memoria con $2^{12}$ celle da 8bit che una con $2^{12}$ celle da 64bit richiedono indirizzi da 12 bit
      
	 
  - Generalmente si sfruttano celle a 8 bit dette **Byte**, raggruppate in **Word**, che possono essere da 4 Byte (32 bit) o 8 Byte (64 bit)
      - Le parole sono inportanti, in quanto le istruzioni generalmente operano su intere parole (una macchina a 32 bit avrà registri a 32bit per manipolare parole da 32bit --> stesso discorso per le 64bit)
 - ## Ordinamento dei Byte | Endianness
	 - I Byte posso essere numerati da Sx a Dx oppure da Dx a Sx

Big-endian           

| 0 | 1 | 2 | 3 |        
|---|---|---|---|    
| 4 | 5 | 6 | 7 |        
| 8 | 9 | 10| 11|
| 12| 13| 14| 15|
<-->Byte
<---------->  Parola 32 Bit

Little-endian           

| 3 | 2 | 1 | 0 |         
|---|---|---|---|    
| 7 | 6 | 5 | 4 |        
| 11 | 10 | 9| 8|
| 15 | 14 |13|12|
 - Esempio: il numero 6 è rappresentanto in entrambi i casi con i bit 110 nei 3 bit più a destra (meno significativi) e 0 negli altri 29.
 Nel Big-endian i bit 110 si troveranno nel byte 3/7/11/15, mentre nel little-endian nel byte 0/4/8/12
 - Memorizzando tipi diversi dagli interi (char, String ...) i sistemi rimangono coerenti internamente ma si creano problemi di comunicazione se le macchine non sfruttano lo steso tipo di memorizzazione
	 - non essite un metodo unico di conversione, quinidi si è costretti a sfruttare un "intestazione" per inidicare il tipo del dato e quindi procedere con la corretta conversione --> grande scomodità
- ## Memoria Cache
  - Le CPU sono sempre state più veloci delle memorie
	Cio crea uno squilibrio che porta la cpu a dover aspettare molti cicli prima di ricevere una parola creando uno "stallo software" dopo ogni LOAD (rifacendosi alla IJVM) da riempire con istruzioni fasulle dette NOP

     - Per tamponare questo problema si abbina una memoria più spaziosa e lenta ad una piccola ma molto veloce (posizionata nel processore) detta **Cache**
     - L'idea di base e memorizzare le parole più utilizzate nella Cache così che la Cpu necessiti di effettuare meno chiamate verso la memoria lenta.
     Ciò riduce nettamente il tempo medio di lettura di una parola.
	     - L'efficenza dipedende dalla capacità di salvare nella cache le parole necessarie prima che vengano richieste dalla cpu
	     - Per fare ciò, ci si rifà al **Principio di Località** cioè l'osservazione secondo cui le chiamate fatte in un ristretto intervallo di tempo tendono a rifarsi ad una piccola frazzione della memoria totale.
	     - Generalmente nel momento in cui una parola viene referenziata, viene copiata nella cache insieme ad alcune delle parole nelle vicinanze. 
	        - Così se la parola $X$ serve $k$ volte verrà letta 1 sola volta lentamente, ed altre k-1 volte velocemente
	      
		  - *Tempo di accesso medio* = $c + (1-h)m$
		      - Se $h \to 1$, tutte le richieste sono soddisfatte dalla cache.
		      Se $h \to 0$, bisogna rifarsi ogni volta alla emoria più lenta
			  - $c$ è il tempo necessario per controllare inizialmente la cache
			  - $m$ tempo per fare riferimento alla memoria
	     
	   - Sia Cache che memoria centrale sono divise in blocchi di dimensioni fisse, così da sfruttare al meglio il Principio di località -> se la lettura della cache va a vuoto, si riscrive l'intero blocco
	     - all'interno della Cache prendono il nome di **Linee di Cache**  
	 
	 - I problemi principali nello sviluppo delle cache sono:
	   - Costi crescenti con le dimensioni
	   - Dimensioni delle linee
	   - Tener traccia di cosa si memorizza e dove
	   - Decidere se tenere dati e istruzioni salvati in una solo cache o più
	   	- Sfruttando una **Cache unificata** si semplifica il tutto, ma ad oggi tutte le cpu sfruttano **Cache specializzate** in una struttura chiamata **Architettura Harvard**
