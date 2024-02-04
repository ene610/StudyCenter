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

