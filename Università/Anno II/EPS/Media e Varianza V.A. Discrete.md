## Media e varianza di V.A. Discrete

- X, PMF
	-  Cerchiamo quantità **riassuntive/sintetiche della PMF** (es. un numero solo)

### Def
Diciamo **Media**(o valore atteso/medio) della v.a. X la seguente quantità:
$$Ɇ(X)= \sum_{x \in Im(X)}x\cdot p_X(x)= \sum_{x \in Im(X)}\cdot P(X=x)$$
**OSS**
1.  Sinonimi: media / valore atteso / valore medio / mean
1.   Cosa abbiamo calcolato?
 		-  $Ɇ(X)= \sum_{x \in Im(X)}x$ <- media pesata
			- $P(X=x)$ <- è il peso per la media pesata 


 Ɇ(X) è la media pesata dei valori assunti da X... Perché?
 - $x_1,x_2,..,x_n$ -> valori in Im(X)
 - $p_X(x_1)=p1,p_2,...,p_n$ -> pesi di probabilità

--> Inserisco i valori di Im(X) in una ruota della fortuna ($x_1,k_1$ volte,$x_2\ \ k_2$ volte ecc..) e faccio girare la ruota K volte (K=$k_1+k_2+...+k_n$)

- $\frac{x_1\cdot k_1+x_2\cdot k_2+...+x_n,k_n}{K}$
	- $x_1\cdot\frac{k_1}{K}+ x_2\cdot\frac{k_2}{K}+...+x_n\cdot\frac{k_n}{K}$
		-  $\frac{k_n}{K} \approx p_n$
	- Se K è "grandissimo", la frequenza si dice relativa 
	- $x_1\cdot p_1+x_2\cdot p_2+...+x_n\cdot p_n = Ɇ(X)$
	 
	 #### Momenti di ordine K
Definiamo momenti di ordine K della V.A. Discreta $x$ la media di $x^k$ cosi' calcolata:

$E(x^k)=\displaystyle \sum_{x \in imm(x)} x^k\times px(k)$
#### Varianza
Definiamo varianza di x la seguente quantità:

$var(x)=E[(x-E(x))^2]=\displaystyle \sum_{x \in Imm(x)}(x-E(x))^2 \times P(X=x)$

È una quantità sicuramente maggiore di zero poiché $(y-E(X))^2\ge0$ e $P(X=x)\ge0$.

La varianza, scarto quadratico medio, è la media degli scarti quadratici ed è quindi una misura di dispersione, ovvero mi dice mediamente quanto posso trovare valori lontani dalla media.

La varianza di x vale 0 ($Var(x)\equiv 0$) quando gli scarti quadratici sono nulli, ovvero $(y-E(X))^2=0$. Avviene quando la varianza di $y$ ha un solo punto nell'immagine, che è costante degenere($c$) che prende un solo valore.

La radice quadrata della varianza è definita **deviazione standard**

$\sqrt{Var(x)}=StDev(x)$

##### Esempio
$x$
$Imm(x)=\{1,-1\}$
$P(x)=(1/2)$

$E(x)=\displaystyle \sum_{x \in Imm(x)}x \times P(X=x)=1 \times 1/2-1 \times1/2=0$
$Var(x)=\displaystyle \sum_{x \in Imm(x)}(x-E(x))^2 \times P(X=x)=(1-E(x))^2\times P(X=1)+(-1-E(x))^2\times P(X=-1)=1\times 1/2 +(-1)^2\times 1/2=1$

$y$
$Imm(y)=\{-100,100\}$
$E(y)=\displaystyle \sum_{y \in Imm(y)}x \times P(Y=y)=100\times P(Y=100)-100\times P(Y=-100)=0$
$Var(y)=\displaystyle \sum_{y \in Imm(y)}(y-E(y))^2 \times P(Y=y)= (100-0)^2\times 1/2+ (-100-0)^2\times 1/2=100^2=10000$

#### Proprietà di media e varianza
- $E(aX+bY)=aE(X)+bE(Y)$
	- La media di combinazioni lineari è uguali alla combinazione lineare di medie
	- La media è un operatore lineare
	- $E(10Y)=1-\times E(y)$
	- $E(X+)$
- $Var(X)=E(x^2)-E^2(x)$
	- Possiamo riscrivere la varianza come momento secondo meno quadrato della media
- La varianza non è lineare: $Var(aX+b)=a^2\times Var(x)$
	- $Var(10X)=10^2\times Var(X)=100\times Var(X)$
	- La varianza è quadratica nelle costanti e invarianti nelle traslazioni

#### Media e varianza delle variabili discrete note
##### Prove bernulliane
$E(x)=\displaystyle \sum_{x\in Imm(x)}x\times P(X=x)=0\times P(X=0)+1\times P(X=1)=1\times p=p$

$Var(x)=\displaystyle \sum_{x \in Imm(x)}(x-E(x))^2 \times P(X=x)=p^2\times(1-p)+(1-p^2)\times p=p\times (1-p)$

##### Binomiale
$E(x)=n\times p$
$Var(x)=n\times p\times(1-p)$
##### Geometrica
$E(x)=\frac{1}{p}$
$Var(x)=\frac{1-p}{p^2}$
###### Poisson
$E(x)=\lambda$
$Var(x)=\lambda$

##### Ipergeometrica
$E(x)=n\times \frac{S}{N}$

[[PMF Congiunte]]