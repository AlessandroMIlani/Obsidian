- ## Teorema del confronto
 	 1°) 
	 Supponiamo che per x -> c, $f(x)$ abbia limite l, mentre $g(x)$ abbia limite m (entrambi finiti o infiniti).
	 Se esiste un intorno $I(c)$ di c t.c.  $f(x) ≤ g(x)$ in $I(c)$ \\ {$c$}, allora $l≤m$
	 - **Dimostrazione**
	     - Se $l = - \infty$ o  $m = + \infty$ non c'è nulla da dimostrare
	     - Consideriamo la funz. $h(x) = g(x) - g(x)$, Si ha per ipotesi $h(x)≥0$ in $I(c)$ \\ {$c$} Inotre, tramite l'algebra dei limiti ci assicura che:
	     $\lim_{x \to c} h(x) = \lim_{x \to c} f(x) - \lim_{x \to c} g(x) = m - l$
		 Applicando il corollario precendente alla funzione $h$, otteniamo $m-l ≥ 0$
	
	2° - caso finito)
	Date le funzioni $f, g, h$ supponiamo $f$ ed $h$ aventi stesso limite finito per $x \to c$: $\lim_{x \to c} f(x) = \lim_{x \to c} h(x) = l$
	Se esiste un intorno $I(c)$ nel quale siano definite le 3 funzioni (tranne al più nel punto c) e tale che: $f(x) ≤ g(x) ≤ h(x)$, $\forall x \in I(c)$ \  {$c$}
	Allora si ha anche $\lim_{x \to c} g(x) =l$
	
	 - **Dimostrazione**
	    - Fissato l'intorno di $I_\epsilon(l)$ di l, dall'ipotesi $lim_{x \to c} f(x) = l$ deduciamo l'esistenza dell'intorno $I'(c)$ di c t.c. : $\forall x  \in dom\ f$, $x \in I'(c)$ \ {$c$} => $f(x) \in I_\epsilon(l)$
       -  Notiamo che $f(x) \in I_\xi(l)$ può essere riscritta come $|f(x)-l| <\epsilon$ oppure $l- \epsilon < f(x) < l+ \epsilon$
       
	   - Simultaneamente, dall'ipotesi $lim_{x \to c} h(x) = l$ deduciamo l'esistenza di un intorno $I''(c)$ tc: $\forall x \in dom\ h$, $x \in I''(c)$ \ {$c$} => $l - \epsilon < h(x) < l - \epsilon$
	   -  Definiamo l'intorno $I'''(c) = I(c)\ \cap\ I'(c)\ \cap I''(c)$ 
	   In $I'''(c)$ \ {$c$} sono verificate le precedenti condizioni, quindi:
	   $x \in I'''(c)$ \ {$c$} => $l - \epsilon < f(x) ≤ g(x) ≤ h(x) < l + \epsilon$%
	   Cioè $g(x) \in I_\epsilon(l)$
	 
	 2° - caso infinito)
	Siano date le funzioni $f$ e $g$ ed esiste $\lim_{x \to c}f(x) = +\infty$ 
	Se esiste  $I(c)$ nel quale sono definite entrambe le funzioni (tranne al più in c) e tale che: $f(x) ≤ g(x)$,  $\forall x \in I(c)$ \ {$c$}
	Allora si ha che: $lim_{x \to c}g(x) = + \infty$   || Situazione analoga per $-\infty$ 
	
## Derivata e la sua continuità
	
- Sia $f$ una funzione definita in un $I(x_0) \in R$. Si dice derivabile in $x_0$ se esiste finito il limite del rapporto incrementale $\Delta f / \Delta x$ tra $x_0$ e $x$, per $x \to x_0$:
	$f'(x_0) = \lim_{x \to x_0}\frac{f(x)-f(x_0)}{x-x_0} = \lim_{\Delta x \to 0}\frac{f(x_0 + \Delta x) - f(x_0)}{ \Delta x}$
	Deicesi **Derivata (prima) di $f$ in $x_0$**
	

