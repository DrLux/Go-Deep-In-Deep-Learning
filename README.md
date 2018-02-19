Capitolo Introduttivo: Modelli basati sull’ energia
Fonte: http://yann.lecun.com/exdb/publis/pdf/lecun-06.pdf
L’obiettivo principale dei modelli statistici e dell’apprendimento automatico è quello di trovare una dipendenza tra le variabili. Una volta individuata, questa correlazione può essere usata per trovare risposte su una nuova e sconosciuta variabile sottoposta.
I modelli basati sull’energia, catturano queste dipendenze assegnando un grado di energia a ogni configurazione di variabili, cioè ogni possibile assegnamento di valor dato alle variabili. 
In questi modelli:
	Fare inferenza (una predizione o il prendere una decisione) consisterà quindi nel settare il valore delle variabili conosciute, e trovare di conseguenza il valore delle rimanenti variabili secondo il criterio di minimizzazione dell’energia complessiva. 
	Fare apprendimento: significa trovare una funzione di energia che associ, un basso livello di energia a valori corretti delle variabili e uno alto ai valori sbagliati. 
	La funzione di perdita: viene minimizzata durante la fase di apprendimento e serve a misurare la qualità della funzione di energia presa in considerazione (trovare quella che fitta meglio i dati).

Appunto non strettamente necessario:
“Nei problemi statistici vi è bisogno di una costante di normalizzazione, cioè una costante che riduce qualsiasi funzione di probabilità, ad una funzione di densità di probabilità con probabilità totale = 1. Nei sistemi a energia globale questa costante non viene usata e ciò permette di avere un design del modello più flessibile.”


Reti di Hopfield: modelli per l’immagazzinamento di memorie 
Fonte: https://www.coursera.org/learn/neural-networks/lecture/9ZOr2/hopfield-nets-13-min
+ Slide del Dipartimento di informatica UniTO.
Nel 1982 John Hopfield, fisico, professore di chimica e biologia, introdusse le reti di Hopfield, che sono l’esempio più semplice di modelli basati sull’ energia. 
Utilizzo: immagazzinamento di memorie e ricostruzione di pattern, cioè una volta immagazzinata una memoria se vengono sottoposte ad un input corrispondente quella stessa memoria ma parzialmente corrotto o incompleto, la rete riesce a ripristinare il dato originale. Le memorie che salviamo sono dette: memorie fondamentali. 
Si compongono di Neuroni (unita binarie) completamente connessi tra loro. Essendo unità non-lineari tutte connesse, sono difficili da analizzare perché possono comportarsi in modi differenti, possono:
	Fermarsi in uno stato stabile;
	Possono oscillare tra più stati;
	Possono seguire traiettorie casuali che rendono impredicibile il loro stato anche avendo informazioni precise sullo stato di partenza;
Ogni neurone ha un bias, che serve come ulteriore controllo oltre ai pesi dei collegamenti, per tenere sotto controllo alla soglia di attivazione del neurone.
Hopfield ha scoperto che se le connessioni sono simmetriche (stesso valore del collegamento tra due neuroni in ambedue le direzioni), si può applicare un modello ad energia globale.
Ogni assegnazione di stato dei neuroni altera il valore finale dell’energia globale e quindi applicando una corretta regole di assegnamento si può minimizzare il valore di questa energia.
L’ energia globale è data dalla somma di tutti i contributi, i quali dipendono dal peso della connessione e dallo stato di due neuroni.
La formula per il calcolo dell’energia prodotta (sarà più chiara dopo aver visionato l’esempio pratico proposto più avanti) è quindi:
 
Wij = rappresenta il peso del collegamento tra il neurone i e il neurone j
Si*Sj = rappresenta il prodotto dello stato di attività dei due neuroni connessi (ricordiamo che sono unità booleane, quindi il valore può essere 1 o 0 oppure a volte 1 o -1) 
SiBi = Bi è il Bias associato al neurone i, un parametro ulteriore alla rete che è arbitrario.
Energia totale è quindi il risultato della differenza tra, il negativo della sommatoria dei prodotti tra stato dei neuroni e relativi Bias, e la sommatoria tra il prodotto dello stato di entrambi i due neuroni comunicanti e il peso del collegamento che li unisce (per tutti i neuroni).

Ogni neurone può calcolare come il valore dell’energia globale cambia al variare del suo stato e in base a ciò scegliere lo stato che minimizzi il valore dell’energia globale.
Cioè:
 
