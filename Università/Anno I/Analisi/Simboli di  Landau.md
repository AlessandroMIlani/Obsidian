## Confronto crescita di 2 succesioni $\{a_n\}$ e $\{b_n\}$
- Sfrutto il rapporto $\frac{a_n}{b_n}$
  - se $\lim_{n \to +\infty} \frac{a_ n}{b_n}=0$, $\{a_n\}$ tende a $+\infty$ più **lentamente** di $\{b_n\}$ 
  - se $\lim_{n \to +\infty} \frac{a_ n}{b_n}=\infty$, $\{a_n\}$ tende a $+\infty$ più **velocemente** di $\{b_n\}$ 
  - se $\lim_{n \to +\infty} \frac{a_ n}{b_n}=l \in (0, +\infty)$, $\{a_n\}$ e $\{b_n\}$ tendono a $\infty$ **con uguale velocità** 

## Gerarchia infiniti
Fattoriali > Esponenziali > Potenze > Logaritmi

$(n^n, n!)>(2^x,3^x)>(x,x^2,x^n)>(ln(ln(x)), ln(x), log_k(x))$

## Simboli di Landau
Date 2 successioni $\{a_n\}$ e $\{b_n\}$ t.c. $\{b_n\} \neq 0$ definitivamente si dice che:

 -  Se $\lim_{n \to +\infty} \frac{a_ n}{b_n}=0$ $\{a_n\}$ è "o piccolo" di $\{b_n\}$ e si scrive $a_n = o(b_n)$
 -  Se esiste $c >0\ \ t.c. |\frac{a_n}{b_n}|\leq c$ per $n \to +\infty$, $\{a_n\}$ è "O grande" di $\{b_n\}$ e si scrive: $a_n = O(b_n)$
 -  Se esistono $c,C >0\ \ t.c.\ \ c \leq |\frac{a_n}{b_n}|\leq C$ per $n \to +\infty$,   $\{a_n\}$ è "$\theta$ grande" di $\{b_n\}$ e si scrive: $a_n = \theta(b_n)$
 -  Se $\lim_{n \to +\infty}\frac{a_n}{b_n}=1$ si dice $\{a_n\}$ equivalente a $\{b_n\}$ e si scrive $a_n \sim b_n$
 
 Riassumendo:
 - o piccolo -> cresce più lentamente
 - O grande -> cresce **NON**  più velocemente
    - o piccolo -> sottintende un o grande ma non viceversa
  - $\theta$ -> $\{^{a_n O(b_n)}_{a_n non o(b_n)}$
    -$\sim$ è una proposizione di $\theta$, dove il limite del rapporto è = 1 