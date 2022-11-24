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

# Ultime generazioni 17/10/2022
## Interrupt
Per poter sovrapporre la CPU alla gestione dell I/O, sono stati introdotti gli __interrupt__, che permetteva di distinguere l'elaborazione dalle fasi di input e output. Grazie agli interrupt, durante le fasi di I/O, la CPU si occupava di altre processi, e questo processo è detto __polling__.

### DMA
In alcuni casi, la CPU verrebbe interrotta da una grande sequenza di interrupt intermedi, non veramente alla CPU, e quindi viene usato un meccanismo asincrono detto DMA, che raccoglie tutti gli interrupt intermedi (fino all'ultimo interrupt), e a quel punto la CPU verrà interrotta.
Nel momento in cui la CPU viene interrotta, salta ad una locazione predefinita dall'interrupt dove troverà un codice da eseguire, per poi tornare ad eseguire quello che stava facendo prima dell'interrupt.

### Spooling
Considerando che la CPU è moltpo più veloce ad elaborare, di quanto i dati ci mettono ad essere letti, ci si trova davanti ancora a dello spreco di tempo della CPU. Se il "buffering" permetteva di leggere i dati che sarebbero poi stati utili nello stesso preocesso, grazie allo "spooling" era possibile iniziare l'acquisizione di dati per altri processi. Si passa così da nastri magnetici a __dischi magnetici__ e quindi a memorie ad __accesso casuale__.

## Terza generazione
Nasce il concetto di __multiprogrammazione__, ovvero la possibilità di avere in memoria più programmi caricati, alternandoli nell'esecuizione della CPU. Nel momento in cui più programmi in memoria si contengono la CPU, è l'OS che decide le priorità tra i vari processi, una così detta "schedule". Cambia anche il modo di approcciarsi al sistema, infatti l'utente non è più tanto interessato a quando si finisce di utilizzarlo, ma al tempo che impiega a rispondere.

### Time sharing
Data la crescente necessità di utilizzare più processi alla volta, i processi iniziano a dividersi la CPU in base a quanti di tempo, dando l'impressione che i comandi vengano eseguiti in parallelo. Con il timesharing, nascono i sistemi "moderni" come tastiera, monitor, e del file system.

Ora che può programmi possono essere eseguiti contemporaneamente, sarà anche possibile che un programma influenzi un'altro. Quindi è necessario proteggere alcune delle componenti del sistema, rispetto a:
- I/O: un programma non può utilizzare direttamente una periferica, ma attraverso il sistema operativo. Qui si crea la distinzione tra modalità user e modalità kernel (può accedere alle risorse hardware). Quindi quando abbiamo bisogno di usare una risorsa hardware, andiamo ad incaricare l'OS attraverso le __system call__.
- Memoria: ad ogni processo viene data della memoria, da cui non può uscire. L'OS interromperà eventuali errori di accesso alla memoria (es. segmentation fault).
- CPU: l'OS deve essere in grado di mantenere il controllo sul sistema, impedendo che alcuni processi uscissero dal controllo della CPU.

### Quarta generazione
La quarta generazione si spinge fino ad oggi, che abbiamo a disposizione O.S di vari tipi e capacità:
- PC e workstation.
- di rete.
- distribuiti.
- real-time: rispetta i vincoli imposti.
- embedded: specializzati per uno o più lavori particolari.

- - -
__nb__: DMA (direct memory access).

___Esempio__: se avviene la scrittura in memoria di 4 Gbyte, in blocchi da 10 Kbyte, la DMA riceve tutti gli interrupt per ogni blocco, alla CPU arriverà solo l'interrupt finale, quando tutti i 4 Gbyte saranno trasferiti.
- - -

## Componenti del sistema operativo
Vediamo di cosa si compone, a livello concettuale l'OS:
- gestione dei processi: sappiamo che un sistema operativo deve far eseguire i programmi nel miglior e semplice modo possibile. Partendo dal codice contenuto nella memoria secondaria, ovvero il __programma__, il sistema operativo genera i __processi__ ovvero delle istanze del programma, e gli assegna delle risorse, la prima è la memoria primaria, su cui eseguire il processo.
- gestione della memoria primaria: la prima risorsa di cui ho bisogno quando ho creato un processo, è la memoria RAM, ed è dove il processo si troverà. L'OS sarà il responsabile di assegnare la memoria ai processi, decidendo quali processi caricare nel momento in cui esiste dello spazio disponibile.
- gestione della memoria secondaria: il programma invece, starà nella memoria di massa. L'OS si occuperà di ottimizzare la memoria secondaria, oltre alla precedenza delle operazioni di lettura e scrittura.
- gestione dell'I/O: permette di semplificare le periferiche di input e output, che permette a chi li utilizza di non dover conoscerne le componenti e il reale funzionamento.
- gestione dei file: il sistema operativo deve creare una struttura in cui contenere i dati.
- protezione: garantisce l'accesso alle varie componenti solo a chi è autorizzato.
- rete: l'OS deve preoccuparsi di mettere in correlazione elementi diversi, rendendo un sistema composto un sistema unico.
- interprete dei comandi: interfaccia tra utente e sistema.

### System call
Tutte queste mansioni potranno essere eseguite grazie alle system call. All'interno di una system call saranno presenti dei parametri, che vanno a specificare all'OS cosa deve fare. I parametri possono essere passati tramite registri di memoria, stack e tabella di memoria. Con il metodo "tabella di memoria" il parametro sarà l'indirizzo in cui si trovano i dati da passare.

# Architettura dell'OS 24/11/2022
## Struttura semplice
Inizialmente l'OS era un sistema monolitico, dove tutte le componenti erano allo stesso livello, e tutti potevano comunicare con tutti. Con l'aumento della complessità dell'OS e la necessità di utilizzarlo su hardware differenti, si è iniziato a strutturarne i livelli gerarchicamente. In origine UNIX presentava la seguente struttura:
1. utente.
2. shell e comandi, compilatori e librerie di sistema.
3. interfaccia systemcall verso il kernel.
4. kernel: gestione I/O, gestione del filesystem, scheduling della CPU, gestione della memoria primaria e virtuale.
5. interfaccia del kernel verso l'hardware (device driver).
6. periferiche.
Grazie ad un sistema a livelli, è semplificata la manutenzione e in particolare individuare eventuali errori. D'altro canto, è più difficile da programmare e meno efficiente (overhead con le system call), questo porterà col tempo ad abbandonare questo approccio.
Questo approccio aveva portato alla creazione di __virtual machine__, ovvero moltiplicare l'hardware grazie ad un "virtual machine layer". Nasce dall'esigenza di avere più calcolatori, ma era poco vantaggioso.
La struttura che utiliziamo oggi, presenta le varie componenti disposte, non a livelli gerarchici, ma in __parallelo__.

## Gestione dei processi
Il processo è l'istanza di un programma, e risiede nella memoria primaria. In un sistema con time-sharing, in esecuzione abbiamo più proccessi che evolvono concorrentemente, competendo per le varie risorse, e il compito dell'OS è gestire più processi. La prima risorsa di cui un processo ha bisogno è la memoria appunto, dove verrà caricato il codice del programma. Successivamente, ci sono i dati che saranno richiesti dal codice del processo. Seguono le variabili, globali, automatiche e dinamiche, che si troveranno in zone diverse della memoria. Sempre nella memoria, serve anche il __program counter__, necessario per un sistema dotato di "time sharing", e non solo. La sezione di memoria destinata al processo, conterrà la così detta __immagine del processo__:
- dati (variabili statiche e globali, non inizializzate).
- stack (variabili automatiche).
- heap (variabili dinamiche).
- istruzione (codice).
- attributi (id, stato del processo, controllo).

```C
int test; // dati globali
int main(int argc, char *argsv[]){
    int n; // stack
    a = (char*) malloc (...); // heap
    n = func(n);
}
int func(int x){
    return x+1;
}
```
### Attributi
L'insieme degli attributi è anche detto __process control block__ e va a rappresentare il processo:
- stato del processo.
- program counter.
- valori dei registri.
- informazioni sulla memoria.
- informazioni sull'I/O.
- informazioni sull'utilizzo della CPU.
- scheduling.

### Stato del processo
Mostra l'evoluzione del processo, lo schema base degli stati è il seguente:
- nuovo: viene generato ed introdotto nel sistema.
- non in esecuzione: processo appena creato e mai stato in esecuzione. Potrebbe essere anche stato messo in pausa, perchè terminato il quanto di tempo, o perchè sta aspettando la risposta ad una system call.
- in esecuzione: la CPU sta eseguendo il processo. Ovviamente solo un processo può stare in questo stato, non più contemporaneamente,
- finito: il processo ha terminato la sua esecuizione, ed è stati quindi eliminato (e la memoria liberata).

Lo stato di non esecuzione può essere di viso in 2 stati, quello di __pronto__ che aspetta gli venga destinata la CPU, o in __attesa__ appunto di una risorsa hardware o di un evento. Dallo stato di "pronto" può essere terminato, ad esempio in caso di deadlock.

### Scheduling
A decidere gli stati del processo è appunto l'OS: lo scheduler seleziona i processi da mandare in esecuzione, ma è il __dispatcher__ che esegue l'effettivo __context switch__. I processi nello stato di "pronto" vengono inseriti in una struttura dati detta banalmente coda, e aspettano il proprio tempo per la CPU. Durante l'operazione di dispatch, viene salvato il PCB del processo uscente, mentre carico quello del processo entrante.

### Creazione di un processo
Un processo durante la propria vita svolge una serie di operazioni, tra cui la creazione di un processo: un processo padre crea un processo figlio, mediante due modalità, ovvero __spartizione__ e __condivisione__, mediante l'operazione di _fork_. In questo caso il figlio sarà un duplicato esatto del padre, mentre sarà un programma diverso con l'operazione _exec_. Grazie all'operazione _wait_ l'esecuzione tra padre e figlio sarà sincrona.
```C
#include <strio.h>
void main(int argc, char *argv[]){
    int pid;
    pid = fork();
    if(pid<0){
        fprintf(stderr, "errore");
        exit(-1);
    } else if(pid == 0){
        execlp("/bin/ls","ls",NULL);
    } else{
        wait(NULL);
        printf("Figlio ha terminato.");
        exit(0);
    }
}
```

- - -
__Esempio__: MS-DOS era strutturato su 3 liveli, programmi di sistema, MS-DOS device driver, ROM BIOS device driver.

__nb__: il processo negli stati di pronto e attesa, viene detto "in memoria".

__nb__: la coda dei processi nello stato di pronto è detta "ready queue".

__nb__: molto importante è lavorare sullo scheduling, invece di aumentare un quanto di tempo.
- - -