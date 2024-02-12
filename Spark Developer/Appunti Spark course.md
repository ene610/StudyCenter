vcluste: group of computers che comunicano tra di loro (nodi)
Spark è veloce perchè distribuisce l'esecuzione tra i nodi
Distribuited computin significa più potenza ma maggiore complessità (Debugging non è facile)

# Cluster components

**Driver**: è il guidatore degli esecutori, contiene il codice e delega i compiti agli esecutori 
**Esecutori**: esegue i compiti, più esecutori abbiamo più possiamo dividere i compiti
**Cluster manager**: è il responsabile della gestione del cluster e mette in collegamento gli esecutori con il driver. Quando il driver decide cosa deve esser fatto e come, richiede le risorse al cluster manager che riserverà un numero di esecutori in base al workload.
**Spark session**: inizializzato da un driver rappresenta il punto di contatto con un workload. rappresenta l'interfaccia con cui il driver comunica con un cluster.

![[Cluster components.png]]

Quando un driver ha necessità di eseguire un workload allora richiede al cluster manager le risorse necessarie. Il Cluster manager allora alloca gli esecutori allo specifico workload. 

Spark session e esecutori si scambiano dati, se dobbaimo fare un operazione in una tabella questa viene inviata in parti a 1 o più esecutori. quando gli esecutori hanno finito con i calcoli questi inviano i risultati al driver. Anche gli esecutori tra di loro si scambiano i dati in base alle esecuzioni che devono completare.

Questa suddivisone non è fisica ma virtuale. un worker node può contenere più esecutori.

**Executors**

![[executros.png]]

Un worker node ha 1 o più executors (tipicamente 1) che non è un programma runnato in una JVM, viene creato quando l'applicazione spark viene iniziata e appartiene a una specifica applicazione. Un executor può lavorare sia in sequenza che in parallelo in base alla configurazione. Un executors è de-commissionato quando finisce l'applicazione Spark oppure quando va in failure.

**Dynamic Resource allocation**

Se attivata, permette di bilanciare il numero di executors in base al carico di lavoro, ottimizzando le performance in scenari in cui il carico di lavoro varia nel tempo.
Quando è attivata , Spark osserva il carico che deve essere eseguito e crea un numero di esecutori esponenziale (1,2,4,8) in base al carico di lavoro rimanente per poi rimuovere automaticamente quelli che rimangono in idle.

# Execution modes

describe in che tipo di com

