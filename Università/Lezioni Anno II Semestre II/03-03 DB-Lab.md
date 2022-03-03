## Cardinalità di una relazione
- è una coppia di valori associati a ogni entità che partecipa ad una relazione
	- (cardinalità minima, cardinalità massima)
- I valri specificano il numero minimo e massimo di occorrenze della relazione cui ciascuna occorrenza di una entità può partecipare
```mermaid 
	flowchart LR
	A(Impiegato) --2,5--> Assegnamento 
	Assegnamento --0,50--> D(Incarico) 
```
- un determinato impiegatopuò avere un minimo di 2 incarichi ed un amssimo di 5
- lo stesso incarico può essere assegnato da  0 a 50 impiegati

- Per sempliicare, siusano solo 3 simboli:
	- **Per cardinalità minimo**
		- 0 -> partecipazoine opzionale
		- 1 -> partecipazione obbligatoria
	- **per cardinalità massima**
		- 1 -> 
		- N -> Non pole alcun limite
### Rappresentazione di una cadinalità
- SI riscrivolo le identità come elementi di un insiemi
- Le relazoini come collegamenti tra gli elem. dei 2 insiemi

![[Pasted image 20220303113610.png]]

## Classificazione delle relazioni
 Con rifrimento alla **cardinalità massima** le relazioni si definiscono:
- uno a uno (1,1)
- uno a molti (1,N)
- molti a molti (N,N)

 Per le **cardinalità minime**, il caso di partecipaizone obbligatoria (1) è raro 

#### Esempi
 ```mermaid 
	flowchart LR
	A(Impiegato) --0,1--> Assegnamento 
	Assegnamento --0,N--> D(Incarico) 

	B(Cinema) --1,1--> ubicazione 
	ubicazione --0,N--> F(Località) 

	C(Comune) --1,1--> Ubicazione 
	Ubicazione --1,N--> E(Regione) 
```

![[Pasted image 20220303113826.png]]

**Relazioni 1 a 1 molto rere:**
![[Pasted image 20220303113901.png]]


## Cardinalità degli attributi
- è possibile associare delle cardinalità anche agli attributi. con 2 scopi:
- inidcarne di opzionali
- indicarne di multivalori

### Identificatori delle entità
Strumenti per identificare unicovamente delle occorrenze di un'entità.
Possono essere costituiti da:
- attributi dell'entità: **identificatore interno**
- entità esterne collegate attraverso una relazione: **identificatore esterno**

- i pallini sono gli attirbuti, quelli anneriti gli identificatori
![[Pasted image 20220303120415.png]]  ![[Pasted image 20220303120433.png]]

### Osservazioni sugli identificatori
- Ogni enittà deve possedere almeno un identificatore
- Un identificatore può coinvolgere più attirbuti, ognuno dei quali con cardinalità (1,1)
- Un identificatore esterno è possibile solo attraverso una relazione a cui l’entità da identificare partecipa con cardinalità (1,1)
- Un'identificazione esterna può coinvolgere entità a loro volta identificate esternamente, purché non vengano generati cicli