Quindi si calcola prima l’energia globale con questa formula, (ponendo Sj ad un valore attivo),  
E al risultato si sottrae la stessa formula con un valore passivo di Sj (ovvero spegnendo il neurone). 



Teorema di Convergenza: 
Per ogni stato iniziale, la rete convergerà sempre ad uno stato stabile.
	Ogni rete ha N unità binarie, quindi possono esserci sono 2^Npossibili stati (quindi un numero finito di stati)
	Ogni stato è associato ad un valore di energia globale
	Il cambiamento di stato può solo tendere verso un abbassamento dell’energia, se non si può diminuire non si cambia lo stato

Algoritmo
Si parte da una configurazione random di stati e si aggiornano man a mano gli stati dei neuroni (con il criterio di minimizzazione dell’energia globale) fino a quando non si raggiunge uno stato stabile in cui i neuroni non cambiano più gli stati (non si può minimizzare ulteriormente). Il teorema di convergenza ci da certezza che si arriverà sempre ad uno stato stabile.

Esempio pratico di una rete di Hopfield:
	Data una rete con i pesi assegnati, trovare la migliore configurazione di neuroni possibile (assegnare i valori di attivazione dei neuroni in modo tale da minimizzare l’energia complessiva della rete)
 
	Si inizializzano i neuroni ad uno stato random (1 o 0 i possibili valori assegnabili)
 
	Calcoliamo l’energia totale secondo la formula data:
 
