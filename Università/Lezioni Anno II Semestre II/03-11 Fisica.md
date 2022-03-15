## Neggi di Newton - introduzione
- introduzione concetto di forza $\vec F$
- $\vec F$ elettrostatica <-> Q carica
- condensatore $G$

- Grandezze adimensionali
	- tangente
	- angolo
- Grandezze dimensionali

| grandezza             | sigla            | unità di misura                 |
| --------------------- | ---------------- | ------------------------------- |
| lunghezza             | l                | 1m                              |
| tempo                 | t                | 1s                              |
| velocità llungo x     | 1m/1s            | 1m/s=$1ms^{-1}$                 |
| accelerazione lungo y | $1\frac{m/s}{s}$ | $1m/s^2=1ms^{-2}$               | 
| Forza                 | $F_x$            | 1 N = $1Kgms^{-2}$              |
| Lavoro                |                  | $1 J = 1 Kgm^2s^{-2}$  --- KCal |
| Energia               | E                |                                 |
| Potenza               |                  | 1 W = $1Kgm^2s^{-3}$            |
| Carica                | Q                | 1 C (coulomb)                   |
| Corrente Elettrica    | I                | 1 A = $1 Cs^{-1}                |
| Capacità              | C                | 1 F (Fared)                     |
| Induttanza            | L                | 1 H                             |


Unità fondamentali -> 1m, 1s, 1Kg, 1C

---
- Eq. paragprano quantità con le stesse dimensioni
	- Es: $\vec F = m\vec a$
		- Forza = $1Kg\cdot 1\frac{m}{s^2}=1Kgms^{-2}$ -- massa = 1 Kg -- accelerazoine = 1 $ms^{-2}$

 - "Lunghezza grande" cosa si intende?
	 - 1 m = 1000 mm = 1000000 $\mu m$ 
	
	
---

## Leggi di Newton
Sono un approssimazione
- velocità piccola ||$\vec v$|| << c (velocità della luce)
- oggetti "grandi" rispetto alle dimensioni $\not h$  (dimensioni della mecc. quantistica)

#### 3 leggi
1. **Un corpo non soggetto ad interazioni (libero) si muove a velocità costante $\vec v$ costante**
2. **m$\vec a$ = $\vec F$ Se conosco $\vec F$ allora posso calcolare $\vec a$ -> calcolo $\vec v(t)$ -> calcolo $\vec r(t)$**
	- non ho interazioni $\vec F$ = 0 => $\vec a$ = 0 => $\vec v$ è costante
1. **Legge di azione-reazione. Se ho un corpo a ed un corpo b** ->  $\vec F_a(b) = - \vec F_b(a)$  
	- nel caso terra/persona, la massa della terra è circa $10^{24}$, arrotondanod una persona a $10^2$ ci sono 22 ordini di grandezza di differenza (anche rispetto all'acceleraiozne che si subisce vicendevolemtne)


misurare "la massa"
- 2 molle uguali (con attaccati 2 corpi diversi) a cui applico la stessa forza
	- misuro accelerazioni diverse, posso calcolare le masse
		- il corpo più leggero viene accellerato maggiormente (**formule su slide**)

Peso $\not =$ massa
- $\vec P = m \vec g$ (se peso 1Kg, la forza peso è crica 10 N)





### Elettrostatica
Forza tra 2 cariche statiche (= ferme), generalmente chiamate $q_1$ e $q_2$ 
Oltre che la forza peso, sono influenzate dalla forza elettrostatica

(formule e grafico da slide)

- 2 cariche positive/negative -> si respingono
- Se 1 neg, 1 pos -> si atraggono 


**intensità (modulo) della forza**
$||\vec F|| = \frac{|q_1||q_2|K_e}{(distanza)^2}$ 
$1N = 1Kgms^{-2} = \frac{\[k_e\](1C)^2}{(1m)^2}$
$K_e = $\frac{Nm^2}{1C^2}= 1Kgm^3s^{-2}C^{-2} = 9\cdot 10^9 \frac{Nm^2}{C^2}$



**$\vec F$ usando le componenti**
(grafico slide)
- $\vec r_1 - \vec r_2$ (vettore che va da 2 a 1) 
- $||\vec r_1 - \vec r_2||$ = distanza^2
- $\frac{\vec r_1 - \vec r_2}{||\vec r_1 - \vec r_2||}= \vec u_{12}$ -> vettore di modulo 1 che inidca la **direzione**
- $\frac{K_e q_1q_2}{||\vec r_1 -\vec r_2||^2}$ -> **modulo**
- $q_1,q_2 > 0$ -> respingono  ||  $q_1 < 0 < q_2$ -> vettore cambia il verso
- $\vec F_{1(2)}=\frac{\vec r_1 -\vec r_2}{||\vec r_1-\vec r_2}\ \frac{K_e q_1 q_2}{||\vec r_1 - \vec r_2||^2}$
- In componenti
	- (procedimento da slide)
	- $F_{1(2)},x = \frac{K_e q_1,q_2}{[\sqrt{(x_1-x_2)^2+(y_1-y_2)^2}]^3}\cdot (x_1-x_2)$  
	- $F_{1(2)},y = \frac{K_e q_1,q_2}{[\sqrt{(x_1-x_2)^2+(y_1-y_2)^2}]^3}\cdot (y_1-y_2)$  


Se ho una terza carica?
$\vec F_3 = \vec F_{3(1)} + \vec F_{3(2)}$
$\vec F_1 = \vec F_{1(2)} + \vec F_{1(3)}$
...
Se ci fossero 5 cariche, ogni carica subirebbe l'influenza delle altre 4 -> $\sum_{i=1}^5 F_1(i)$ 
	- $\vec F_1 = \sum^5_{i=2}\frac{K_2 q_1 q_i}{||\vec r_1-\vec r_i||^3}$ 