- Se $f$ è una funzione derivabile in un punto $x_0$, allora essa è continua in $x_0$
	  - **Dimostrazione**
	  La continuità di $f$ può essere espressa come: $\lim_{x \to x_0}(f(x) - f(x_0)) = 0$
	  Ora, se $f$ è derivabile in $x_0$, abbiamo:
	 
	$\lim_{x \to x_0}(f(x) - f(x_0)) = \lim_{x \to x_0}\frac{f(x)-f(x_0)}{x-x_0}(x-x_0) = \lim_{x \to x_0} \frac{f(x)-f(x_0)}{x-x_0}\lim_{x \to x_0}(x-x_0) = f'(x_0)*0 = 0$
	 
## Primitive e caratteristiche
- Ogni funzione $F$ derivabile in $I$ è tale che $F'(x) = f(x)$, $\forall x \in I$ --> dicesi una **primitiva** di $f$ in $I$ (o su $I$)
	 
	 - Se $F$ e $G$ sono 2 primitive di $f$ su intervallo $I$, allora esiste una costante $c$ tale che: $G(x) = F(x) +c$, $\forall x \in I$
	    - Sia $f$ una funzione integrabile su $I$ e sia $F$ una sua primitiva
	    Allora le priomitive di $f$ sono tutte le funzioni $F(x) + c$, $\forall c \in R$
		
		- L'insiemte delle primitive di $f$ si indica con $\int f(x) dx = F(x)+c$

## Monotonia
- $f$ dicesi **monotona crescente** su $I$ se presi $x_1$ e $x_2$ con $x_1 \leq x_2$ si ha $f(x_1) < f(x_2)$; in simboli:
$\forall x_1,x_2 \in I$, $x_1 < x_2$ => $f(x_1) \leq f(x_2)$
  - $f$ dicesi **monotona strettamente crescente** su $I$ se:
  $\forall x_1,x_2 \in I$, $x_1 < x_2$ => $f(x_1)<f(x_2)$
 
 - La **monotonia decrescente** si ottiene rovesciando la disuguaglianza tra $f(x_1)$ e $f(x_2)$ 
 - Se $f$ è strettamente monotona sul suo dominio, allora $f$ è iniettiva

## Concavità e Convessità

- $f$ **è convessa** in $x_0$ se esiste un intorno $I_r(x_0)\subseteq dom f$ tale che:
$\forall x \in I_r(x_0)$, $f(x) \geq t(x)$
Diciamo $f$ **strettamente convessa** se $f(x) > t(x)$ per $x \neq x_0$

- Le definizioni di funzione **concava** e **strettamente concava** si ottengono dalla precedente sostituendo i simboli $\geq$ e $>$ con $\leq$ e $<$

