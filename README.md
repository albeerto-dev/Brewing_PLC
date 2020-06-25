# Brewing_PLC
PLC programmato tramite piattaforma CODESYS e l'utilizzo di Raspberry Pi per la gestione di I/O con l'utilizzo di una HMI accessibile tramite WebServer.

## Obiettivi di sviluppo 
*Codice*
- [ ] Struttura generale delle varibili globali e SFC / LD
- [ ] Implementazione modalità manuale
- [ ] Implementazione modalità automatica
- [ ] Implementazione allarmi
- [ ] Implementazione I/O
- [ ] Implementzaione timer 
- [x] Implementazione PID
- [ ] Implementazione voce MAIN
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
![Immagine 01](https://github.com/albeerto-dev/Brewing_PLC/blob/master/immagine01.png)
Dall'imagine 1 si denota la prima struttura dell'interfaccia HMI che consentirà di gestire la varia attrezzera tramite pannello "Settings..." di visualizare "DATA" di poter usare il controllore in modlaità manule "MAIN" e di poter procedere con una completa cotta con la modalità "START A BREW" che consete di insererire una ricetta tramite file .xml o crearla sul momento.
* Resoconto 22.06.2020
![Immagine 02](https://github.com/albeerto-dev/Brewing_PLC/blob/master/immagine02.png)
Prime prove di struttura codice PID. Procede con complicazioni la gestione dell'impulso basato sui calcoli dell'algoritmo PID. Questa prima versione è basata sul codice in C++ di un precedente progetto personale. La difficolta sta nel tramutare il valore di errore di tipo REAL in un impulso dell'attuatore di una durata consona ed efficacie da applicare secondo una finestra temporale di azione da parte dell'SSR.
* Resoconto 25.06.2020
![Immagine 03](https://github.com/albeerto-dev/Brewing_PLC/blob/master/immagine03.png)
Codice PID ultimato. Tramite prove di simulazione sono riuscito a gestire il valore di output PID.Y in maniera tale da produrre un impulso di una certa lunghezza temporale per l'attivazione dell'SSR. Manca il tuning dei parametri.
