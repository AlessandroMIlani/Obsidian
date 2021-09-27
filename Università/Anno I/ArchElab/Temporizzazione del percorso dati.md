La seguente figura mostra la temporizzazione degli eventi sul percorso dati:

**![[Pasted image 20210618160850.png]]**
1. all'inizio di ogni ciclo viene generato un breve inpulso che può essere determinato dal clock principale
2. sul fronte di discesa vengono impostati i bit che piloteranno tutte le porte logiche
   - quest'operazione richiede un intervallo di tempo definito: $\Delta w$
3.   Il registro richiesto viene selezionato e portato sul bus B.
      - Il valore si stabilizza in un tempo: $\Delta x$
4. La ALU e lo shifter cominciano ad operare sui dati validi.
      - l'output si stabilizza in un tempo: $\Delta y$
4. Passa un tempo $\Delta z$ ed i risultati vengono prorogati sul bus C  e vengono caricati nei registri durante il fronte di risalita
   - Anche se modifico dei registri di input, gli effetti delle modifiche giungeranno al bus C dopo un tempo sufficientemente lungo rispetto a quando sono stati caricati i registri
   - Sul fronte di salita non viene più alimentato il bus B, in preparazione al ciclo successivo

Ricordarsi che esiste un tempo di propagazione finito: una modifica sul bus B, intaccherà il bus C solo dopo un intervallo finito.
 - Per far si che ciò funzioni serve una rigida temporizzazione, un lungo ciclo di clock, un ritardo del'ALU conosciuto ed un rapido caricamento dei registri dal bus C

Un modo diverso per vedere il ciclo è la sua divisione in sottocicli **definiti implicitamente** e che l'inizio del sottociclo 1 sia guidato dal fronte di discesa del clock:
1. Si impostano i segnali di controllo ($\Delta w$)
2. I registri vengono caricati nel bus B ($\Delta x$)
3. La ALU e lo shifter svolgono le loro operazini ($\Delta y$)
4. I risultati vengono prorogati lungo il bus C e ritornano nei registri ($\Delta z$)

Con Definiti Implicitamente si intende che: nessun segnale comunica all'ALU quando funzionare, nè dice ai risultati quando entrare nel bus C.
ALU e shifter funzionano continuamente, ma i loro input sono da considerare inconsistenti fino al tempo $\Delta w + \Delta x$ dopo il fronte di discesa.
   - Analogo per l'output finchè non passa $\Delta w + \Delta x + \Delta y$ dopo il fronte di discesa
   
  Gli unici segnali espliciti sono:
   - il fronte di discesa del clock, che fa partire il ciclo del percorso dati
   - il fronte di salita del clock, che carica i registri dal bus C.

I limiti degli altri sottocili sono delterminati implicitamente dai tempi di propagazione dei circuiti.
È responsabilità del progettista assicurasi che $\Delta w + \Delta x + \Delta y + \Delta z$ giunga in anticipo rispetto il fronte di risalita del clock, per far funzionare il caricamento in ogni momento

## Comunicazione con la memoria
tramite i registri **MAR** e **MDR** a 32bit
- **MAR**: Memory Address Register
  - ha un solo segnale di controllo (input da bus C, ma nessun output verso bus B)
  - Mappatura particolare
    - Mar indicizza barole, mentre la memoria fisica byte
    - viene eseguita una moltiplicazione x4 -> perdo i 2 bit più a sinistra ed i 2 più a destra varranno 0
	 - è  caricato durante la discesa del Clock
	 - Accesso alla memoria entro il ciclo

- **MDR**: Memory Data Register
 - 2 segnali di controllo: lettura/scrittura da e per la memoria
  - Dopo una richiesta di lettura nel ciclo $k$, i dati saranno disponibili in MDR nel ciclo $k+2$
  - i dati sono disponibilli in MDR dopo 1 ciclo di data path
    - Durante il tempo di lettura dei nuovi dati, in MDR rimangono ancora i vecchi dati, su cui si può ancora operare
  - Si possono effettuare 2 richieste di lettura consecutive
    