```mermaid
flowchart TD
	r --> b(fork 1)
	b --> c(fork 2)
	a(main.sh) --> r(check valori in setting.conf)
	b --> d(exec node.sh, n+con)
	c --> e(exec user.sh, n)
	f(Librerie-varie.h) -.-> a
```