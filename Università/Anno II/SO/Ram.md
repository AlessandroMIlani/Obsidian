## RAM
- **Risorsa disponibile ai processi**
- **Accesso della cpu, alla ram attraverso gli indirizzi che produce**

CPU -> la vediamo come generatore di un flusso d'indirizzi (dati / flussi)
Ram -> array d'indirizzi

- Quando la cpu esegue un programma, cerca gli indirizzi di ram indicati nel programma, ma ciò può impedire la rilocabilità del codice

- Adesso, la maggior parte dei linguaggi permette la rilocabilità del codice (in java, non ci siamo mai preoccupati d'idicare le celle di ram)
	- Ci pensa il compilatore: 
	- Programma sorgente (indirizzi simbolici) -> compilaotre -> indirtizzi assoluti

```mermaid 
	flowchart TD
Prog.sorgente --> compilatore
compilatore --> indirizzi-assoluti
compilatore --> c(moulo oggetto \n ind. riallocabili base + 100byte)
compilatore --> linker
modulo.oggetto --> linker
linker --> d(modulto rilocabile)
d --> loader
e(lib. di sistema) --> loader
loader --> f(modello eseguibile)
````
- Gli indirizzi assoluti non si usano quasi più
- Creo dei moduli oggetto, i quali sfruttano indirizzi rilocabili
	- Spesso un programma è composto da più file più file oggetto, quindi il linker li unisce
	- il loader unice le lib. di sistema necessarie e crea il modello eseguibile.
		-  Quindi, la cpu eseguendo il programma cerca un inidirizzo logico (nome persona in rubrica) che viene collegato ad un indirizzo fisico in Ram (numero di telefono)

- Indirizzi generati della CPU -> Spazio degli Indirizzi Logici del processo
	-	<==> Binding tra i 2 spazi degli indirizzi
- Indirizzi in Ram -> spazio degli indirizzi fisici del processo

### MMU
**Memory Manag. Unit**

```mermaid 
	flowchart LR
a(CPU \n Ind. logico) --> b(+)
subgraph MMU
c(registro di rilocazione) --> b
end
b --> d(indirizzo fisico)
````

**Linking**
Permette la composizione di più moduli che compongono lo stesso programma
(es. Modulo1 con funzione -> modulo2 con dichiarate le variabili della funzione)

**Loading**
 È il software di sistema che carica il file eseguibile generato dal linker nella memoria principale
 
Sono detti:
- statici, se eseguiti prima dell'esecuzione (quando creo il mio "a.out")
	- Si caricano tutte le librerie (COMPLETE) in memoria 
```mermaid 
	flowchart LR
a(oggetto 1) --> linker
b(oggetto 2) --> linker
c(oggetto 3) --> linker
linker --> d(modello eseguibile)
````

- Dinamici, se avvengono durante l'esecuzione (ho il mio a.out, ma l'aggancio con una eventuale funzione stampa, viene creato al primo richiamo della funzione)

#### Librerie dinamiche
- Può venir modificata senza chiede ai programmi invocanti di venire ricompilati 

#### Allocazione della ram ai processi
Diversi approcci
1. Allocazione contigua
2. paginazione
3. segmentazione

##### Allocazione Contigua
Una parte viene subito assegnata al SO, noi ci occuperemo del resto disponibile ai processi utente

