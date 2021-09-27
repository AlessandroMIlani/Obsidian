# Passaggi

data la funzione $\int^6_2(\frac12x^2\log_ex-\frac34x^2)dx$

1. Suddivisione con N=5
   - 6-2 = 4 /5 -> intervalli da 0.8
     - [2-2,8][2,8-3,6][3,6-4,4][4,4-5,2][5,2-6,0]
	    - calcolo il punto medio di ogni intervallo
	        2,4| 3,2 | 4,0 | 4,8 | 5,6
	    - calcolo f(x) con x = i punti medi
	     -1.7987| \-1.7249 | \-0.9096 | 0.7905 | 3.493 
	 - La formula del punto medio è $\frac{b-a}{N}\sum^N_{i=1}(w_i)$ 
	   - Sulla base della formula del punto medio l'integrale dato vale circa -0.1197
2. Stimare l'errore compiuto dall'approssimazione seguendo lo schema:
   - Formula teorica dell'approssimazione integrale è: 
   $\int^b_af(x)dx$
     - Con la formula del punto medio con N suddivisioni è:  
     $|E|\leq\frac{K}{24N^2}(b-a)^3$
	    - Dove K è uguale a:
	    $max_{[a,b]}|f''|$ 
		
3. - Calcolo il valore di K = 1.7918
   - Calcolo l'errore massimo commesso = $\frac{K}{24N^2}(b-a)^3$	= 0.1911