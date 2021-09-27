  # IJVM 
IJVM è un microprogramma interpretato dalla microarchitettura

### STACK (pila)
é un area della memoria, dedicata alla memorizazione delle variabili, al cui interno non si stabiliscono indirizzi assoluti per le singole variabili.

-Si crea un registro(*LV*) che punta alla base delle variabili locali della procedura corrente

## Modello memoria IJVM
Esistono 2 modi diversi per concepire la memoria:
1. 1 array da 4.294.967.296 byte (4GB)
1. 1 array da 1.073.741.824 parole da 4 byte

La JVM non rende direttamente visibile a livello ISA gli indirizzi di memoria assoluti, ma utilizza degli **indirizzi impliciti** che forniscono la base per l'uso dei puntatori.
Questi puntatori sono l'unico modo per la **IJVM**  ha per accedere alla memoria.
Sono sempre definite le seguenti aree di memoria:
1. *Porzione costante della memoria*
   - **I programmi IJVM non posso scrivere in questa zona**
   - Contiene costanti, stringhe, puntatori ad altre aree
   -   Caricata quando il programma è portato in memoria
   -   Esiste un registro implicito, CPP, contenente l'indirizzo della prima parola della porzione costante di memoria
  1. *Blocco delle variabili locali*
     - Viene allocata all'invocazione di un metodo
     - Nella parte iniziale contiene i paramentri con cui è evocato il metodo
     - **Non contiente lo stack delgi operandi**
     - è presente un *LV* contenente l'indirizzo della prima locazione all'interno del blocco delle variabili locali
    1. *Stack degli operandi*
        - Non può superare una certa dimensione (stabilita in anticipo dal compilatore Java)
        - **è allocata direttamente sopra il blocco delle variabili locali** 
        - Non c'è un registro contenente l'indirizzo della parola in cima allo stack
        - Diversamente da *CPP* e *LV* questo puntatore (*SP*) cambia durante l'esecuzione del metodo a seconda dell'aggiunta e/o rimozione degli operandi dallo stack
    1. *Area dei metodi*
        - Regione di memoria in cui risiede il programma
        - Presente registro(*PC*) implicito con l'indirizzo della successiva istruzione da prelevare
        - è trattato come un array di byte

[[Istruzioni IJVM]]
