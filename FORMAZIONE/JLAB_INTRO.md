## FORMAZIONE: JupyterLab Intro
*Appunti per il gruppo di studio IPASS sul Machine Learning*

# Andrea Ribuoli: andrea.ribuoli@yahoo.com

# ItPAss, Italian Power Association: www.itpass.org

Traccia per la sessione introduttiva a **JupyterLab**

### Premessa

Innanzi tutto esitono già tutorial sull'uso di JupyterLab (ad esempio [Jupyter Lab Tutorial](https://www.youtube.com/watch?v=7wfPqAyYADY)) quindi lo scopo di questo documento è esclusivamente accompagnare il Webinar che verrà programmato da **FAQ400** a breve.

Alcuni cenni *storici* saranno utili e possono trovare un approfondimento in questo saggio introduttivo: [Introduction to Jupyter Notebooks](https://programminghistorian.org/en/lessons/jupyter-notebooks). 

### Interfaccia grafica

**JupyterLab** costituisce la ultima generazione nella evoluzione del **Progetto Jupyter**. Offre i componenti base dello *Jupyter Notebook* classico (notebook, terminale, editor di testi, browser dei documenti, eccetera) in una interfaccia nuova, potente e flessibile.

I tradizionali progetti Jupyter Notebook sono ospitati come oggetti speciali al pari di altri oggetti speciali: la lista dei quali è in continua espansione grazie alla architettura aperta e al contributo di terze parti.

Di fatto si tratta di un IDE per web. 

![IDE](JupyterLabFace.png)

Ne studiamo prima gli aspetti standard e poi le possibilità di integrazione offerte verso il mondo IBM i.

## Utilizzo standard

SESSIONE INTERATTIVA

[Jupyter Lab on-air](http://gesis400:14143/lab?)

È interessante osservare come la navigazione all'interno dei Notebook vada a braccetto con l'uso preferenziale della tastiera: la **keyboard** torna ad essere la via preferenziale per il conseguimento della produttività.

Vediamo innanzitutto dove reperire in autonomia informazioni sull'uso dei comandi. Sulla sinistra troviamo una lista di icone (sidebar verticale sinistra *"collapsible"*). Un click su una ciascuna di esse apre una sezione diversa. Un successivo click produce la contrazione della espansione originata all'apertura.
Molto banalmente questo conduce al aumentare l'area utile per visualizzare la pagina coi lavori aperti (*Work Area*).

Abbiamo così:

* un **File browser** del percorso dell'IFS a cui l'avvio del servizio è stato ancorato
* un monitor dei **Running Terminals and Kernels** che mostra lo stato dei sotto-lavori attivati (terminali, notebook kernel)
* una interfaccia per eseguire **Commands** (*New Console*, *New Launcher* e tutti i sotto-comandi, raggruppati per sezioni, comprensivi delle abbreviazioni da tastiera -vedremo in particolare quelle per l'uso degli *Jupyter Notebook*-)
* un **Property Inspector** per i Notebook
* una lista con le **Open Tabs** ed infine
* un **Extension Manager** che ci apre ad un modo di altre applicazioni installabili

### Notebook

# &#x238B; .vs. &#x23CE;
I tasti **esc** e **return** alternano tra *Command Mode* e *Edit Mode*

# y .vs. m .vs. r
Quando siamo in *Command Mode*, i tasti **y**, **m** e **r** modificano il tipo di cella (*Code*, *Markdown* e *Raw* rispettivamente) 

# a .vs. b
Quando siamo in *Command Mode*, i tasti **a** e **b** inseriscono una cella nuova rispettivamente prima (**A**bove) o dopo (**B**elow) 

# a .vs. b
Quando siamo in *Command Mode*, i tasti **a** e **b** inseriscono una cella nuova rispettivamente prima (**A**bove) o dopo (**B**elow) 

# shift + &#x23CE; .vs. ctrl + &#x23CE; .vs. opt + &#x23CE;
Quando siamo in *Command Mode*, tutte e tre le combinazioni **eseguono** il contenuto delle celle selezionate (se *Code* interviene l'interprete Python; se *Markdown* si ha il rendering grafico). Con lo *shift* passo alla prossima cella (eventualmente creandone una se sono alla fine), con il *ctrl* resto nella stessa, con *opt* inserisco una nuova cella (sempre di tipo *Code*).

# c &amp; v .vs. x
*Copy* and *Paste* (vale anche per selezione multipla). Il *paste* può essere ripetuto.
Con **x** si effettua un *Cat* che può essere seguito dal *Paste*

# z
*Undo* (ripetibile: recupera gli stati precedenti a ritroso)

# dd
*Delete*
### &#x2325;

# shift + k .vs. shift + j
Estende la selezione verso l'*alto* o il *basso* (eventualmente riducendo: l'ancoraggio è la cella corrente)

# shift + m
*Merge* selected cells

## Utilizzo specifico per IBM i 


Potrà sembrare banale ma la prima cosa che appare ovvia a chiunque si sia confrontato con il mondo Open Source in ambito IBM i è che il **Terminal** offerto da JupyterLab è *eccezionale*. Risolve molte complessità all'utente finale supportando Unicode, le *Unix* pipe, il tunneling via WebSocket. 

La impossibilità di supportare (ad oggi) **Jupyter Hub** frena gli entusiasmi per una adozione più estesa, ma per chi sviluppa è sicuramente una manna.

Partiamo quindi da qui.

Il panel standard con cui si avvia Jupyter Lab è il **Launcher**. In Inglese, *to launch* significa *avviare* quindi da questo pannello si avviano i diversi programmi che compongono l'IDE di Jupyter Lab.

Icone giganti rappresentano i diversi programmi: queste sono organizzate in tre sezioni/raggruppamenti:

* Notebook
* Console
* Other

È nella terza sezione che troviamo **Terminal**.

![IDE](JupyterLabTerminal.png)

Ad ogni pressione del bottone viene avviata una nuova sessione di terminale che utilizzerà un panel dedicato. Avremo così Terminal 1, Terminal 2, e così via. Uno solo dei panel riceverà l'input della tastiera e sarà quello la cui etichetta non è grigia.  

![IDE](JupyterLabActive.png)

Opportunamente configurato il terminale deve utilizzare la **bash** shell resa disponibile da IBM via yum nel percorso `/QOpenSys/pkgs`.
Importanti per una installazione su server localizzato in **Italia** i seguenti due parametri di ambiente: `QIBM_PASE_CCSID`  e `PASE_LANG`.
Possiamo visualizzarne il valore corrente con i seguenti comandi *echo*:

```
bash-4.4$ echo $QIBM_PASE_CCSID
1208
bash-4.4$ echo $PASE_LANG
IT_IT
```

### system 

Quando necessario ricorriamo alla [documentazione ufficiale](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_74/rzalf/rzalfpasesystem.htm) relativa alla utilità in oggetto.

![IDE](PASEsystem.png)

```
bash-4.4$ system -h
Utilizzo: system [-beEhiIkKnOpqsv] command
```

Esempio di utilizzo:

```
system 'DSPMSGD RANGE(CPF0001 CPF0099)' | grep -1 'Messaggio . . . :'
system 'DSPMSGD RANGE(CPF0001 CPF9999)' | grep    'Messaggio . . . :' | grep può > ElencoMsg.txt 
```