Non essendoci il Bias (fai che b = 0 e quindi ignora la prima sommatoria) in questo esempio, sommiamo il risultato della moltiplicazione tra il valore degli stati dei neuroni e il valore dei pesi che li legano.
E = - ( (1 * 1) * 3 + (0*1) * -1 + (0*0) * -1 …….. = -(3)
L’ energia globale è -3, quindi il grado di bontà = 3.
Vogliamo aumentare il grado di bontà e far salire questo valore (facendo scendere il livello di energia)
	A questo punto prendiamo un neurone a caso e ne calcoliamo l’ energy gap   
(sempre ignorando il Bias):
Spiegazione della formula:
Prendendo in considerazione il neurone i, la sua energia locale è data dalla moltiplicazione del peso del collegamento con il suo neurone vicino j per lo stato del neurone j.  IL risultato si ottiene sommando tutti i prodotti cosi ottenuti, tra i vari vicini J del neurone I.


 
L’ energia di quel singolo neurone è:
(1*-4)+(0*3)+(0*3) = -4 -> Quindi andrebbe a peggiorare il grado di bontà, per cui ci conviene lasciarlo a 0 cioè tenerlo spento in modo che la sua energia non contribuisca al calcolo dell’ energia totale. 

 
Energia di questo neurone è:
(1*3) + (0*-1) = 3 -> Che è un numero positivo, e quindi lo lasciamo attivo

 
Energia di questo neurone è:
(1*-1)+(1*2)+(0*3)+(0*-1) = 1 -> La sua energia fa aumentare il valore totale, quindi dobbiamo attivarlo

	A questo punto abbiamo ottenuto questa situazione:
 
In cui il valore di bontà è aumentato: 3 + 2 – 1 = 4 -> prima era 3.
Questa è uno stato minimo locale dal quale non possiamo uscire (nessun neurone cambierà il proprio stato perché peggiorerebbe la situazione).
Il minimo globale invece sarebbe questo, al quale non potevamo arrivare partendo dallo stato iniziale (generato casualmente) da cui siamo partiti. 
 

L’ aggiornamento degli stati dei neuroni non può essere parallelizzato, deve procedere in modo asincrono o si rischia di avere delle oscillazioni.
La proposta di Hopfield è di usare questi modelli per immagazzinare memorie facendo corrispondere quello stato a quello di energia minima, cosicché anche se si dovesse corrompere l’informazione, la rete tenderebbe naturalmente a tornare in quello stato (o anche in caso di informazioni parziali fornite da ricostruire). Inoltre, questi modelli sono fault tollerant, ovvero continuano a lavorare anche se una parte della rete si danneggia o viene a mancare, il risultato prodotto può essere ancora accettabile.

Come immagazzino le informazioni nella rete?
L’input che forniamo alla rete corrisponde ad un vettore di N elementi (dove N corrisponderà poi al numero dei neuroni della rete) dove ogni elemento avrà valore 1 o -1, oppure 1 o 0 (valori che avranno anche poi i neuroni). Durante l’addestramento i pesi dei collegamenti dovranno essere settati in modo da rendere favorevole l’attivazione dei neuroni corrispondenti agli elementi del vettore e rendere cioè quella configurazione, uno dei minimi energetici.
L’output sarà lo stesso un vettore sempre di N elementi il più possibile vicino a quello di input.
Il principio si ispira alla biologia: le sinapsi che collegano neuroni attivi/spenti contemporaneamente sono più forti, quindi pesi maggiori per i collegamenti di neuroni con lo stesso grado di attivazione e minori per quelli di gradi di attivazione differente (ovvero il collegamento tra un neurone attivo ed uno spento sarà minore).
La formula per neuroni di tipo 1 o -1 è più semplice ed è la seguente:
 
Ovvero si incrementa il valore del peso in base alla moltiplicazione tra lo stato dei due neuroni agli estremi del collegamento. Se entrambi sono attivi/disattivi il collegamento sarà incrementato, altrimenti decrementato.
Nel caso si vogliano memorizzare più memorie fondamentali nella stessa rete si andranno a sommare i pesi ottenuti da ogni configurazione di valori di neuroni ottenuta per ogni memoria fondamentale, e si divideranno per il numero di memorie immagazzinate.
 
Ovvero lo stesso collegamento tra il neurone i e j si calcola per tutte le M configurazione di valori di i e j, si sommano tra di loro i valori di tutti gli M pesi e si divide il risultato per M.
La formula è guidata dagli errori, quindi non si basa sul verificare il risultato proposto con quello che ci si aspetterebbe di ricevere. Incrementiamo il collegamento tra due neuroni in base al prodotto tra gli stati dei due.
La formula per neuro di tipo 1 o 0 è un leggermente più complicata:
 

Capacità di immagazzinamento delle informazioni
La capacità di una rete totalmente connessa, con N unità è solo di 0.14N memorie fondamentali immagazzinabili prima che la rete si sovraccarichi e inizi a confonderle e fare errori.
Perché accade ciò?

Ogni volta che memorizziamo una nuova configurazione, ci immaginiamo di creare un nuovo picco minimo di energia. Quando però ve ne sono due troppo vicini, questi tendono a fondersi in un unico minimo intermedio.
 
Per cercare di arginare questo problema, e rimuovere questi stati stabili che però non rappresentano nessuna memoria (stati spuri), si è ideato il sistema dell’unlearning:
Una volta che la rete arriva ad uno stato spurio, procediamo attraverso un calcolo perfettamente inverso a quello fatto per raggiungerlo in modo da eliminarlo. È dimostrato che si può distinguere uno stato spurio da una memoria fondamentale. ( Robins, A. V., & McCallum, S. J. R. (2004). A robust method for distinguishing between learned and spurious attractors. Neural Networks, 17(3), 313–326. doi:10.1016/j.neunet.2003.11.007)
Non era ben chiaro però quanto unlearning si dovesse fare.
Oltre a rimuove i minimi spuri, ci sono altri modi per aumentare le capacità della rete? 
Si, invece di immagazzinare tutto il vettore dati in un colpo solo si possono ciclare più fasi di apprendimento. Usando la procedura di convergenza del percettrone per addestrare ogni unità al suo corretto stato conoscendo il valore di tutti gli altri elementi del vettore dati.

Epilogo
Nota: Crick and Mitchison proposero che il processo di unlearning potrebbe essere ciò che succede nel nostro cervello durante la fase REM (Rapid Eyes Movement). Ovvero, durante il giorno noi acquisiamo un sacco di nuove informazioni (e otteniamo dei minimi spuri) e durante la notte disimpariamo (il che spiegherebbe perché non memorizziamo “l’esperienza” che viviamo durante i sogni e ce li dimentichiamo, a parte quelli che abbiamo poco prima di svegliarci, in quanto memorizzati nella memoria a breve termine).
  

Lati positivi di queste reti:
	Completano pattern parziali
	Sono fault tolerant: anche se alcune connessioni si danneggiano, un risultato viene comunque prodotto e spesso è accettabile.
	Posso estrarre prototipi di informazione, ovvero il modo in cui codificano una memoria fondamentale in uno stato stabile. 
	Il modo in cui apprendono è simile a ciò che accade nel nostro cervello.
Lati negativi:
	Non sempre uno stato stabile è una memoria fondamentale, esistono stati spuri
	L’ opposto di uno stato stabile, è ancora uno stato stabile
	Anche le combinazioni di stati stabili lo sono
	IL numero di memorie fondamentali memorizzabili (con quasi nessun errore)
N/2logN
(Dove N = num neuroni)
	Il numero massimo di memorie fondamentali memorizzabili senza errori è di 0.14N 






 






