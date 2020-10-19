# Brewing_PLC
PLC programmato tramite piattaforma CODESYS e l'utilizzo di Raspberry Pi per la gestione di I/O con l'utilizzo di una HMI accessibile tramite WebServer.

## Obiettivi di sviluppo 
*Codice*
- [x] Struttura generale delle varibili globali e SFC / LD / ST
- [x] Implementazione modalità manuale
- [ ] Implementazione modalità automatica
- [ ] Implementazione allarmi
- [ ] Implementazione I/O
- [x] Implementzaione timer 
- [x] Implementazione PID
- [x] Implementazione voce MAIN
- [ ] Implementazione voce START A BREW
- [ ] Implementazione voce SETTINGS & CONFIGURATION
- [ ] Implementazione voce DATA

*Wiring*
- [ ] Bozza su breadboard
- [ ] Disegno su PCB
- [ ] Realizzazione PCB
- [ ] Assemblaggio PCB
- [ ] Cablaggio bassa tensione
- [ ] Disegno schema circuito bassa tensione
- [ ] Cablaggio alta tensione 
- [ ] Disegno schema circuito alta tensione


## Aggiornamenti di sviluppo
* Resoconto 19.06.2020
![Immagine 01](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/immagine01.png)
Dall'imagine 1 si denota la prima struttura dell'interfaccia HMI che consentirà di gestire la varia attrezzera tramite pannello "Settings..." di visualizare "DATA" di poter usare il controllore in modlaità manule "MAIN" e di poter procedere con una completa cotta con la modalità "START A BREW" che consete di insererire una ricetta tramite file .xml o crearla sul momento.
* Resoconto 22.06.2020
![Immagine 02](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/immagine02.png)
Prime prove di struttura codice PID. Procede con complicazioni la gestione dell'impulso basato sui calcoli dell'algoritmo PID. Questa prima versione è basata sul codice in C++ di un precedente progetto personale. La difficolta sta nel tramutare il valore di errore di tipo REAL in un impulso dell'attuatore di una durata consona ed efficacie da applicare secondo una finestra temporale di azione da parte dell'SSR.
* Resoconto 25.06.2020
![Immagine 03](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/immagine03.png)
Codice PID ultimato. Tramite prove di simulazione sono riuscito a gestire il valore di output PID.Y in maniera tale da produrre un impulso di una certa lunghezza temporale per l'attivazione dell'SSR. Manca il tuning dei parametri.
* Resoconto 28.06.2020            
![Immagine MAIN](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/mainImage_semi_complete.png)     
Interfaccia MAIN ultimata. Tutti i pulsanti sono stati introdotti. Gli SSR di HLT e BOIL seguono un algoritmo di tipo ON/OFF per il riscaldamento e la tenuta a SET POINT. L'SSR del MASH TUN invece ha la doppia possibilità di eseguire il controllo tramite algoritmo ON/OFF oppure di tipo PID (oppurtunamente tarato) semplicemente premendo il pulsante apposito. I due algoritmi di controllo temperatura sono stati introdotti nel programma tramite FUNCTION BLOCK per avere una maggiore versatilità nel codice. La funzionalità del timer ha come unico scopo la funzione di disattivare l'SSR a fine countdown. Ho implementato un pulsante di EMERGENZA per disattivare tutti gli attuatori contemporaneamente. La struttura del codice è per ora interamente in TESTO STRUTTURATO (ST).
* Resoconto 05.08.2020 //
Ripreso lo sviluppo del codice da circa una settimana dopo la puasa esami e estiva. Dopo svariati tentativi di utilizzo della libreria RecipeMangaer per la gestione delle ricette avevo inizialmente deciso di abbandonarne l'utilizzo. La pessima documentazione la rendeva inutilizzabile, ma da pochissimi giorni CODESYS Italia ha pubblicato su Youtube un video esplicativo dell'utilizzo della libreria. Al momento sembra essere il tutorial più completo ed efficace dato che le uniche risorse online sono un paio di domande sui forum dedicati e altri due video su Youtube, di cui uno in russo (incomprensibile) e uno in inglese totalmente inutile e inefficace all'apprendimento. Ripongo estrema fiducia nel risucire ad implementare la gestione delle ricette (salvataggio/caricamento/scrittura/utilizzo) in un arco di tempo relativamente breve. Ad oggi la parte complessa di implementazione risulta essere lo storage, il caricamento e la lettura dei file in .txtrecipe .  
* Resoconto 15.10.2020 
![Immagione ricette implementate](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/Implentazoine_ricette.png)
Finalmente sono arrivato ad un punto di svolta. Da come si vede nell'immagine, sono riuscito a implementare la scrittura e lo storage delle ricette. La lista di sinistra indica i nomi delle ricette create e disponibili, il riquadro centrale fa visualizzare i file interni alla cartella dove vengono salvate le ricette con i relativi nomi. Sotto alla finestra di navigazione è presente l'interfaccio di scrittura delle varibaili da registrare nella ricetta/file da salvare o creare. Sulla destra si trovano una moltitudine di funzionalità a pulsante che corrispondono ad alcuni dei metodi che vengono forniti dalla libreria RecipeManager che ho deciso di implementare. Probabilmente alcune di queste funzionalità non sono strettamente utili e in futuro qualcuna sarà probabilmente eliminata. Il prossimo passo consiste nell'implementare la modalità automatica che funziona se e solo se si seleziona un file RICETTA precedentemento creato; dopo aver selezionato il file il programma salva le varibili in una struct temporanea in cui si trovano i parametri che seguirà il processo durante la birrificazione
* Resocotno 16.10.2020
![Immagine inizio sviluppo modalità automatica](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/Progresso_automatic_mode.png)
Risolto il problema di lettura al momento della selezione della ricetta. Ho appena iniziato lo sviluppo della modalità automatica e si possono già ben vedere tutti i pre-requisiti da soddisfare prima di comiciare la cotta : caricamento dell'acqua e selezione della ricetta (che se mal selezionata genera errore; la selezione avviene tramite scrittura del nome della ricetta nell'apposito riquadro). Ho pensato anche di inserire una progressbar per indicare lo status temporale della cotta e ho avuto l'idea di implementare una modalità semi-automatica che può essere attivata e disattivata a piacimento durante la cotta.

