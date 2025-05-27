#  Cloud-Architektur – Second Style

##  Annahmen

- Eine Instanz verarbeitet **100 Requests/s**
- Eine Instanz erhält **1 CPU** und **2 GB RAM**

---

##  Schätzungen

- **Monatliche User:** 300.000  
- **Durchschnittliche Requests pro User:** 200  
- **Nutzung pro Tag:** 12 Stunden  
- **Durchschnittliche Last:** ~46 Requests/Sekunde

---


##   <img src="https://static-00.iconduck.com/assets.00/google-cloud-icon-2048x1646-7admxejz.png" alt="Google Cloud" width="25">&nbsp;  GCP Produkte und Konfiguration

### 1️⃣ Google Kubernetes Engine (GKE)

- **Region:** Frankfurt (`europe-west3`)  
- **Node-Typ:** `e2-custom` (4 vCPU, 8 GiB RAM)  
- **Anzahl Nodes:** 4  
- **Autoscaling:** Aktiviert  
- **Kosten pro Monat:** **514,84 $**

---

### 2️⃣ Datenbanken

#### PostgreSQL  
*(Auth DB, Artikel DB, Review DB, Zahlungs-DB, User DB, Versand-DB)*

- **Produkt:** Cloud SQL  
- **Region:** Frankfurt (`europe-west3`)  
- **Instanz-Typ:** `db-lightweight-1` (1 vCPU, 3,75 GiB RAM)  
- **Speicher:** 20 GB + 20 GB Backup  
- **Speichertyp:** SSD  
- **Anzahl Instanzen:** 6  
- **Kosten pro Monat:** **766,32 $**

#### MongoDB & Elasticsearch  
*(Mongo: Auth DB, Like DB | ES: Suche DB)*

- **Produkt:** Kubernetes Engine  
- **Node-Typ:** `e2-custom` (1 vCPU, 3,75 GiB RAM)  
- **Region:** Frankfurt  
- **Anzahl Nodes:** 3  
- **Betriebssystem:** Ubuntu  
- **Kosten pro Monat:** **200,70 $**

#### Memorystore (Redis Cluster)

- **Region:** Frankfurt (`europe-west3`)  
- **Typ:** Shared-Core Nano (1,4 GB)  
- **Shards:** 1  
- **Replikas:** 1  
- **Kosten pro Monat:** **54,75 $**

---

### 3️⃣ Asynchrone Kommunikation (Pub/Sub)

- **Topics:** 2 (Zahlung → Versand, Versand → Notification)  
- **Subscriptions:** 5  
- **Datenvolumen:** 1 GiB/Tag  
- **Retention:** 7 Tage  
- **Kosten pro Monat:** **9,32 $**

---

### 4️⃣ Cloud Storage

- **Location Type:** Multi-region  
- **Region:** Europa (`eu`)  
- **Typ:** Standard Storage  
- **Gesamtspeicher:** 1 TB  
- **Monatlich geschrieben:** 50 GB  
- **Monatlich gelesen:** 5 TB  
- **Kosten pro Monat:** **128,96 $**

---

### 5️⃣ Monitoring & Analytics

#### Cloud Monitoring

- **Metriken:** 40  
- **Datapoints pro Stunde:** 120  
- **Ressourcen:** 24  
- **Kosten pro Monat:** **126,83 $**

#### BigQuery

- **Typ:** On-Demand  
- **Datenmenge:** 120 GB  
- **Aktiver Speicher:** 120 GB  
- **Kosten pro Monat:** **2,34 $**

---

## Gesamtkosten pro Monat

**1.804,06 $**

---

## 🔗 Link zur GCP-Konfiguration

[Cloud Pricing Calculator](https://cloud.google.com/products/calculator?dl=CjhDaVE1TWpZeU5URmpNQzAzTldVMExUUTNNR0l0T0RBMll5MWxOVEZoTW1FeVkyVTNOMk1RQVE9PRAPGiQxQ0RDQTNGNi04NTlELTQ1MTMtQjhCRS1DNTM1RDYzNTEyNUI)
