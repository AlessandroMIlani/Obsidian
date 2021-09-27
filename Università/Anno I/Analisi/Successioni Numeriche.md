Una **successione numeriche** è una funzione $a: N \to R\ \ \ \ (a:\{n  \in N | n \geq n_0\}\to R$ per qualunque $n_0 \in N$

### Assegnazione successioni

- Formula esplicita
  - $a_n=\frac{1}{n+1}$ | $a_n=(-1)^n$ | $a_n=n!$
 - Formula ricorsiva
   - $\{^{a_0=x}_{a_{n+1}=a_n^2-a_n}$
   
  ### Posso definire le succ. come:
  - **Monotonia**
    - Crescente: $a_n+1 \geq a_n$
    - Decrescente: $a_{n+1}\leq a_n$
   - **Limitatezza**
      - Inferiormente Limitata: $\exists m \in R\ t.c. \ m \leq a_n \forall n \in N$
      - Superiormente Limita: $\exists M \in R \ t.c. \ M \geq a_n \forall n \in N$
      - Limitata: $\exists m,M \in R \ t.c. \ m \leq a_n \leq M\ \ \forall n \in N$
    - **Convergenza** 
       - Convergente: a $l \in R$: $\lim_{n \to +\infty}a_n=l$ $\forall \xi > 0\ \ \exists N_\xi >0 \ t.c. \ n > N_\xi$=>$|a_n-l|<\xi$
       - Divergente: a $+\infty/-\infty$: $\lim_{n \to +\infty} a_n = +\infty/-\infty \ \forall M >0 \ \ \exists N_\xi > 0 \ t.c. \ n>N_\xi$ => $a_n>M / a_n < -M$
       - Indeterminata: $\nexists \lim_{n \to +\infty}a_n$

## Teoremi
1. Se $\{a_n\}$ è convergente, allora $\{a_n\}$ è limitata
2. Se $\{a_n\}$ è monotona allora $\lim_{n \to +\infty}a_n$ esiste
   -  $\{a_n\}$ Crescente [decrescente] è sup.[inf] limitata => $\{a_n\}$ è convergente
   -  $\{a_n\}$ Crescente e sip. illimitata => $\{a_n\}$ è divergente

## Tabella riassuntiva
|q | Limitatezza| Monotonia | Limite |
|:---:|:---:|:---:|:---:|
| $q>1$|no|Crescente| $+\infty$|
|$q=1$|si|Costante|1|
|$0<q<1$|si|Decrescente|0|
|$-1<q<0$|si|no|0|
|$q=-1$|si|no|$\nexists$|
|$q<-1$|no|no|$\nexists$|