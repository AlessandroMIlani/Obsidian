| Nome File    | Descrizione                          |
| ------------ | ------------------------------------ |
| makefile     | file di costruzione                  |
| setting.conf | parametri da decidere all'esecuzione |
| main.c       |                                      |
| nodo.c       |                                      |
| user.c       |                                      |


```mermaid 
	flowchart TD
	
	a(main -> processo manster) --> b(fork -> nodi + user)
	
	
  
```