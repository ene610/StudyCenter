vcluste: group of computers che comunicano tra di loro (nodi)
Spark è veloce perchè distribuisce l'esecuzione tra i nodi
Distribuited computin significa più potenza ma maggiore complessità (Debugging non è facile)

# Cluster components

![[Cluster architecture.png]]

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

(Spark's execution/deployment mode determines where the driver and executors are physically located when a Spark application is run)
descrive l'infrastruttura computazionale usata da spark, in particolare, il network e i nodi.
(deployement mode vs execution mode spesso sono la stessa cosa).

- **Local mode**: tutte le componenti sono eseguite in una singola JVM. driver, executor e "cluster manager" sono eseguiti sulla stessa macchina per testing purpose. Il cluster manager non fa molto poichè le risorse si trovano tutte in un punto.![[Local mode.png]]
- **Standlone mode**: le componenti girano su un singolo cluster. Il cluster manager e il driver possono girare su un nodo in cui gira già un esecutore.![[Standlone mode.png]]
- **Client mode**: Il driver (edge node) è eseguito al di fuori del cluster, il cluster manager è eseguito su un nodo a parte.![[Client mode.png]]
- **Cluster mode:** il driver viene eseguito all'interno del cluster in un nodo dedicato.![[Cluster mode.png]]

# Executor Memory management

## Caching & Storage levels

Caching significa persistere i dati nel esecutore. utile quando devi usare dati o risultati frequnetemente, affinchè i dati sono disponibili se richiesti nuovamente.
i dati sono memorizzati in diversi Storage levels:

![[Caching & storage levels.png]]

Nel caso del memory level "Memory only" i dati sono salvati in cache, permettendo un più veloce accesso mentre nel caso di "Memory And Disk" i dati sono salvati in prima battuta sulla cache, quelli che eccedono la memoria sono salvati sul disco del executor.

![[Caching eviction.png]]

In scala invece possono essere salvati anche in formato serializzato, in pyspark non è possbili scegliere questa opzione (sono sempre serializzati).
![[Code4Caching.png]]

## Partition functions

**repartition** e **coalesce** sono le funzioni che partizionamento il dataframe.
La differenza tra le due funzioni sono:

- repartition incrementa e diminuisce le partizioni, coalesce riduce il numero di partizioni
- repartition è una wide trasformation (causa una shuffle), coalesce è una narrow transformation, repartition è più lenta della coalesce
- repartition distribuisce bene i dati rispetto a una coalesce, che può risultare in una data skew
