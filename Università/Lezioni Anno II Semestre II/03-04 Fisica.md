## Eq. e Eq. differenziali
Utili per apire i fenomeni elettrici, onde elettromagnetiche e circuite

P.S. 40+ minuti di ripasso lezione precendente

## approssimaizone con polinomi (da completare)
Approssimaizoni sempre migliori:
- $x(t) -> x_{app} = x(t_0)$
- $x(t) -> x_{app}=x(t_0)+v(t_0)(t-t_0)$
- $x(t) -> x_{app}(t) = x



## Velocità (da completare)
è un vettore, dire solo 130 km/h è un informazione parzila (mancano direzione e verso)
- velocità media: $\frac {\vec r(t_1)-\vec r(t_0)}{t_1-t_0} = \vec V_m\{t_1,t_0\}$ $||\vec V_m||$ -> valore misurato dal "tutor"
	- caso moto 1D: $\vec r(t)=(X|t) = x(t)\vec i
		- $\vec(t_1)-\vec r(t_0) = (x(t_1)\vec i)-(r(t_0)\vec i) = (t(t_1)-r(t:0)\vec i)$
		- $\vec v_m(v_1,t_0) = \frac{r(t_1)-r(t_0)}{t_1-t_0}$
		- $V_{media},r=\frac{r(t_1)-r(t_0)}{t_1-t_0} = \frac {\Delta x}{\Delta t}$
Il tachimetro NON misura la velocità media, ma quella istantanea
$\vec v_{in}(t_1,t_0) = \frac{\Delta\vec r(t_1,t_0)}{\Delta t} = \frac{\vec r(t_1)-\vec r(t_0)}{t_1-t_0}$
se t1 -> t0 allora ottengo la velocità istantanea

$lim_{t_1\to t_0} ... (da finire di copiare )

Come porto tutto questo su un computer?
- uso prog. di amnipolazione simbolica (maxima)
- numericamente, ma ha dei problemi
	1. devo fare il conto per ogni $t_0$
	2. $t_1$ rispetto $t_0$? scelgo $\Delta t = t_1 - t_0$


## Accelerazione
è un vettore che indica la variazione di velocità nel empo

$a_m(t_1,t_0) = \frac{\vec v(t_1)-\vec v(t_0)}{t_1-t_0} = \frac{\Delta \vec t}{\Delta t}$
$\vec a(t_0) = lim_{t_\ \to t_0} \frac{\Delta \vec v (t_1,t_0)}{\Delta t} = \frac {a\dev v}{at}$
![[Pasted image 20220304105134.png]]
