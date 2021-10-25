# Linguaggi Liberi
## Introduzione
**Motivazione**
- il Linugaggio $L=\{a^nb^n| n \in N\}$ non è regolare
- ponendo a = (e b =), notiamo che L è il linguaggio delle parentesi bilanciate
- Lingaggio L è fondamentale per descrivere la struttura di espressioni e blocchi nei lingu. di programmazione

## Grammatiche libere dal contesto
Una grammatica è una quadrupla $G = (V,T,P,S)$
- V è un insieme finito di variabili
- T è un alfabeto di simboli terminali
- P è un insieme finito di produzioni della forma A -> $\alpha$ in cui
	- $A \in V$ è detta testa della produzione
	- $\alpha \in (V \cup T)^*$ è dellta corpo della produzione
- $S \in V$ è il simbolo iniziale della grammatica

**Convenzioni**
![[Pasted image 20211019102817 1.png]]

## Derivazioni
**Definizioni**
Fissata G, def. le derivazoini in un passo e in zero o più passi come segue:
- scriviamo $\alpha A \beta$=>$G\ \alpha\gamma\beta$ se A -> $\gamma \in P$
	- In tal caso dichiamo che $\alpha\gamma\beta$ __deriva __ _in un passo_ da $\alpha A \beta$ in G
- Scrivimao $=>^*_G$ per la chiusura riflessiva e transitiva di $=>_G$, ovvero: 
	- $\alpha =>^*_G\alpha$
	- se $\alpha => G \beta\ e \ \beta =>^*_G\gamma$ allora  $\alpha =>^*_G \gamma$

Quando $\alpha=>^*_G$ diciamo che $\beta$ deriva in zero o più passi da $\alpha$ in G 

**Convenzione**
Omettiamo G da $=>_G$ e $=>^*_G$ quando è chiaro a quale grammatica ci si riferisce.

## Linguaggio generato da una grammatia
Dato G, il linguaggio generato da G, denotatoda L(G) è definito come:
$$L(G)=^{def}\{w \in T^*| S =>^*_Gw\}$$
esempio $L(G)=\{w \in \{\ 0,1\}^*| w =w^R\}$
**Definizione**
Diciamo che è L un linguaggio libero se esiste una grammatica libera che lo genera

## Grammatiche  e Linguaggi regolari
**Teorema**
Per ogni linguaggio regolare L eisisre una grammatica G t.c. L(G)=L
**Dimostrazione**
Slide

**Osservazioni**
- il teorema mostra che le grammatiche possono generare tutti i linguaggi regolari
- Sappiamo che le grammatiche possono generare linguaggi non regolari
- I linguaggi liberi includono propriamente i linguaggi regolari


## Esempio: comando di assegnamento in Java
grammatica: $$(\{S,R,E\},\{=,[,],c,x\},P,S)$$

In cui P è l'insieme di produzioni
- S -> R = E
	- R -> x | R[E]
	- E -> c | R

[[Alberi Sintattici]]