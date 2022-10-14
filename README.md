# Introduzione 10/10/2022
## Processi
Parliamo di __programma__ come un file binario contenente un insieme di istruzioni e informazioni, che interagisce con il sistema operativo, mentre il __processo__ è l'istanza di un programma. Il programma è statico, mentre il processo è dinamico.
L'OS lavora in modo che i vari processi non entrino in conflitto tra di loro. Ogni processo verrà visto dal Kernel come:
- spazio di memoria che contiene il programma.
- delle variabili usate dal programma.
- delle strutture di dati, contenenti informazioni sul processo.

## Memory Layout
Quando un processo viene creato, gli viene destinata della memoria, che segue il seguente layout:
- codice del programma (read only).
- dati statici e globali inizializzati.
- dati statici e globali non inizializzati.
- heap (memoria dinamica).
- stack (dinamico), destinato alle funzioni al momento attive.
Quando il processo termina, la memoria destinata e allocata viene rilasciata.

- - -
__nb__: le variabili globali sono utili, ma vanno usate solo se necessario, in quanto sono sempre disponibili, ma occupano sempre memoria.
- -  -
## Descrittori
I file descrittori, sono dei numeri che identificano univocamente un file nel'OS, e descrivono come deve avvenire l'accesso alla risorsa. I descrittori semrpe presenti in un processo sono: 
- standard input (0): STDIN_FILENO
- standard output (1): STDOUT_FILENO
- standard error (2): STDERR_FILENO

## System call
### Architettura dell'OS
L'architettura del sistema operativo, può essere semplificata con il seguente schema: le applicazioni che noi utilizziamo girano nello __user space__, e vengono messe in comunicazione con il Kernel mediante delle system call. Il Kernel a sua volta, può se necessario comunicare con i dispositivi hardware, mediante dei driver. Le system call, i driver e lo stesso Kernel fanno parte del __kernel space__.

- - -
__Esempio__: un applicazione necessita un input da tastiera, viene messa in "pausa" (interrupt), manda la richiesta al Kernel mediante system call, che attraverso i driver, permette di utilizzare la tastiera.

__nb__: dal punto di vista di un programmatore, chiamare una system call, è come chiamare una funzione in C.
- - -

### Esecuzione della system call
57:33
