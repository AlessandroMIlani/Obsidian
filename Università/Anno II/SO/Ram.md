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

##### Librerie dinamiche
- Può venir modificata senza chiede ai programmi invocanti di venire ricompilati 

#### Allocazione della ram ai processi
Diversi approcci
1. Allocazione contigua
2. paginazione
3. segmentazione

##### Allocazione Contigua
Una parte viene subito assegnata al SO, noi ci occuperemo del resto disponibile ai processi utente.

![[Pasted image 20211113161040.png]]
- Mando in esecuzione 2 programmi (P1 e P2) e successivamente termina P1#
- ![[Pasted image 20211113161149.png]]
- Se mando P3 in running quale spazio occupa?
	- Se va ad occupare lo spazio di P1, si crea un **frammento interno** tra lui e P2, ovvero un frammento troppo piccolo per contenere un processo e, quindi, viene inglobato dalla memoria circostante
	- La parte libera sottostante P2 fiene detto **Frammento esterno** in quanto abbastanza grande da essere utlizzato da altri processi.

**Tipo di allocazione**
1. Best Fit
2. First Fit
3. Worst Fit

*Esempio:*
Processo richiede 10 "unità" di ram e ci sono liberi blocchi da 15,11,25 e 5
1. Best Fit --> sceglierà quello più piccolo in cui entra 10 (11), e il frammento interno che si crea, viene inglobato da p;
2. Worst Fit --> si sceglie il frammento più grande (25), supponendo che nello spazio rimanente possa entrare un altro processo
3. First Fit --> Il primo in grado di contenere il processo (15), può generare un frammento interno o esterno in base alla parte restante

**Memoria inutilizzabile**
A forza di frammenti interni, la RAM è "spezzettata"
- La tecnica First Fit fa perdere circa il 50%, ogni N blocchi perdo N/2, quindi perdo 1/3 della ram.
- Best first è simile al First
- Worst è la peggiore, a lungo andare crea frammenti inutilizzabili

![[Pasted image 20211113162214.png]]

**Come ottengo la rilocabilità?**
 Invece di far partire la memoria da 0, iniziamo a u numero differente (0-max --> 100-100+max)
 Per la CPU gli spazi sono sempre[0,max]
 ![[Pasted image 20211113162610.png]]
 In questo modo viene guadagnata la rilocabilità. Perché?
 *Swapping/Schedulind* medio termine: ![[Pasted image 20211113162934.png]]
 - C è un processo in ready e supponiamo occupi da 100 a 150
 - C va in Ram grazie allo scheduler, ma cambia indirizzo: la sua partizione è [350,400]

Tale approccio ha 2 caratteristiche:
1. Vincolo di continuità -> spazio indirizzi fisici di ciascun processo è contiguo
2. Assunzione implicita -> caricamento completo del processo

##### Paginazione
Non sfrutta la continuità:
- Spazio ind. fisici di P= $I_A \cup I_B \cup I_C$

Immaginiamo la ram divisa in porzioni dette **Frame**
Mem. logica del processore divisa in parti di pari dimensione dette **pagine**
- un indirizzo logico è una cpiia <p,o> (p -> pagina | o -> offset)

![[Pasted image 20211113165748.png]]

La paginazione permette la rilocabilità? SI

Supponiamo uno spazio gramdne $2^m$ e pagine grandi $2^n$, facendo $\frac{2^m}{2^n}$ ottengo il numero di pagine necessarie al processo
- (m-n)bit per scrivere la componente p dell'indirizzo logico 
- per l'offset mi serve invece il dato n

**Approfondimento swapping:** *il S.O. deve caricare il processo:*

```C
if(#frame liberi >= pagine p){
	foreach(pagine di P){
		<<identifica frame libero>>
		<<crea entry nella tabella delle pagine p>> ||
		<<causa la copiatura della pagina nel fram>>
		<<aggiorna le informazioni sui frame liberi>>
	else...
		TO BE CONTINUED..
	}
}
```

![[Pasted image 20211113170452.png]]

