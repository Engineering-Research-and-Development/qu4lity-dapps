# Identity - v 1.0
## Introduzione e modello dati

Identity è una applicazione per la creazione e la gestione di identità digitali, registrate utilizzando una tecnologia Blockchain, collegate da un processo di validazione da parte di identità già censite, facendo uso di un processo di autenticazione attraverso una firma digitale. 
Una identità digitale è intesa come una identità dotata di un sistema di crittografia a chiave asimmetrica, con una chiave pubblica e una chiave privata.

Il meccanismo prevede che venga inserita una (o più) identità Root (controller di se stessa) che poi possa fare da Controller e in questo modo garantisca per le nuove identità create. Ogni identità creata potrà a sua volta essere controller di una nuova identità fino ad un massimo di 5 gradi di separazione.

Per la creazione di una identità, il Controller dovrà aver ricevuto la public Key 
dell'identità da creare e firmare suddetta chiave mediante la propria chiave privata, per certificare la propria identità. Lo smartcontract verificherà mediante la chiave pubblica del controller la firma apposta sui dati della nuova identità da inserire e solo se tutti i controlli vanno a buon fine, verrà fatto un inserimento sul Ledger del nuovo record che identifica la nuova identità.

Il controller (e solo lui) avrà anche la possibilità di modificare lo stato di una identità sul ledger, i cui stati possono variare in Attiva, Sospesa o Revocata.

La struttura dati che modella questa casistica è Identity che è composta di due parti: baseEntry e statusEntry.  


Identity:

```
Identity { 
  BaseEntry,
  StatusEntry
}
```

Base Entry: contiene i dati fissi censiti nel momento del censimento.

```
BaseEntry {
  Address,
  Created,
  CreatedBy,
  Controller,
  PKeyBlob,
  KeyType,
  Details
}
  
```

Status Entry: rappresenta lo stato dell'identità al momento della data specificata.

```
StatusEntry {
  Address,
  SubAddress,
  ValidFrom,
  UpdatedBy,
  Status
}
  
```



