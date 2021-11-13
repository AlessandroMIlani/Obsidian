## Tipologie Variabili aleatorie
1. Variabili aleatorie di Bernulli
1. Variabili aleatorie bionamiali
2. Variabili aleatorie geometriche

Fanno parte del gruppo di variabili discrete **note**
- hanno una definizione specifica dato che sono utilizzate spesso

### V.A. di Bernulli

- Esperimento probabilistico di riferimento

Prova Bernoulliana -> esperimento probabilistico con esito dicotomico (binario -> T/C, v/f, si/no ...)

Spazio campionario $\Omega$={s,f} (successo/fallimento)

- Definizione della variabile

X: associa il valore 1 al successo e 0 al fallimento
X({s})=1 e X({f}) = 0

- PMF

$p_x:$ $Im(X)$ -> $R$
$x$ --> $p_x(x)=P(X=x)$
$Im(X)=\{0,1\}$
$p_x(0)=P(X=0)=P(X^{-1}(\{0\}))=P(\{f\}) = 1-p$ 
$p_x(1)=P(X=1)=P(X^{-1}(\{1\}))=P(\{s\}) = p$
Chiamiamo $p$ la probabilità di successo ($1-p$ è la prob. d'insuccesso)

X ~ Bernulli(p) (tradotto -> X ha legge di probabilità di Bernulli)
(tilde = ha legge di probabilità/ha distribuzione di / è distribuita come una )

$p_x(x)=\{^{p\ \ \ \ \ \ \ \ \ \ x=1}_{1-p\ \ \ \ \  x=0}$

P = 1/0 sono casi degeneri, il risultato è certo e non ha senso parlare di probabilità

**OSS**
- si possono avere v.a. diverse con la stessa PMF

**Esempio**
1. lancio moneta, successo uscita testa da una moneta $\Omega$={T,C}
2. Lancio dado, successo numeri dispari $\Omega$={1,2,3,4,5,6}
	- Y: Y({1})=Y({3})=Y({5})=1 Y({2})=Y({4})=Y({6})=0

![[Pasted image 20211028120829.png]]


PMF di Y: 
- $p_y: Im(y)$ --> R
- $y$ --> $p_y(y)=P(Y=y)$
- $Im(Y)=\{0,1\}$
- $p_y(\{1\})=P(Y=1)=P(Y^{-1}(\{1\}))=P(\{1,3,5\})= 3/6 = 1/2$
- $p_y(\{0\})=P(Y=0)=P(Y^{-1}(\{0\}))=P(\{2,4,6\})= 3/6 = 1/2$

### V.A. Binomiale
- Esperimento probabilistico
- 
Costituito da una generalizzazione della prova di bernulli, ad un numero n. di prove riepetute, indipendenti (non si influenzano/dipendono a vicenda) e identicamente distribuite (la p, probabilità di successo è costante durante le prove)

Es. n=10 -> lancio 10 monete insieme oppure lancio 10 volte la stessa moneta

$\Omega$={$\omega_1,\omega_2,,,\omega_n$} con $\omega_i \in$ {s,f}, i=1,..,n} ($\Omega$= stringhe lunghe n.)

- Definizione delle V.A.

X: V.A. Che conta il numero di successi Ottenuti in n. prove -> X((s, f, f))=1

![[Pasted image 20211028123626.png]]

$Im(X)=$ {0,1,2,3} -> generalizzato: $Im(X)=$ {0,1,2,3,..., n}

- PMF di X

$Im(X)=$ {1,2..., n}
x ---> $p_x(x)=P(X=x)$
(fisso n=3 per comodità)
$p_x(0)=P(X^{-1}(\{0\}))=P(\{(f,f,f\})= (1-p)(1-p)(1-p)=(1-p)^3$

$\Omega$={$(\omega_1,\omega_2,\omega_3)$: $\omega_i \in$ {s,f}, i=1,2,3} = $\Omega^1$ x $\Omega^1$ x $\Omega^1$
$\Omega^1=\{s,f\}$ $P^1$=({s})=p; $P^1$({f})=1-p
($\Omega^1, P^1$) sono gli stessi spazi che corrispondono alle prove di Bernoulli indipendenti e sono variabili identicamente distribuite

$p_x(1)=P(X^{-1}(\{1\}))=P(\{(s,f,f\},\{(f,s,f\},\{(f,f,s\})=$
$=P(\{(s,f,f\}) + P(\{(f,s,f\}) +P(\{(f,f,s\})$
$=p(1-p)^2+(1-p)p(1-p)+(1-p^2)p=3p(1-p)^2$

? Come proseguiamo ?
- $p_x(K)=P(X=K)=\binom{n}{k}p^k(1-p)^{n-k}$ 

$K \in Im(X)=$ {0,1,2,..., n} 
p: prob. di successo in ogni prova 

X ~ Binomiale(n, p) ha PMF come: $p_x(K)=P(X=K)=\binom{n}{k}p^k(1-p)^{n-k}$ 

### Variabile aleatoria geometrica

Svolgiamo prove ripetute di tipo bernulliano (ripetiamo in maniera identica una prova che ha un esito dicotomico, che può essere descritto con due etichette(Successo=S e Fallimento=F)), fino a quando non otteniamo il primo successo.

$\Omega=\{\{S\},\{F,S\},\{F, F,S\}...\}=\{n-1\ F,S\}$

Definiamo X come contatore delle prove eseguite:

- X=$\{F,F,S\}=x=3$

Questa ci permette di stimarle l'immagine che è infinita($N$\0).

$Px(1)$->{$successo$}

Con P che indica la probabilità di successo nella singola prova

$Px(2)$->{$fallimento,successo$}->P(2)=$(1-p)^1$ x $p$

$Px(K)$=Probabilità della stringa di lunghezza $K$=$(1-p)^{K-1}$ x $p$

### Variabile aleatoria Passon

Osservo il verificarsi di un evento d'interesse raro (a bassa frequenza) in una data finestra temporale o spaziale

- Px(k)=P(X=x)=$frac{\lambda^k}{k!}e^{-\lambda}$

[[Media e Varianza V.A. Discrete]]