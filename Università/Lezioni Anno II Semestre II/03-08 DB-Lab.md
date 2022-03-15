## Generalizzazioni

Una generalizzaziooe mette in relaizone una o più entità $E_1, E_2,...,E_n$ con una entità **E**, che le comprende come casi particolari:
- **E** è generalizzazione di $E_1, E_2, ..., E_n$
- $E_1,E_2,...,E_n$ sono specializzaiozni (o sottotipi) di **E**  => (Es. **E** = data di nascita -> $E_1$ giorno $E_2$ mese $E_3$ Anno)


![[Pasted image 20220308142545.png]]
Persona è una generalizzazione di Studente e Lavoratore
- E (genitore) è generalizzazione di $E_1,...,E_n$ (figlie)
	- Ogni proprietà di E è significativa per $E_1,E_2,...,E_n$ (es. attributo CodiceFiscale)
		- **Propietà Ereditarietà** -> basta indicarli nel genitore e sono valide anche per i figli
	- Ogni occorrenza di $E_1,E_2,...,E_n$ è occorrsenza anche di E

### Tipi di generalizazioni
- **Totale**, ogni occorrenza dell'entità genitore è occorenza di almeno una delle entità figlie altrimenti è **parziale**
- **Esclusiva** se ogni ocorrenza dell'entità genitore è occorrenza di al più una delle figlie, altrimenti è **sovrapposta**

> Considerando solo generalizzazioni esclusive e distinguiamo tra totali e parziali

#### Osservazioni
1. Possono esistere gerearchie a più livelli e multiple generalizzazioni allo stesso livello
2. Un'entità può essere inclusa in più gerarchie, come genitore e/o come figlia
3. Se una generalizzazione ha solo un'enittà figlia si parla di *sottoinsieme*


### riassunto sui modelli, utilizzando un modello
![[Pasted image 20220308144042.png]]

Alcuni vincoli non sono esprimibili tramite i costrutti offerti dal modello. ES:
- Le gerarchie di generalizzazione non possono avere cicli
- La cardinalità minima deve essere minore della cardinalità massima
- Non ci devono essere cicli di identificatori esterni

### Documentazione associata agli schemi concettuali
Uno schema E-R non è quasi mai sufficente a raprresentare tutti gli aspetti di un'applicazione, compenso con le "reogle aziendali"

#### Regole aziendali
Sono uno strumento per rappresentare "regole" del dominio applicativo, in particolare:
- Descrizione di un concetto (entità, relazione, attributo) <- *dizionario dei dati*
- Vincolo di integrità (distingue le basi di dati leggittime dalle altre ) <- *asserzioni*
	- es. stipendio di un direttore > stipendio di un dipendente -- Impossibile da scirvere nello schema, devo considerarlo dopo
- Derivazione (concetto ottenuto attraverso inferenza o calcoli da altri concetti dello schema) <- *regole che specificano le operazioni necesarie per ottenere il concetto derivato*

## Dizionario dei dati (entità)
![[Pasted image 20220308145831.png]]

## Dizionario dei dati (relazioni)
![[Pasted image 20220308145854.png]]

### Vincoli di integrità
esempi:
1. direttore di un dipartimento **Deve** guadagnare più di un inpiegato
2. un inpiegato che non afferisce a nessun dipartimenot **non deve** partecipare a nessun progetto

quindi:
- devono essere atomici
- utile la forma deve/non deve
- non tutte le informazioni che si ricevono da un clienti sono utili per la base di dati

#### Derivaizoni
es.
1. il budget di un progetto si ottiene moltiplicando per 3 la somma degli stipendi degli impiegati che vi partecipano

quindi:
- frase atomica
- utile la forma "si ottiene"


---
