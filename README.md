Lotteria - Java Project

Scopo del Progetto:
Il progetto simula un sistema di lotteria in cui un insieme di giocatori seleziona numeri e il sistema determina i vincitori. Ogni giocatore può selezionare numeri e, se questi coincidono con i numeri estratti casualmente dal sistema, vengono dichiarati vincitori. La lotteria termina quando ci sono tre vincitori.

Classi Principali
1. Estrazione
   - Questa classe gestisce il processo di estrazione dei numeri e la verifica dei vincitori. È un'estensione della classe 'Thread' e gestisce la lotteria parallelamente all'esecuzione dei giocatori.
   - Metodo: 'verifica(int numero, int idGiocatore)'
     Questo metodo ha lo scopo di controllare se il numero scelto dal giocatore è presente nella matrice dei numeri estratti. Se sì, il giocatore viene aggiunto alla lista dei vincitori. Se sono già stati determinati tre vincitori, il metodo impedisce che altri giocatori vincano.
     'java
     public void verifica(int numero, int idGiocatore) {
         if (vcont >= 3) {
             System.out.println("Il giocatore con ID: " + idGiocatore + " non puo' vincere piu' premi");
             return;
         }
         for (int i = 0; i < n; i++) {
             for (int j = 0; j < n; j++) {
                 if (matrice[i][j] == numero && !premiati[i][j]) {
                     premiati[i][j] = true;
                     vincitori[vcont] = idGiocatore;
                     vcont++;
                     System.out.println("Il giocatore con id: " + idGiocatore + " ha scelto il numero vincente: " + numero);
                     return;
                 }
             }
         }
     }
     '

2. Giocatore
   - Questa classe rappresenta i giocatori della lotteria. Ogni giocatre ha un ID univoco e un nome, e può partecipare alla lotteria selezionando un numero casuale.
   - Ogni giocatore è eseguito come un thread, simulado la selezione simultanea dei numeri.

3. Lotteria
   - Questa classe contiene il metodo `main` del progetto e coordina l'esecuzione del gioco. Inizializza l'estrazione e i thread per i vari giocatori, aspettando che ogni thread finisca prima di annunciare i vincitori.

Librerie:
Il progetto utilizza le seguenti librerie standard di Java:
- 'java.util.Random': utilizzato per generare numeri casuali per l'estrazione.
- 'java.util.logging': utilizzato per loggare eventuali errori o eventi durante l'esecuzione.

Scenari Alternativi e Gestione degli Errori
- Se un giocatore tenta di vincere un premio ma sono già stati dichiarati tre vincitori, il messaggio "Il giocatore con ID: X non può vincere più premi" viene stampato e il metodo termina.
- Il progetto è configurato per evitare che più di tre vincitori vengano selezionati, garantendo che l'esecuzione continui correttamente anche se più giocatori provano a vincere dopo che i tre premi sono stati assegnati.

Commento sull'Esecuzione
L'esecuzione del programma segue i seguenti passi:
1. Viene avviata l'estrazione dei numeri casuali.
2. I giocatori (rappresentati come thread) iniziano a partecipare e selezionano i numeri.
3. Dopo che ogni giocatore ha scelto il proprio numero, il sistema determina se il numero è vincente.
4. Una volta determinati tre vincitori, l'estrazione termina e i vincitori vengono annunciati.

Al termine dell'esecuzione, i nomi dei tre vincitori vengono stampati a schermo.