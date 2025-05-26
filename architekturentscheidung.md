## Architektonische Eigenschaften für SecondStyle

Die drei wichtigsten Eigenschaften für SecondStyle sind:

1.  **Skalierbarkeit:** Das System muss in der Lage sein, steigende Nutzerzahlen und Transaktionen zu bewältigen.
2.  **Sicherheit:** Schutz der Nutzerdaten und sichere Zahlungsabwicklung.
3.  **Benutzerfreundlichkeit:** Einfache und intuitive Bedienung für alle Nutzer.

### Details:

1.  **Skalierbarkeit:**
    *   **Warum wichtig:** SecondStyle soll wachsen und viele Nutzer gleichzeitig bedienen können.
    *   **Details:** Wir müssen eine Architektur wählen, die es uns erlaubt, Ressourcen (Server, Datenbanken etc.) einfach hinzuzufügen, wenn die Last steigt. Dies könnte durch Microservices, Cloud-basierte Lösungen oder Load Balancing erreicht werden.
    *   **Beispiel:** Wenn die Anzahl der Nutzer um das Zehnfache steigt, sollte die Plattform nicht zusammenbrechen, sondern weiterhin reibungslos funktionieren.

2.  **Sicherheit:**
    *   **Warum wichtig:** Nutzer vertrauen SecondStyle ihre persönlichen Daten und Zahlungsinformationen an.
    *   **Details:** Wir benötigen robuste Sicherheitsmaßnahmen, um Daten vor unbefugtem Zugriff zu schützen. Dazu gehören Verschlüsselung, sichere Authentifizierungsmethoden und regelmäßige Sicherheitsüberprüfungen.
    *   **Beispiel:** Die Kreditkarteninformationen der Nutzer müssen sicher gespeichert und übertragen werden, um Betrug zu verhindern.

3.  **Benutzerfreundlichkeit:**
    *   **Warum wichtig:** Eine einfache und intuitive Plattform fördert die Nutzung und Bindung der Nutzer.
    *   **Details:** Wir müssen auf ein klares Design, einfache Navigation und reibungslose Prozesse achten. Nutzer sollten schnell finden, was sie suchen, und ihre Aufgaben einfach erledigen können.
    *   **Beispiel:** Das Hochladen eines Artikels zum Verkauf sollte mit wenigen Klicks erledigt sein.

## Architekturentscheidungsdokumente (ADR)

### ADR-1: Wahl der Datenbanktechnologie

*   **Titel:** Wahl zwischen relationaler und NoSQL-Datenbank  
*   **Status:** Akzeptiert  
*   **Datum:** 01.04.2025  

#### Kontext:

SecondStyle benötigt eine Datenbank zur Speicherung von Nutzerdaten, Artikelinformationen, Transaktionen und anderen relevanten Daten. Es gibt zwei Haupttypen von Datenbanken: relationale (z.B. PostgreSQL, MySQL) und NoSQL (z.B. MongoDB, Cassandra).

#### Entscheidung:

Wir entscheiden uns für eine relationale Datenbank (PostgreSQL).

#### Gründe:

*   **Datenkonsistenz:** SecondStyle benötigt eine hohe Datenkonsistenz, insbesondere für Transaktionen und Finanzdaten. Relationale Datenbanken bieten ACID-Eigenschaften (Atomicity, Consistency, Isolation, Durability), die dies gewährleisten.
*   **Komplexität der Datenbeziehungen:** Die Beziehungen zwischen Nutzern, Artikeln und Transaktionen sind komplex. Relationale Datenbanken sind gut geeignet, diese Beziehungen abzubilden und abzufragen (z.B. über JOINs).
*   **Erfahrung des Teams:** Das Entwicklerteam hat mehr Erfahrung mit relationalen Datenbanken, was die Entwicklung und Wartung vereinfacht.

#### Konsequenzen:

*   **Positive:**
    *   Hohe Datenkonsistenz und Zuverlässigkeit.
    *   Einfache Abbildung komplexer Datenbeziehungen.
    *   Gute Unterstützung durch das Entwicklerteam.
*   **Negative:**
    *   Skalierung kann komplexer sein als bei NoSQL-Datenbanken.
    *   Weniger flexibel bei Änderungen des Datenmodells.

#### Alternativen:

