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
I file descrittori, sono dei numeri che identificano univocamente un file nel'OS, e descrivono come deve avvenire l'accesso alla risorsa. I descrittori sempre presenti in un processo sono: 
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
Esistono delle funzioni __wrapper__, che permettono di chiamare altre funzioni o system call.
Per favorire le prestazioni, i passaggi di informazioni avvengono mediante indirizzi.
Le system call, hanno tutte un valore di ritorno, e per convenzione in caso di fallimento è sempre -1. In caso di errore delle system call, possiamo trovare la descrizione dell'errore nell'header file <errno.h>.
- - -
#include <errno.h>

fd = ...
if(fd == -1){
    if(errno == EACCES){
        printf("Errore di accesso");
    }else{
        printf("Altri errori");
    }
}
- - -
Possiamo vedere quale system call viene usata dal processo mediante il comando __strace__.

### Manuale
Per consultare il manuale incorporato nel dispositivo, è possibile utilizzare il comando __man__ da shell. Possiamo usarlo seguito dal nome del comando, o dal numero della pagina a cui vogliamo accedere:
- 1: contiene i comandi utente.
- 2: contiene la documentazione sulle system call.
- 3: contiene la documentazione delle standard library C.
- 4: contiene dettagli sui dispositivi.
- 5: contiene formati di file e convenzioni.

## Filesystem
Vediamo ora alcune system call che ci permettono di lavorare con i file:
- La system call __open__, permette di aprire un file, creandolo se non esiste. In caso di errore restituisce -1, mentre se avviene con successo restituisce un file descriptor, che "punta" al file identificato dal pathname.
- La system call __read__, permette di leggere il contenuto di un file, restituendo -1 in caso di errore, altrimenti il numero di bytes letti.
- La system call __write__, permette di scrivere su un file descriptor, restituendo -1 in caso di errore, altrimenti il numero di bytes scritti.
- La system call __lseek__ permette di muoversi all'interno di un file. Restituisce -1 in caso di errore, altrimenti l'offset corrispondente alla posizione nel file.
- La system call __close__ permette di chiudere un file descriptor aperto. Restituisce -1 o 0.
- La system call __unlink__ permette di rimuovere un link ad un file, e se è l'ultimo rimasto, elimina il file stesso. Restituisce -1 o 0.
- Le system call __stat lstat fstat__ permettono di ricavare informazioni su un file. Restituisce -1 o 0.
- La system call __access__ permette di verificare i permessi di un file. Restituisce -1 se non ha accesso a tutti i permessi.
- Le system call __chmod fchmod__ permetto di cambiare i permessi di un file. Restituisce -1 o 0.
- - -
__nb__: grazie al comando "unmask" andremo a creare file con gli stessi permessi.

__nb__: la read è una call bloccante, ovvero, se i dati non sono disponibili, il kernel la interrompe momentaneamente fino a che non sono disponibili, in modo da non perdere tempo.
- - -

#  10/10/2022
