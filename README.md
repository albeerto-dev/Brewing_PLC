# Fellow Brewer - PLC <img src= "https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/Risorsa%205FELLOW_BREWER_LOGO.png" width="30%" align="right" />
Un sistema automatico per la produzione della birra:
PLC programmato tramite piattaforma CODESYS e l'utilizzo di Raspberry Pi per la gestione di I/O con l'utilizzo di una HMI accessibile tramite WebServer.
Sviluppato da Alberto M. Ramagini

## Obiettivi di sviluppo 
*Codice*
- [x] Struttura generale delle varibili globali e SFC / LD / ST
- [x] Implementazione modalità manuale
- [x] Implementazione modalità automatica
- [ ] Implementazione allarmi
- [x] Implementazione I/O
- [x] Implementzaione timer 
- [x] Implementazione PID
- [x] Implementazione ON/OFF
- [x] Implementazione voce MAIN
- [x] Implementazione voce BREW
- [x] Implementazione voce RECIPE

*Wiring*
- [x] Bozza su breadboard
- [ ] Disegno su PCB
- [ ] Realizzazione PCB
- [ ] Assemblaggio PCB
- [ ] Cablaggio bassa tensione
- [x] Disegno schema circuito bassa tensione
- [ ] Cablaggio alta tensione 
- [x] Disegno schema circuito alta tensione


