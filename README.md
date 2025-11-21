# 🔬 Analisi dell'Interdisciplinarità e Autarchia nella Scienza

Questo progetto implementa un'analisi approfondita della struttura delle citazioni tra diverse discipline scientifiche, utilizzando la **Social Network Analysis (SNA)** e metriche avanzate come la **Rao Quadratic Entropy** per quantificare l'interdisciplinarità.

L'analisi si basa sulla comparazione dei **flussi di citazione osservati** con i **flussi attesi** in un modello nullo, rivelando le relazioni di dipendenza e le dinamiche di auto-referenzialità di ogni disciplina.

## 🌟 Concetti Chiave

Il progetto si concentra sulla matrice di flusso di citazioni $F$, dove $F_{i \rightarrow j}$ rappresenta le citazioni dalla disciplina $i$ alla disciplina $j$.

### 1. Flusso Atteso ($E$)
Per determinare se una citazione da $i$ a $j$ è significativa, si calcola il flusso atteso $E$ assumendo una distribuzione casuale basata sui volumi di output e input di ciascuna disciplina:
$$
E_{i \rightarrow j} = \text{out}_i \cdot \frac{\text{in}_j}{n}
$$

### 2. Metrica di Normalizzazione (G-test)
La matrice di flusso normalizzata $G$ è cruciale per la visualizzazione e si basa sulla devianza tra $F$ ed $E$:
$$
G_{ij} = F_{ij} \cdot \log \left( \frac{F_{ij}}{E_{ij}} \right)
$$
Archi con $G_{ij} > \text{threshold}$ (ad esempio, 10) indicano una **relazione di citazione significativamente più forte del previsto**.

### 3. Interdisciplinarità (Rao Quadratic Entropy)
La misura centrale per l'interdisciplinarità ($H_i$) cattura la **diversità** e la **distanza** delle discipline citate da $i$. Una disciplina è più interdisciplinare se cita in modo diffuso discipline che sono, a loro volta, molto distanti tra loro nella rete:
$$
H_i = \sum_{j,k} p_{ij} \cdot p_{ik} \cdot d_{jk}
$$

## 💾 Struttura del Repository e Dataset

Il progetto utilizza R come linguaggio di analisi e le librerie `igraph` e `dplyr`.

I file di input necessari sono:

| File | Descrizione | Formato |
| :--- | :--- | :--- |
| `flows.txt` | Matrice dei flussi di citazioni **assoluti** ($F$). | Numerico (una riga per riga della matrice) |
| `disciplines.txt` | Nomi delle discipline (nodi della rete). | Caratteri (uno per riga) |
| `size.txt` | Dimensione di ciascuna disciplina (numero di articoli). | Numerico (uno per riga) |

## 🚀 Obiettivi del Progetto (Challenges)

Il codice R (`Interdisciplinarity_and_hierachity.Rmd`) è stato sviluppato per affrontare le seguenti sfide analitiche:

### 1. Auto-citazione e Popolarità
* Identificare le discipline più **auto-citanti** (alto ratio $F_{ii}/\text{out}_i$).
* Identificare le discipline più **citate** (alto $\text{in}_j$).

### 2. Normalizzazione
* Calcolare la **matrice di flusso atteso** ($E$) e le matrici normalizzate ($X$-test e $G$-test).

### 3. Visualizzazione della Rete
* Visualizzare la **rete di flusso normalizzata** (basata su $G$), mostrando solo gli archi che superano la soglia di significatività.
* Il layout grafico è ponderato: la **dimensione del nodo** riflette la dimensione della disciplina e lo **spessore dell'arco** riflette il peso $G_{ij}$. 

### 4. Quantificazione dell'Interdisciplinarità
* Calcolare e classificare le discipline in base alla loro **Rao Quadratic Entropy** ($H$), identificando i veri **"crocevia della conoscenza"**.

## 🛠️ Come Eseguire l'Analisi

1.  **Requisiti:** Assicurarsi di avere R e RStudio installati.
2.  **Librerie:** Installare le librerie necessarie:
    ```r
    install.packages(c("igraph", "dplyr"))
    ```
3.  **Dati:** Posizionare i file `flows.txt`, `disciplines.txt` e `size.txt` nella stessa directory del file `.Rmd`.
4.  **Esecuzione:** Aprire il file `.Rmd` in RStudio e fare clic su **Knit** per generare il report HTML completo contenente tutti i passaggi, le spiegazioni e i risultati delle analisi.
