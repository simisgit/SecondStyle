
# Microservice-Architektur für SecondStyle

## Übersicht der Microservices

| Service                | Beschreibung                                      | Datenbank                  | API vorhanden | Kommunikation           |
|------------------------|---------------------------------------------------|----------------------------|---------------|-------------------------|
| API Gateway            | Zentrale Schnittstelle für alle Anfragen          | ❌                         | ✅            | Verteilt synchron Anfragen |
| Auth Service           | Authentifizierung, Tokenmanagement                | PostgreSQL (Auth DB)       | ✅            | REST synchron           |
| User Profile Service   | Nutzerprofile, Stammdaten                         | PostgreSQL (User DB)       | ✅            | REST synchron           |
| Artikel Service        | Artikel einstellen, bearbeiten                    | PostgreSQL (Artikel DB)    | ✅            | REST synchron           |
| Artikel Suche Service  | Artikelsuche, Filter                              | Elasticsearch (Suche DB)   | ✅            | REST synchron           |
| Bestellservice         | Bestellen von Artikeln                            | ❌                        | ✅            | REST synchron           |
| Zahlungsservice        | Zahlungen, Transaktionen                          | PostgreSQL (Zahlungs-DB)   | ✅            | REST + Events           |
| Versandservice         | Versandabwicklung, Labels, Tracking               | PostgreSQL (Versand-DB)    | ✅            | Asynchron (Event-basiert)|
| Bewertungsservice      | Bewertungen, Rezensionen                          | PostgreSQL (Review DB)     | ✅            | REST synchron           |
| Like Service           | Likes, Favoriten                                  | MongoDB (Like DB)          | ✅            | REST synchron           |
| Messaging Service      | Nachrichten zwischen Nutzern                      | MongoDB (Messaging DB)     | ✅            | REST synchron           |
| Notification Service   | E-Mail & SMS Benachrichtigungen                   | ❌                         | ✅            | Asynchron (Events)      |
| Monitoring Service     | Monitoring, Healthchecks                          | ❌                         | ✅            | REST synchron           |
| Moderation Service     | Moderation von Inhalten                           | ❌                         | ✅            | REST synchron           |
| Analytics Service      | Statistiken, Auswertungen                         | ❌                         | ✅            | REST synchron           |

---

## Kommunikationstypen

| Von → Nach                 | Typ        |
|----------------------------|------------|
| Client → API Gateway → Services | Synchron   |
| Zahlungsservice → Versandservice | Asynchron  |
| Versandservice → Notification   | Asynchron  |
| Moderation → Artikel/Review/Messaging | Synchron   |
| Services → User Profile Service | Synchron   |

---

## PlantUML-Komponenten-Diagramm