- Il punto $x_0$ dicesi **punto di flesso** di $f$ se esiste $I_r(x_0)\subseteq dom f$ in cui è soddisfatta una delle seguenti condizioni:

  $\forall x \in I_r(x_0)$, $\{^{se\ x< x_0,\  f(x) \geq t(x)}_{se\ x > x_0, \ f(x) \leq t(x)}$  --> Flesso **ascendente**

  $\forall x \in I_r(x_0)$, $\{^{se\ x< x_0,\  f(x) \leq t(x)}_{se\ x > x_0, \ f(x) \geq t(x)}$ --> Flesso **discendente**
  
 - Sia $I$ un intervallo ed $f$ una funzione derivabile su $I$; valgono le seguenti applicazioni:
    - Se $f$ è convessa su $I$, allora $f'$ è crescente su $I$
    -  Se $f'$ è crescente su $I$, allora $f$ è convessa su $I$
    -  Se $f'$ è strettamente crescente su $I$, allora $f$ è strettamente convessa su $I$
    -  Se $f$ è derivabile 2 volte:
         - se $f$ è convessa su $I$, allora $f''(x) \geq 0$ per ogni $x \in I$
         - se $f''(x) \geq 0$ per ogni $x \in I$, allora $f$ è convessa su $I$
         - se $f''(x) > 0$ per ogni $x \in I$, allora $f$ è strettamente convessa su $I$
       
## Polinomio di McLaurin
 - Il **Teorema di Taylor** fornisce una sequenza di approssimazioni di una funzione differenziabile attorno ad un dato punto mediante i polinomi di Taylor, i cui coefficienti dipendono solo dalle derivate della funzione nel punto.
    - (Resto di Peano) Sia $n \geq 0$ ed $f$ derivabile $n$ volte in $x_0$. allora vale la formula di Taylor:
       $f(x) = Tf_{n,x_0}(x)+o((x-x_o)^n)$, $x \to x_0$
	   dove
	   $Tf_{n,x_0}(x)=\sum_{k=0}^n\frac{1}{k!}f^{(k)}(x_0)(x-x_0)^k$
- Un polinomio di Taylor con $x_0=0$ ischiama **sviluppo di McLaurin**
   - Il polinomio di McLaurin di una funzione pari contiene soltanto potenze pari della variabile indipendente (viceversa per le funz. dispari)

- $e^x = \sum_{n=0}^\infty\frac{x^n}{n!} = 1 +x+\frac{x^2}{2}+\frac{x^3}{6}+...+\frac{x^n}{n!}+o(x^n) \forall x \in R$
- $ln(1+x) = \sum_{n=0}^\infty(-1)^{n+1}\frac{x^n}{n} = x -\frac{x^2}2+\frac{x^3}3-\frac{x^4}4+...+\frac{(-1)^{n+1}}nx^n+o(x^n) per |x|<1$
- $\sin(x) =\sum_{n=0}^\infty\frac{(-1)^n}{(2n+1)!}x^{2n+1} = x - \frac{x^3}6 + \frac{x^5}{120}-\frac{x^7}{5040}+...+\frac{(-1)^nx^{2n+1}}{(2n+1)!}+ o(x^{2n-1}) \forall x \in R$
- $\cos(x) =\sum_{n=0}^\infty\frac{(-1)^n}{(2n)!}x^{2n} = 1- \frac{x^2}2 +\frac{x^4}{24}-\frac{x^6}{720}+...+\frac{(-1)^nx^{2n}}{(2n)!}+o(x^{2n}) \forall x \in R$
-  $(1+x)^\alpha = \sum_{n=0}^\infty\binom{\alpha}{n}x^n = 1+ \alpha x + \frac{\alpha(\alpha -1)}{2}x^2+\frac{\alpha(\alpha-1)(\alpha-2)}{6}x^3+...+\binom{\alpha}{n}x^n+o(x^n) per |x|<1$
     - P.S. con $\binom{\alpha}{n}$ non si intende il Coefficente binomiale standard, ma quello generalizzato  $\binom{\alpha}{n} = \frac{\alpha(\alpha-1)(\alpha -2)...(\alpha-n+1)}{n!}$
     
## Media Integrale
- Si definisce **media integrale** (o valore medio) di $f$ sull'intervallo [a,b] il numero:
$m(f;a,b) = \frac1{b-1}\int_b^af(x)dx$

- *Teorema:* Sia $f$ una funzione integrabile sull'intervallo $[a,b]$. la media integrale di $f$ su $[a,b]$ soddisfa le seguenti disuguaglianze: 
$inf_{x \in [a,b]}\ f(x)\leq m(f;a,b) \leq sup_{x \in [a,b]}\ f(x)$
Inoltre, se $f$ è continua su [a,b], esiste almeno 1 punto $z \in [a,b]$ tc. $m(f;a,b)=f(z)$

   - **Dimostrazione** (da sistemare)
      - Poniamo $i_f = inf_{x \in [a,b]}\ f(x)$ e $s_f = sup_{x \in [a,b]} f(x)$. 
   Per ogni $x \in [a,b]$ si ha: $i_f \leq f(x) \leq s_f$
   
     - Considerando il confronto tra integrali definiti (dati $a < b$ se $f \leq g$ in [a,b] -> $\int_a^bf(x)dx \leq \int_a^bg(x)dx$) e l'espressione dell'integrale di una costante, si ottiene:
	 $(b-a)i_f = \int_a^bi_fdx\leq \int_a^bf(x)dx \leq \int_a^b s_f dx = (b-a)s_f$
	 - Dividendo per (b-a) perviene la convergenza degli integrali.
	 Se ora supponiamo $f$ continua per il teorema di Weierstrass si ha: $i_f = min_{x \in [a,b]}\ f(x)$ e $s_f = max_{x \in [a,b]}\ f(x)$
	 e dunque la convergenza garantisce che $m(f;a,b)$ è un valore compreso tra il minimo ed il massimo di $f$ su [a,b].  L'esistenza di un punto $z$ per cui vale definizione di integrale definito
	 
	 
## Teorema fondamentale del calcolo Integrale

- Sia $f$ definita e continua nell'intervallo $I$ della retta reale.
Sia $x_0 \in I$ fissato e sia $F(X) = \int_{x_o}^xf(s)ds$ una funzione integrale di $f$ su $I$. Allora $F$ è derivabile su ogni punto di $I$ e  si ha $F'(x) = f(x), \forall x \in I$

   - **Dimostrazione**
	   -  Fissiamo da prima un punto x interno ad $I$ e sia $\Delta x$ un incremento tale che $x + \Delta x$ appartenga ad $I$. 
	   Consideriamo il rapporto incrementale della funzione $F$ tra $x$ e $x+\Delta x$:
	   $\frac{F(x+ \Delta x)- F(x)}{\Delta x} = \frac{1}{\Delta x}(\int_{x_0}^{x+ \Delta x}f(s)ds-\int_{x_0}^xf(s)ds)$
	   
	   - Considerando l'additività rispetto il dominio di integrazione ($\int_a^b=\int_a^c+\int_c^b$) si ha:
	   $\int_{x_0}^{x+\Delta x}f(s)ds= \int_{x_0}^xf(s)ds+\int_x^{x+\Delta x}f(s)ds$
	   e dunque: $\frac{F(x+ \Delta x)- F(x)}{\Delta x} =\frac{1}{\Delta x}\int_x^{x+\Delta x}f(s)ds= m(f;x,x+ \Delta x)$
	   - Abbiamo stabilito che il rapporto incrementale della funzione integrale $F$ tra $x +\Delta x$ coincide con la media integrale di $f$ sull'intervallo di estremi $x$ e $x+ \Delta x$. Possiamo dunque applicare il Teorema della media integrale alla funzione continua $f$; esso garantisce l'esistenza del punto $z=z(\Delta x)$ in tale intervallo, per il quale si ha $m(f;x,x+\Delta x)=f(z(\Delta x))$ e dunque:
	   $\frac{F(x+\Delta x)-F(X)}{\Delta x}=f(z(\Delta x))$
	   - Facciamo ora tendere $\Delta x$ a 0. Supponiamo $\Delta x >0$ dalla relazione $x\leq z(\Delta x)\leq x+ \Delta x$ e dal 2° Teorema teorema del confronto sui limiti, deduciamo -> $\lim_{\Delta x \to 0^+}z(\Delta x)=x$
	   - Similmente $\lim_{\Delta x \to 0^-}z(\Delta x)=x$ e quindi: $\lim_{\Delta x \to 0}z(\Delta x)=x$.
	   Usando la continuità di $f$ in $x$ e il suo mantenimento si ha: $\lim_{\Delta x \to 0}f(z(\Delta x))=f(\lim_{\Delta x \to 0}z(\Delta x))=f(x)$
	   Pertanto, vedento l'integrale definito come: $\int_If=\sum_{k=1}^nc^k(x_k-x_{k+1})$ 
	   |con $x_k$ punti della suddivisone di $I$ e $c_k$ la costante di $f$ su $I$ |
	   otteniamo la tesi: $F'(x)=\lim_{\Delta x \to 0}\frac{f(x+ \Delta x)-F(x)}{\Delta x}= f(x)$
	   
	   - Nel caso $x$ sia un estremo, è sufficente considerare i limiti unilaterali destro e sinistro.

## Successioni Ricorrenti


## Teorema di esistenza degli zeri
	
 - Data una funzione reale $f$, chiamiamo **zero** di $f$ ogni punto $x_0 \in dom\ f$ in cui la funzione si annulla
 - Terorema: sai $f$ una funzione continua nell'intervallo chiuso e limitato $[a,b]$. Se $f(a)f(b) < 0$ cioè se $f$ assume valori di segno discorde agli estremi dell'intervallo, allora esiste uno zero di $f$ nell'intervallo aperto $(a,b)$.
 Se inoltre $f$ è strettamente monotona in $[a,b]$, allora lo zero nell'intervallo è unico
  
## Teorema di convergenza del metodo di Newton
  - 