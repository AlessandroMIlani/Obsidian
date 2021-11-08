algoritomo del banchiere
costanti:
- M -> numero tipi di risorse
- N -> numero processi

Variabili:
- Disponibili[M] -> disopnibilità per ogni tupo di risorsa
- Massimo[N][M] 
- Assegnate[N][M] 
- Necessarie[N][M] 
	- Coordinate (i,j) -> informazioni relative processo $P_i$ sull'uso della risorsa $R_j$ 

### Algoritmo
Diviso in 2:
- algoritmo che gestiscce le richieste dei processi
- algoritmo di verifica che uno stato sia sicuro

- Dichiamo che X < Y, quando  X e Y sono array e vale: $\forall i\ X[i]<Y[i]$

##### 1) Verifica stato sicuro
1. siano lavoro e fine 2 array di lunghezza  M e N rispettivamente
2. lavoro = disponibili
3. fine[i] = falso per ogni $i \in [i,N]$
4. cerca $i \in [1,N]$ | fine[i] = falso & necessarie[i]$\leq$ lavoro
5. se trovato:
	- lavoro = lavoro + assegnate[i]
	- fine[i] = vero
	- goto(4)
1. Se $\forall i \in[i,N]$, fine[i] = vero -> lo stato è sicuro  


**esempio** 

è sicuro?

| PX  | A   | R   |
| --- | --- | --- |
| P1  | 5   | 5   |
| P2  | 2   | 2   |
| P3  | 2   | 7   |
Libere ---> 3 

Disponibili = [3]
Necessarie: [5][2][7] | Assegnate: [5][2][2]
Fine = [F,F,F] | Lavoro = [3]

- cerco P con fine = falso e necessarie < di disponibili
	- salto P1 (necessarie =5) e vado a P2
- Lavoro passa a 5
- adesso cerco p con fine = fine e max 5 risorse richieste
	- Servo P1
- aggiorno lavoro a 10
- Servo P3    

##### 2) Gestione delle richieste 

M tipi di risorse diverse, quindi una richiesta di un processo è un array( int ) di M componenti. (es. v2 è quante istanze servono della risorsa 2, se nessuna Vx=0 )

- matrice necessarie[N][M] -> contiene tutte le richieste (ogni riga, un processo pn diverso) 

- Se richieste < necessarie[j]?
	- Richieste $\leq$ disponibili?
		- se Falso -> Pj aspetta le risorse  
		- Se Vero simula l'assegnazione delle risorse e verifica se lo stato è sicuro:
			disponibili = disponibili - richieste
		 assegnate[j]= assegnate[j] + richieste 
		 necessarie[j]=necessarie[j] - richieste
			- Se sicuro, assegna sul serio
			- Se non è sicuro, aspetta 


## Algoritmi rilevazione del DL
Gia visto i Grafi di assegnazione delle risorse
- Quando abbiamo 1 sola istanza per risorsa e cerco un loop, posso rinominare quel grafo come "Grafo d'attesa" (schema a video)

Se ho più istanze per più risorse?
- Utilizzo i già visti:
	-  un array disponibili[M] (M = n. tipi di risorse)
	- una matrice assegnate[N][M] (N = n. processi)
	- matrice richieste[N][M] -> quali richieste pendenti ...
- Nuovi array 
	- un array int lavoro[M] = disponibili
	- un arrai boolean fine[N] 
		- ```C
	 for(i $\in$ [1,N])
	 	if(Assengate[i]={0,..0})
				fine[i]= true;
			else fine[i]=false;
		while((esiste i) Fine[i]==false & richieste[i] <= lavoro){
			lavoro = lavoro + assegnate[i];
			fine[i]=true;
		For(i in [1,N])
			if(fine[i]==false) //DEADLOC
		}```
	 
	 
** Quando ha senso applicarli?**	 
- Di tanto in tanto, a intervalli predefiniti
- Quando un proc. richiedere una risorsa e la trova occupata
- Quando l'utilizzo della cpu scende sotto una certa soglia

**Cosa fare se rilevo un deadlock?**
- Terminare qualche processo (quindi liberare risorse)
	- Se non basta, continuo a terminare processi
		- devo considerare vari fattori quando termino i processi:
			- risultati parziali / transazioni (rollback) / interazioni con l'utente
			- Devo scegliere buone vittime
- Alternativa: prelazione risorse e redistribuzione     

[[Ram]]