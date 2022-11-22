# Introduzione 10/10/2022
## Sistema operativo
L'interazione tra user e OS sono continue, ogni volta che sfruttiamo l'interfaccia di un dispositivo. Anche le applicazione comunicano costantemente con l'OS attraverso le systemcall. Il __sistema operativo__ è un insieme di programmi che svolgono il ruolo di intermediario tra hardware e utente, rendendo facile l'utilizzo del calcolatore. Il suo compito è quello di ottimizzare le risorse, gestirle evitando conflitti, non complicandone l'utilizzo per l'utente.
- user
- applicazione
- os
- hardware
L'OS può essere visto in due modi: un __gestore di risorse__, che possono essere sia software che hardware, e un __programma di controllo__ che controlla l'esecuzione dei programmi, e come i processi interagiscono tra loro e con il calcolatore, soprattuto in momenti critici.

## Cenno storico
L'informatica parte dal bisogno di concretizzare e automtizzare calcoli e concetti. I calcolatori possono essere divisi in 4 generazioni:
1. macchine di enormi dimensioni, per lo più meccaniche, non provviste di sistema operativo. Vede la diffusione delle prime periferiche, che permettevano lo scambio di informazioni mediante schede perforate, la cui gestione portò allo sviluppo di __device driver__, un primo accenno di sistema operativo. Inizia lo sviluppo di software, librerie di funzioni comuni e quindi compilatori, linker e loader. Presentava una scarsa efficienza.
2. i meccanici calcolatori a valvole vengono sostiuiti da quelli elettronici, che presentavano dei __transistor__. Qui si crea la distinzione tra operatore, che si occupa del suo funzionamento, e programmatori. Questo permette la parallizzazione tra gli utenti (programmatori), eliminando i tempi morti nell'utilizzo del processore. Nascerà l'OS che andrà a sostituire l'operatore, che permetterà di gestire i programmi in sequenza. Mentre le scede dei dati e dei programmi venivano caricate e scaricate, il processore non veniva utilizzato, quindi sono ancora presenti tempi morti. Vengono quindi sviluppati dei sistemi dedicati, che lavorano con __operazioni offline__ per caricare le schede sotto forma di nastri magnetici.