# Cable and towel Detection and Segmentation

Questo repository contiene il progetto sviluppato per il corso di Computer Vision (a.a. 2024). Il lavoro è stato svolto in gruppo e ha come obiettivo la realizzazione di un modello di segmentazione per identificare cavi elettrici e torri di trasmissione all'interno di immagini aeree.

![Cable and Towel Detection and Segmentation](images/cable%20and%20tower%20detection.png)


## Dataset
Per l’addestramento e la valutazione del modello è stato utilizzato il dataset introdotto nel paper:

TTPLA: An Aerial-Image Dataset for Detection and Segmentation of Transmission Towers and Power Lines [Y. Lu et al., 2021]

Il dataset TTPLA è composto da immagini aeree che raffigurano reti di distribuzione elettrica. In particolare, le annotazioni fornite consentono la segmentazione delle torri di trasmissione e delle linee elettriche. Le immagini presentano scenari realistici e variegati, con condizioni ambientali diverse. 

## Modello utilizzato
Per affrontare il task di segmentazione, abbiamo scelto di utilizzare il framework **Detectron2**, sviluppato da Facebook AI Research (FAIR), che fornisce un’ampia gamma di modelli preaddestrati per compiti di detection e segmentation.

Dopo aver sperimentato diversi modelli preaddestrati messi a disposizione da Detectron2, abbiamo deciso di utilizzare il modello mask_rcnn_X_101_32x8d_FPN_3x.yaml, appartenente alla famiglia Mask R-CNN. Questo modello combina una backbone ResNeXt-101 con Feature Pyramid Network (FPN), offrendo un buon compromesso tra accuratezza e capacità di generalizzazione, particolarmente utile per riconoscere oggetti sottili e complessi come cavi e torri.

## Fine Tuning
Abbiamo condotto una serie di esperimenti per identificare la configurazione ottimale dei parametri di addestramento del modello. In particolare, sono stati esplorati diversi valori per il learning rate, il numero di iterazioni, la dimensione dei batch, al fine di massimizzare la qualità della segmentazione di cavi e torri.

## Data Augmentation
Per migliorare la capacità di generalizzazione del modello, abbiamo applicato tecniche di data augmentation sul set di addestramento. Le immagini aumentate sono state ottenute selezionando campioni casuali e applicando trasformazioni quali flip orizzontale/verticale e modifiche a luminosità, contrasto e saturazione, utili soprattutto per distinguere i cavi dallo sfondo.

Tuttavia, i modelli addestrati con data augmentation non hanno mostrato un miglioramento significativo delle prestazioni. Questo potrebbe essere dovuto a un’eccessiva somiglianza tra immagini aumentate e originali, al rischio di overfitting o alla necessità di riadattare gli iperparametri per un dataset più esteso. Ulteriori esperimenti sarebbero necessari per valutare trasformazioni alternative e strategie di ottimizzazione più efficaci.

## Risultati
Il modello migliore tra quelli addestrati è risultato essere quello senza data augmentation, capace di raggiungere soglie più soddisfacenti con una minore complessità. In particolare, con 18.000 iterazioni è stato possibile ottenere punteggi di bbox: 59.5 e segm: 40.5. Sebbene anche i modelli con data augmentation abbiano mostrato buone performance, abbiamo preferito la soluzione più semplice ed efficace in termini di stabilità e tempi di addestramento.
