## PlantUML-Komponenten-Diagramm

```
@startuml
!define RECTANGLE class
skinparam componentStyle rectangle
top to bottom direction

package "Clients" {
    actor "Web User" as WebUser
    actor "Mobile App User" as MobileUser
    actor "Admin User" as AdminUser
    [Web UI] as WebUI
    [Mobile App] as MobileApp
    [Admin UI] as AdminUI

    WebUser --> WebUI
    MobileUser --> MobileApp
    AdminUser --> AdminUI
}

package "SecondStyle System" {

    [API Gateway] as Gateway

    component "Auth Service" as Auth
    component "User Profile Service" as UserProfile
    component "Artikel Service" as Artikel
    component "Bestell Service" as Bestell
    component "Artikel Suche Service" as ArtikelSuche
    component "Zahlungsservice" as Payment
    component "Versandservice" as Shipping
    component "Bewertungsservice" as Review
    component "Like Service" as Like
    component "Messaging Service" as Messaging
    component "Notification Service" as Notification
    component "Monitoring Service" as Monitoring
    component "Moderation Service" as Moderation
    component "Analytics Service" as Analytics

    database "Auth DB\n(PostgreSQL)" as AuthDB
    database "User DB\n(PostgreSQL)" as UserDB
    database "Artikel DB\n(PostgreSQL)" as ArtikelDB
    database "Suche DB\n(Elasticsearch)" as SearchDB
    database "Zahlungs-DB\n(PostgreSQL)" as PaymentDB
    database "Versand-DB\n(PostgreSQL)" as ShippingDB
    database "Review DB\n(PostgreSQL)" as ReviewDB
    database "Like DB\n(MongoDB)" as LikeDB
    database "Messaging DB\n(MongoDB)" as MessagingDB

    WebUI --> Gateway
    MobileApp --> Gateway
    AdminUI --> Gateway

    Gateway --> Auth : REST
    Gateway --> UserProfile : REST
    Gateway --> Artikel : REST
    Gateway --> ArtikelSuche : REST
    Gateway --> Bestell : REST
    Gateway --> Review : REST
    Gateway --> Like : REST
    Gateway --> Messaging : REST
    Gateway --> Notification : REST
    Gateway --> Monitoring : REST
    Gateway --> Moderation : REST
    Gateway --> Analytics : REST

    Bestell --> Payment : REST
    Bestell --> Artikel : REST
    Auth --> AuthDB
    UserProfile --> UserDB
    Artikel --> ArtikelDB
    ArtikelSuche --> SearchDB
    Payment --> PaymentDB
    Shipping --> ShippingDB
    Review --> ReviewDB
    Like --> LikeDB
    Messaging --> MessagingDB

    Payment --> Shipping : Event (asynchron)
    Shipping --> Notification : Event (asynchron)
    Payment --> UserProfile : REST
    Artikel --> UserProfile : REST
    Review --> UserProfile : REST
    Like --> UserProfile : REST
    Messaging --> UserProfile : REST
    Moderation --> Artikel : REST
    Moderation --> Review : REST
    Moderation --> Messaging : REST
}

package "Externe Adapter" {
    [Stripe Adapter] as Stripe
    [Twilio Adapter] as Twilio
    [SendGrid Adapter] as SendGrid

    Payment --> Stripe : Zahlungsabwicklung
    Notification --> Twilio : SMS
    Notification --> SendGrid : E-Mail
}

Nur für Design!
Payment -[hidden]-> Stripe
@enduml
```
