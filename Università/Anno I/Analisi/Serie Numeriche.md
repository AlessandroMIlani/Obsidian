- Sia data la succesione $\{a_n\}$, si vuol definire, quando possibile: $\sum^{+\infty}_{n=0}a_n=a_0+a_1+a_2...$

	- $a_n=1 \ \ \ \ \forall n \geq 0 \to \sum^{+\infty}_{n=0}1$
	- $a_n=\frac{1}{2^n} \ \ \ \ \forall n \geq 0 \to \sum^{+\infty}_{n=0}\frac{1}{2^n}$
	- $a_n=(-1)^n \ \ \ \ \forall n \geq 0 \to \sum^{+\infty}_{n=0}(-1)^n$
----
La seire è la sommatoria dei termini della successione
- La successione è composta dai singoli termini
---

- Definiamo la successione $\{S_n\}$ come *successione delle somme parziali:* $S_N=\sum^{N}{n=0}a_n$ 

	-  Allora $\sum^{+\infty}_{n=0}a_n=\lim_{N \to +\infty}S_N$  [Se il limite esiste]
	
	
- La serie $\sum^{+/infty}_{n=0}a_n$:
	- **Converge**: se $\exists s \in R \ t.c. \lim_{N \to +\infty}S_N \to S$  [S = somma della serie]
	- **Divergente**: se $\lim_{N \to +\infty}S_N=+\infty/-\infty$
	- **Indeterminata**: Se $\lim_{N \to +\infty} S_N$ Non esiste
- $a_n=q^n$
  - $q \geq 1 \to +/infty$
  - $q \leq -1 \to \ \nexists$  
  - $|q| < 1 \to \frac{1}{1-q}$

- Sia data la successione $\{a_n\}$, se la serie $\sum^{+/infty}_{n=0}a_n$ è convergente, allora $\lim_{n \to +\infty}a_n=0$
---
Per essere convergente, q dev'essere compreso tra -1 e 1.
Se compreso, allora a $n \to +\infty$ avremo $\frac{1}{Q^\infty}$ che converge a 0

**NB** $\lim_{n \to +\infty}a_n=0 \neq \sum^{+\infty}_{n=0}a_n$ convergente 

---

- Nel caso di **Serie a termini positivi** ($a_n \geq \forall n$) la convergenza o divergenza si determina dalla *velocità con cui $a_n$ tende a 0* 
  - $a_n \to 0$ "velocemente" =>  $\sum^{+\infty}_{n}a_n$ converge ($a_n = \frac{1}{2^n}$)
   - $a_n \to 0$ "lentamente" =>  $\sum^{+\infty}_{n}a_n$ diverge ($a_n = \frac{1}{n}$)
 - Considerando $\sum^{+\infty}_{n=1} \frac{1}{n^\alpha}$ con $\alpha$ >0 
   - Diverge se $0<\alpha\leq 1$
   - Converge se $\alpha > 1$

## Criteri di convergenza 
- **Criterio del confronto**:  siano $\{a_n\},\{b_n\}\ t.c. \ a_n \geq 0, b_n \geq 0 \forall n$ 
 SE $a_n \leq b_n \forall n$ allora:
  - $\sum^{+/infty}_{n=0}b_n$ convergente => $\sum^{+\infty}_{n=0}a_n$ convergente [Se $b_n$ è più grande di $a_n$ e converge, allora anche $a_n$ converge]
  - $\sum^{+/infty}_{n=0}a_n$ divergente => $\sum^{+\infty}_{b=0}a_n$ divergente [Se $a_n$ e diverge ed è più piccola di $b_n$, allora anche $b_n$ diverge]
  