*   **NoSQL-Datenbank (MongoDB):** Wäre flexibler bei Änderungen des Datenmodells und potenziell einfacher zu skalieren. Allerdings wäre die Datenkonsistenz geringer, und das Team hat weniger Erfahrung damit.

### ADR-2: Wahl der Authentifizierungsmethode

*   **Titel:** Auswahl der Authentifizierungsmethode für Benutzerkonten  
*   **Status:** Angenommen  
*   **Datum:** 01.04.2025  

#### Kontext:

SecondStyle benötigt eine sichere Methode, um Benutzer zu authentifizieren. Es gibt verschiedene Optionen, darunter:

*   **Lokale Authentifizierung:** Benutzername und Passwort werden in der Datenbank gespeichert.
*   **Social Login:** Benutzer melden sich über bestehende Konten bei Drittanbietern an (z.B. Google, Facebook).
*   **Multi-Faktor-Authentifizierung (MFA):** Kombination aus Passwort und einem zweiten Faktor (z.B. SMS-Code, Authenticator-App).

#### Entscheidung:

Wir entscheiden uns für eine Kombination aus lokaler Authentifizierung mit starken Passwortrichtlinien und der optionalen Möglichkeit, Social Login zu nutzen. Zusätzlich wird die Implementierung von Multi-Faktor-Authentifizierung (MFA) als zukünftige Erweiterung in Betracht gezogen.

#### Gründe:

*   **Sicherheit:**
    *   **Lokale Authentifizierung:** Ermöglicht die Kontrolle über die Passwortrichtlinien (Mindestlänge, Komplexität).
    *   **Social Login:** Bietet eine zusätzliche Sicherheitsebene durch die Sicherheitsmechanismen der Drittanbieter.
    *   **MFA:** Erhöht die Sicherheit erheblich, da selbst bei Kompromittierung des Passworts ein zweiter Faktor erforderlich ist.
*   **Benutzerfreundlichkeit:**
    *   **Social Login:** Vereinfacht die Registrierung und Anmeldung für Nutzer, die bereits Konten bei den unterstützten Anbietern haben.
    *   **Lokale Authentifizierung:** Bietet eine einfache, standardmäßige Option für Benutzer, die keinen Social Login nutzen möchten.
*   **Flexibilität:**
    *   Die optionale Nutzung von Social Login ermöglicht es Benutzern, die für sie bequemste Methode zu wählen.

#### Konsequenzen:

*   **Positive:**
    *   Hohe Sicherheit durch starke Passwortrichtlinien und optionale MFA.
    *   Benutzerfreundlichkeit durch Social Login und einfache lokale Authentifizierung.
    *   Flexibilität für die Benutzer.
*   **Negative:**
    *   Zusätzlicher Entwicklungsaufwand für die Implementierung von Social Login und MFA.
    *   Abhängigkeit von Drittanbietern bei Social Login.
    *   **Technische Schulden:**
        *   Die anfängliche Implementierung von MFA als "zukünftige Erweiterung" kann zu technischen Schulden führen, wenn die Sicherheitsanforderungen steigen und MFA nicht rechtzeitig implementiert wird.
        *   Die Integration von Social Login kann zu technischen Schulden führen, wenn die APIs der Drittanbieter sich ändern und die Integration angepasst werden muss.

#### Alternativen:

*   **Ausschließliche lokale Authentifizierung:** Wäre einfacher zu implementieren, würde aber die Benutzerfreundlichkeit und Sicherheit potenziell beeinträchtigen.
*   **Ausschließlicher Social Login:** Wäre einfacher für die Benutzer, würde aber einige Benutzer ausschließen, die keinen Social Login nutzen möchten.

#### Details zur Umsetzung:

*   **Lokale Authentifizierung:**
    *   Implementierung von starken Passwortrichtlinien (Mindestlänge, Komplexität, regelmäßige Änderung).
    *   Sichere Speicherung der Passwörter durch Hashing und Salting.
*   **Social Login:**
    *   Integration mit etablierten Anbietern wie Google und Facebook.
    *   Sorgfältige Prüfung der Berechtigungen, die von den Drittanbietern angefordert werden.
*   **Multi-Faktor-Authentifizierung (zukünftig):**
    *   Unterstützung von zeitbasierten Einmalpasswörtern (TOTP) über Authenticator-Apps.
    *   Optionaler SMS-Code als zweiten Faktor.