## Aggiornamenti di sviluppo
* Resoconto 19.06.2020 //<img src= "https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/immagine01.png"/>
Dall'imagine 1 si denota la prima struttura dell'interfaccia HMI che consentirà di gestire la varia attrezzera tramite pannello "Settings..." di visualizare "DATA" di poter usare il controllore in modlaità manule "MAIN" e di poter procedere con una completa cotta con la modalità "START A BREW" che consete di insererire una ricetta tramite file .xml o crearla sul momento.
* Resoconto 22.06.2020 // <img src= "https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/immagine02.png"/>
Prime prove di struttura codice PID. Procede con complicazioni la gestione dell'impulso basato sui calcoli dell'algoritmo PID. Questa prima versione è basata sul codice in C++ di un precedente progetto personale. La difficolta sta nel tramutare il valore di errore di tipo REAL in un impulso dell'attuatore di una durata consona ed efficace da applicare secondo una finestra temporale di azione da parte dell'SSR.
* Resoconto 25.06.2020 //
![Immagine 03](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/immagine03.png)
Codice PID ultimato. Tramite prove di simulazione sono riuscito a gestire il valore di output PID.Y in maniera tale da produrre un impulso di una certa lunghezza temporale per l'attivazione dell'SSR. Manca il tuning dei parametri.
* Resoconto 28.06.2020 //           
![Immagine MAIN](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/mainImage_semi_complete.png)     
Interfaccia MAIN ultimata. Tutti i pulsanti sono stati introdotti. Gli SSR di HLT e BOIL seguono un algoritmo di tipo ON/OFF per il riscaldamento e la tenuta a SET POINT. L'SSR del MASH TUN invece ha la doppia possibilità di eseguire il controllo tramite algoritmo ON/OFF oppure di tipo PID (oppurtunamente tarato) semplicemente premendo il pulsante apposito. I due algoritmi di controllo temperatura sono stati introdotti nel programma tramite FUNCTION BLOCK per avere una maggiore versatilità nel codice. La funzionalità del timer ha come unico scopo la funzione di disattivare l'SSR a fine countdown. Ho implementato un pulsante di EMERGENZA per disattivare tutti gli attuatori contemporaneamente. La struttura del codice è per ora interamente in TESTO STRUTTURATO (ST).
* Resoconto 05.08.2020 //
Ripreso lo sviluppo del codice da circa una settimana dopo la puasa esami e estiva. Dopo svariati tentativi di utilizzo della libreria RecipeMangaer per la gestione delle ricette avevo inizialmente deciso di abbandonarne l'utilizzo. La pessima documentazione la rendeva inutilizzabile, ma da pochissimi giorni CODESYS Italia ha pubblicato su Youtube un video esplicativo dell'utilizzo della libreria. Al momento sembra essere il tutorial più completo ed efficace dato che le uniche risorse online sono un paio di domande sui forum dedicati e altri due video su Youtube, di cui uno in russo (incomprensibile) e uno in inglese totalmente inutile e inefficace all'apprendimento. Ripongo estrema fiducia nel risucire ad implementare la gestione delle ricette (salvataggio/caricamento/scrittura/utilizzo) in un arco di tempo relativamente breve. Ad oggi la parte complessa di implementazione risulta essere lo storage, il caricamento e la lettura dei file in .txtrecipe .  
* Resoconto 15.10.2020 //
![Immagione ricette implementate](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/Implentazoine_ricette.png)
Finalmente sono arrivato ad un punto di svolta. Da come si vede nell'immagine, sono riuscito a implementare la scrittura e lo storage delle ricette. La lista di sinistra indica i nomi delle ricette create e disponibili, il riquadro centrale fa visualizzare i file interni alla cartella dove vengono salvate le ricette con i relativi nomi. Sotto alla finestra di navigazione è presente l'interfaccia di scrittura delle varibaili da registrare nella ricetta/file da salvare o creare. Sulla destra si trovano una moltitudine di funzionalità a pulsante che corrispondono ad alcuni dei metodi che vengono forniti dalla libreria RecipeManager che ho deciso di implementare. Probabilmente alcune di queste funzionalità non sono strettamente utili e in futuro qualcuna sarà probabilmente eliminata. Il prossimo passo consiste nell'implementare la modalità automatica che funziona se e solo se si seleziona un file RICETTA precedentemento creato; dopo aver selezionato il file, il programma salva le varibili in una struct temporanea in cui si trovano i parametri che seguirà il processo durante la birrificazione
* Resoconto 16.10.2020 //
![Immagine inizio sviluppo modalità automatica](https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/Progresso_automatic_mode.png)
Risolto il problema di lettura al momento della selezione della ricetta. Ho appena iniziato lo sviluppo della modalità automatica e si possono già ben vedere tutti i pre-requisiti da soddisfare prima di comiciare la cotta : caricamento dell'acqua e selezione della ricetta (che se mal selezionata genera errore; la selezione avviene tramite scrittura del nome della ricetta nell'apposito riquadro). Ho pensato anche di inserire una progressbar per indicare lo status temporale della cotta e ho avuto l'idea di implementare una modalità semi-automatica che può essere attivata e disattivata a piacimento durante la cotta.
* Resoconto 19.10.2020 // <img src="https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/Lista_POU_FB_FUN.png" align="right"/>
Oggi è una buona giornata di commit. Sono stati raggiunti ottimi risultati. Dopo aver recentemente introdotto la lettura delle ricette, ho ora completato l'implementazione della parte interamente automatica. Il meccanismo di utilizzo è come segue: come prima cosa si spuntano le checkbox di verifica di inserimento acqua nelle pentole di impianto. Dopo ciò è possibile selezionare la ricetta, precedentemente creata tramite l'apposito menu "RECIPE". Avvenuto il salvataggio nelle variabili globali, comincia il riscaldamento dell'acqua in entrambe le pentole (se si fa sparge, altrimenti viene riscaldata solo quella di mash). Un avviso indicherà l'inserimento dei grani per iniziare l'ammostamento e dopo averli inseriti si confermerà tramite slider che darà il via a tutti gli step del mash con relativo tempo e temperatura. Terminato il mash si può procedere con lo sparge a corretta temperatura grazie all'azione paralella durante l'azione di ammostamento. Una volta confermato l'inizio di sparge tramite slider, il timer parte. Terminato il timer si richiede all'operatore di confemrare il trasferimento del mosto nel tino di bollitura tramite slider. Una volta confermato si attiva l'SSR del tino di bollitura per portare il  mosto ad ebollizione. Raggiunti circa i 96°C si chiede conferma all'operatore per l'inizio della bollitura tramite slider. Una volta confermato, si attiva il timer di controllo durata della bollitura e in contemporanea una spia luminosa (e sonora in futuro) che avvisa l'operatore di confermare la gettata di luppolo. Terminata la bollitura si disattiva l'SSR della termoresistenza riscaldante e si attiva il relay dell'elettovalvola di raffreddamento o per arrivare a temperatura di hopstand (se richiesto da ricetta) oppure per raffredare il mosto a temperatura di inoculo del lievito. La giornata di cotta è terminata. 
Nell'immagine di destra si possono osservare tutte le POU e le FB del codice, alcune sono ridondanti, altre no, altre saranno eliminate pechè non utili, ma in linea di massima dovrebbero essere quelle definitive. Inserisco anche un'immagine della HMI dedicata alla modalità automatica abbastanza semplice ed essenziale e che non crei confusione all'operatore. All'interno della cartella images ho allegato anche il DEBUG visivo di una simulazione di cotta tramite valori forzatamente scritti all'interno del PLC per verificare il corretto funzionamento.
* Resoconto 24.10.2020 //
Il progetto cambia ufficialmente nome e diventa "FELLOW BREWER" che dall'inglese può essere tradotto con "collega birraio". Ho scelto questo nome perchè risalta l'importanza di un "collega" durante un faticoso e complesso processo produttivo come quello della produzione del mosto di birra. Collega perchè aiuta a portare a termine i compiti di produzione nel modo più efficiente possibile, riducendo i rischi e aumentado la replicabilità del processo. FELLOW BREWER è un collega/assistente a tutti gli effetti.
Questo resoconto è l'ultimo riguardante lo sviluppo del codice: lo sviluppo software è terminato (salvo eventi eccezionali per aggiungere funzionalità non ancora pensate).
Tutti i bug sono stati risolti e tutti tutte le funzionalità sono state implementate correttamente. Il cuore del sistema è chiaramente la funzionalità BREW che consente di produrre un batch in modalità automatica con qualche accortezza da parte dell'operatore. Quest'ultimo dovrà rispondere al PLC durante la cotta così da verificare se alcuni passaggi siano stati effettuati e se si possa procedere allo step successivo. Seguiranno poi spiegazioni più dettagliate alla stesura della tesi o anche in un video spiegazione del codice scritto (ampiamente commentato). Questa è l'HMI:
<img src= "https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/HMI%20definitiva/HMI_main.png" width="100%"  /> <img src= "https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/HMI%20definitiva/HMI_recipes.png" width="45%" /> <img src= "https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/HMI%20definitiva/HMI_brew1.png" width="45%" /> <img src= "https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/HMI%20definitiva/HMI_brew2.png" width="45%" /> <img src= "https://github.com/albeerto-dev/Brewing_PLC/blob/master/Images/HMI%20definitiva/HMI_brew3.png" width="45%"  />
* Resonto 27.10.2020 //
Gli schemi elettrici sono stati disegnati tramite KiCAD e completati al meglio. Potrebbero esserci delle modifiche in futuro ma comunque il grosso è stato realizzato. Qui sotto compaiono 2 schemi elttrici: uno approfondisce i collegamenti 5VDC dei PIN della Raspberry Pi con qualche aggiunta di componenti in 220VAC e 12VDC per chiarezza e completezza di progetto; l'altro invece approfondisce il circuito in 220VAC e a 12VDC sfruttati dai segnali della Rappberry Pi. Manca un terzo circuito dove i collegamenti agli attuatori e sensori sono "eliminati" per fare posto alle morsettiere di collegamento che saranno utili sia nella progettazzione della "HAT" (il PCB) sia nel cablaggio del protipo finale.
<img src= https://github.com/albeerto-dev/Fellow-Brewer/blob/master/Electric_schemes/schemaAC_DC_2.png  />
<img src= https://github.com/albeerto-dev/Fellow-Brewer/blob/master/Electric_schemes/schema_RaspberryPi.png />
