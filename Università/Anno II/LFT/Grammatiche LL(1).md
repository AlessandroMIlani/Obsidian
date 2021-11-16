## Grammatiche LL(1)

**Def**
Diciamo che una grammatica G è LL(1) se, per ogni coppia di produzioni distinte A --> $\alpha$ e A --> $\beta$ in P, abbiamo che: $$GUIDA(A --> \alpha)\ \cap\ GUIDA(A --> \beta)=0$$

## Struttura parser ricorsivo
**idea**
Usare la pila del linguaggio di programmazione per ricordare il suffisso della forma sentenziale sinistra da riconoscere
**Elementi chiave**
- Il Parser ha _una procedura per ogni variabile_ della grammatica
- La procedura A nel parser riconosce le stringhe generare da A nella grammatica
- La procedura A usa il simbolo corrente e gli insiemi guida, per scegliere la produzione A -> $\alpha_1$ | $\alpha_2$ | .. |$\alpha_n$ da usare per scrivere A
- Per ogni simbolo X trovato nel corpo della produzione scelta:
	- Se X è un simbolo terminale, il metodo controlla che il simbolo corrente sia proprio X
	- Se X è una variabile, il metodo invoca la procedura di X
>PseudoCode
![[Pasted image 20211110123212.png]]

>Java
![[Pasted image 20211110123715.png]]