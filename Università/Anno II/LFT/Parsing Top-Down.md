**problema**

Data una grammatica G=(V,T,P,S) e una stringa $w \in T^*$ determinare se
$$S => \alpha_1 => \alpha_2 => ... => w$$
O equivalente se esiste una albero sintattico di G con radice S e prodotto $w$.
- La costruzione dell'automa corrispondente a G produce un PDA non deterministico
- Per alcune G sappiamo che non è possibile trovare una DPDA

# Strategia per il parsing top-down
Data una grammatica G=(V, T, P, S) e una stringa $w \in T^*$, il parsec cerca di ottenere una derivazione a sinistra S =>$_{lm}^* e$ in cui, il passo i, il parser sa che: **S=>$_{lm}^*uA\beta$** e serve stabilire se $uA\beta$=>$_{lm}^*w$.

Ci sono 2 casi da considerare
- Se u non è prefisso di w, allora il parsec rifiuta $w$.
- Se w = uav, allora il parser deve scegliere una produzione per scrivere: A -> $\alpha_1 | ... | \alpha_n$  e per farlo può usare a come "guida", a patto che tale simbolo identifichi univocamente l'$\alpha_i$ tale che $\alpha_i\beta$=>$_{lm}^*av$

![[Pasted image 20211109093321.png]]

### Stringhe annullabili (NULL)
**definizione**
Data una grammatica G, diciamo che $\alpha \in (V \cup T)^*$ è *annullabile*, se scriviamo NULL($\alpha$) se e solo se $\alpha$=>$_G^*\epsilon$, ovvero se $\alpha$ può essere riscritta nella striga vuota

**Determinare se stringa annullabile**
- Se NULL($X_1$),....,NULL($X_n$), allora NULL($X_1...X_n$)
- Se esiste una produzione A -> $\alpha \in P$ e NULL($\alpha$), allora NULL(A)

**Note**
- La stringa vuota è annullabile
- combinando 1 e 2, se A -> $\epsilon \in P$ implica NULL(A)
- Una stringa con termini terminali, non è annullabile

###Inizi di una stinga
- data una grammatica G, e una stringa  $\alpha \in (V \cup T)^*$ , indichiamo con FIRSTR($\alpha$) gli inizi di $\alpha$, ovvero l'insieme dei simboli terminali che possono trovarsi all'inizio delle strighe derivate da $\alpha$. Formalmente: $$FIRST(\alpha) =^{def}\{ a \in T | \alpha =>_G^* a\beta\}$$

![[Pasted image 20211109095316.png]]

### Come calcolare FIRST
- Calcolo First($\alpha$) per induzione, seguendo le regole:
1. FIRST($\epsilon$)= 0
2. FIRST($\alpha$)={a}
3. FIRST(A)=$\bigcup_{A->\alpha}FIRST(\alpha)$
4. FIRST($X\alpha$)={$_{FIRST(X)\ \ altrimenti}^{FIRST(X)\cup FIRST(\alpha) \ \ se\ NULL(X)}$

**Attenzione**
Applicando le regole, posso ritrovarmi nella forma: FIRST(A)=FIRST(A) $\cup$ S, dove S è un insieme di terminali -> quindi posso semplificare in FIRST(A) = S. 

### Seguiti di una variabile (FOLLOW)
**Def**
data una grammatica G e una variabile $A \in V$, indichiamo con FOLLOW(A) i seguiti di A, ovvero l'insieme dei simboli terminali che possono seguire A in una forma sentenziale. FOrmalmente: $FOLLOW(A)=^{def}\{a \in T |  S =>_G^* \alpha a\beta\}$
![[Pasted image 20211109103308.png]]

#### Come calcolare FOLLOW
**FASE 1**
Annoto relazioni di appartenenza e inclusione insiemistica secondo il seguente algoritmo:
- Annotare $\$ \in FOLLOW(S)$
- Ripetere i passi seguenti per ogni produzione per ogni variabile nel corpo di queste:
	1. Se A --> $\alpha B\beta$, allora annotare FIRST($\beta$)  ⊆ FOLLOW(B)
	2. Se A --> $\alpha B\beta$, allora anotare FOLLOW(A) ⊆ FOLLOW(B)
		- caso particolare di (2): se A --> $\alpha B$, allora annotare FOLLOW(A) ⊆ FOLLOW(B)

**Fase 2**

- Si determinano i seguiti prorogando i simboli terminali (e \$) rispettando l'ordine delle inclusioni insiemistiche ⊆ che sono state annotate
- Per grammatiche complesse può essere utile fare una tabletta con 2 colonne, l'elenco di tutte le variabili nela prima ed i seguiti corrispondenti alle variabili nela seconda 

![[Pasted image 20211110112614.png]]

| Variabili | Follow      |
| --------- | ----------- |
| E         | $, )        |
| E'        | $, )        |
| T         | $, +, )     |
| T'        | $, +, \)     | 
| F         | $, +, \*, \) |

## Insiemi guida
**def**
Data una grammatica G e una produzione A --> $\alpha$, indichiamo con GUIDA(A -> $\alpha$) l'insieme guida di A -> $\alpha$, ovvero l'insieme 
$$Guida(A -> \alpha)=^{def}\{_{FIRST(\alpha)\ \ \ altrimenti}^{FIRST(\alpha)\cup FOLLOW(A)\ \ se\ NULL(\alpha)} $$

**intuizione**
 Un parser predittivo che sceglie di riscrivere la variabile A usando la produzione A -> $\alpha$ si aspetta di leggere nella stringa d'input uno dei simboli nell'Insieme guida di A -> $\alpha$
 
 Sono 2 casi da considerare:
 1. Il simbolo è uno degli inizi di $\alpha$
 2. $\alpha$ è annullabile e il simbolo è uno dei seguiti di A


[[Grammatiche LL(1)]]