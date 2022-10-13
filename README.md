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

- - -
nb: le variabili globali sono utili, ma vanno usate solo se necessario, in quanto sono sempre disponibili, ma occupano sempre memoria.
- -  -
36:19