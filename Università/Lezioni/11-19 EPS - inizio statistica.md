## Statistica
- Introduzione alla statistica
- Statistica descrittiva per variabili quantitative:
	- Indici di posizione
	- indici di variabilità/dispersione




### Introduzione

La statistica è una scienza (ramo della matematica) che trae informazioni efficaci relativamente a grandi gruppi limitandosi ad esaminare solo alcuni elementi 
E' basata quindi sulla raccolta e l'analisi di set di dati.
Tutto ciò che concerne...:
- raccolta
- trattamento
- sintesi
- analisi 
- interpretazione
- rappresentazione

...dei dati, appartiene al campo della statistica.

**Esempi**
- Sondaggi
- Studi sugli effetti di una terapia
- Analisi da parte di una ditta per stabilirte i paramentri dei propri prodotti
- ...

```mermaid 
	stateDiagram-v2
Popolazione --> Campione :campionamento
Campione --> Popolazione :inferenza
````
- Non posso misurare tutta la popolazione (es. Stress test di tutte le auto)
	- quindi prendo un sottoinsieme **rappresentativo** della popolazione
		- Se non è rappresentativo, si crea un bias (errore commesso sistematicamente): es. devo prendere le misure per dei parcheggi, ma nel campione di auto ho solo Smart

#### Consideriamo dati univariati
 (dati con una sola variabile alla volta)

Processo di raccolta dei dati::
- Campionamento: Consiste nel passata dalla popolazione d'interesse, a una collezione di casi (unità statistiche) il campione, su cui misurare una certa caratteristica (la Variabile Aleatoria)
	- Campione = $X=(X_1,X_2,X_3,...,X_n)$ Collezione di V.A. Identicamente distribuite e indipendenti
-  ![[Pasted image 20211122164239.png]]
	-  $x=(x_1,x_2,x_3,..,x_n)$ è la collezione delle misure, ovvero dei valori assunti da X sugli elementi del campione

Misura:
- Applicare la v.a. ai casi estratti nel campione

---
### Livelli di misura e tipologie di dati
- Dati di tipo quantitativo(o numerico):
	- Discreti
	- Continui
- Dati di tipo qualitativo (o categoriale) -> (detti fattori in R)
   Non sono espressi tramite numeri
	- Nominali --> i valori assunti sono puramente nominali, per esempio la regione in cui si è nati / colore preferito ecc...
	- Ordianali --> i valori assunti sono categorie e possono essere ordinate, per esempio un giudizio
- Character data (non raggruppano in categorie)
	- Dati di tipo identificativo, per esempio un ID 
	- Data & time data

---
 - Com'è strutturato un dataset?
	 - Righe -> casi
	 - Colonne -> variabili
		 - incrocio le righe --> ho un dato specifico

 ## Statistica descrittiva per dati numerici univariati

- Indici di posizione
	- media
	- mediana
	- (moda)
- Indici di variabilità:
	- range
	- IQR
	- varianza 

```R
Per aggiungere un pacchetto ad R:
- install.packages("nome-pacchetto") nella console di R
- richiamarlo nel file eseguibile con: library("nome-pacchetto")
----------------------------------------
Richiamo singola variabile: nome_dataset$nome_variabile
es: babyboom$running.time[8] <-- 8 elemento d€l vettore running time
-----------------------------------
babyboom$running.time[-c(7,8,9)] <-- elimina gli elementi nelle posizioni indicate
```

#### Media campionaria
$(x_1,x_2,x_3,..,x_n)$ --> $\bar x_n=\frac{1}{n}\sum_{i=1}^nx_i=\frac{1}{n}x_1 +\frac{1}{n}x_2+...+\frac{1}{n}x_n$

- Corrisponde a un "baricentro" dei dati
- è influenzata dai valori estremi
- La media degli scarti dalla media è = 0
	- Scarto dalla media = differenza tra un punto e la media = $x_i - \bar x_n\ \ \ \ x_i \in campione$
- La media in R si calcola con mean()

```R
mean(babyboom$wt, na.rm=T)

babyboom -> dataset
wt -> variabile in quesitone
na.rm=T -> ignora i dati mancanti, scritti come NA (not available)
--------------

```


#### Mediana
- valore centrale
	- maggiore di metà dei dati e minore dell'altra metà

Se volessimo calcolarla senza R, dovremmo ordinare i dati

Mediana si calcola con median()
```R
median(babyboom$wt, na.rm=T)
```
 
 $(x_1,x_2,x_3,..,x_n) --> (x_{(1)},x_{(2)},x_{(3)},..,x_{(n)})$ 
 - I valori con il pedice tra parentesi, indicano un array ordinato
	 - quindi $x_{(1)}$ è il valore più piccolo e $x_{(n)}$ è il più grande
- Se n dispari:
	- $\bar M$: elemento di posto $\frac{n-1}{2}+1$
	$\bar M$ = $x(\frac{n-1}{2}+1)$
- Se n pari
	-  $\bar M$ media degli elementi $\frac n2,\frac n2+1$
	 $\bar M = \frac{[x(\frac n2)+x(\frac n2 +1)]}{2}$