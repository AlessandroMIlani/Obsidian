![](https://users.cs.fiu.edu/~prabakar/cda4101/Common/notes/figs/mic1-architecture.gif)


## Sincronizzazione del data path
![[Pasted image 20210603114040.png]]
  1) stabilizzazione segnali di controllo
  2) un regisro viene strittosul bus B
  3) ALU e shifter calcolano
  4) I risultati passano per il Bus C e tornano ai registri

## Registri

- **MAR**: Memory Address Register
  - ha un solo segnale di controllo (input da bus C, ma nessun output verso bus B)
  - Mappatura particolare
    - Mar indicizza barole, mentre la memoria fisica byte
    - viene eseguita una moltiplicazione x4 -> perdo i 2 bit più a sinistra ed i 2 più a destra varranno 0
	 - è  caricato durante la discesa del Clock
	 - Accesso alla memoria entro il ciclo

- **MDR**: Memory Data Register
  - Dopo una richiesta di lettura nel ciclo $k$, i dati saranno disponibili in MDR nel ciclo $k+2$
  - i dati sono disponibilli in MDR dopo 1 ciclo di data path
    - Durante il tempo di lettura dei nuovi dati, in MDR rimangono ancora i vecchi dati, su cui si può ancora operare
  - Si possono effettuare 2 richieste di lettura consecutive
  - 2 segnali per la lettura e scrittura da e per la memoria
 
 - **PC**: Program COunter
   - Lettura del programma del livello ISA da eseguire

- **MBR**: Memory Buffer Register
   - registro a soli 8bit
   - Ha 2 bit di controllo per l'output su B
     - Signed ed unsigned
    - per i tempi di accesso valgono le considerazioni fatte per MDR
    -   Serve 1 segnale per avviare il fetch di memoria su MBR
 - Es. Signed / Unsigned
   - Unsigned: si introducono 24 zeri supplementari alla sinistra degli 8 bit di MBR
   - Signed: se il bit più significativo è = 1 si esegue il complemento a 2:
     - 10011010 -> 11111111 11111111 11111111 10011010   
	
- **H**
  - input sinistro dell'ALU
  - un solo bit di controllo per l'input dal bus C
  - output verso l'ALU sempre attivo

## Organizzazione dei sottoclicli
![[Pasted image 20210603114303.png]]