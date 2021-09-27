## Formato di una microistruzione

![[Pasted image 20210603103724.png]]

- **Addr**: Indirizzo microistruzione seguente
- **JAM**: determina come selezionare l'istruzione successiva
- **ALU**: bit controllo ALU e shifter
- **C**: selezione registro memorizzazione velore bus C
- **MEM**: Controllo operazioni sulla memoria
- **B**: selezione input bus B


- **TOT 36 Bit per istruzione**

---


## Aggiungere Istruzione MIC1

- "annotare" il nuovo comando in ijvm.conf assegnandoli un valore esadecimale non ancora utilizzato
  - es. -> 0x50 new_comand 

- Creare nuovo labeled statements in mic1ifvm.mal
	- es. -> label new_comand 0x50 (stesso codice presente in ijvm.conf)
	 
- Definire le verie istruzioni da eseguire:
  - bipush1	SP = MAR = SP
bipush2	PC = PC + 1; fetch			
bipush3	MDR = TOS = MBR; wr; goto Main1	


---

**Sommare due registri**
(uno dei 2 deve per forza essere H)
SP = MDR = SP +1

*Attenzione* ad utilizzare solo istruzioni legali:
 - MDR = SP + MDR
 - H = H - MDR 	
 _Sono istruzioni illegali_
 
 Tabella riportante le operazioni legali dove:
   - **Source** può essere: 	MDR, PC,MBR,MBRU,SP,LV,CPP,TOS o OPC
   - **DEST** può essere MAR,MDR,PC,SP,LV,CPP,TOS,OPC o H 
   Sono concessi assegnamenti multipli
   
 ![[Pasted image 20210612173430.png]]
 
 Le operazioni indicate nella tabella possono essere estese sfruttando lo *shift register*
 H = MBR << 8
 
 **Accesso alla memoria** 
 In lettura/scrittura tramite MAR/MDR viene semplicemente indicando rispettivamente rd e wr
 *N.B.* il dato letto non è disponibile nel ciclo successivo
 
 **Lettura di opcode**
 Di 1 byte dal flusso di istruzioni ISA(IJVM) tramite la porta PC/MBR viene indicato da
 - fetch
 
 il byte letto può essere utilizzato per il salto al *termile del ciclo successivo*
 Ambedue le letture della memoria (dati e fetch) possono procedere il parallelo.
 
 ATTENZIONE alle sequenze illegali:
 - MAR = SP; rd
 - MDR = H
 entrambe assegnano un valore a MDR al termine del secondo ciclo (no bueno)
 
 ## Direttive di salto
 Ogni riga che non contenga un salto esplicito, viene tradotta impostando NEXT_ADDRESS all'indirizo della microisturzione della riga seguente
 
 Per eseguire il **salto incondizionato** è suffciente indicare al termine della riga:
 goto label
 forzando in questo modo il valore a NEXT_ADDRESS
 
 Per i **Salti condizionati** 