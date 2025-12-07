# Authorization Testing Report, Booking System (Phase 3)

## 1. Overview
Tässä raportissa käsitellään Booking System -sovelluksen autorisointiin liittyvää testaamista kolmella eri käyttäjäroolilla. Testaus sisälsi myös käyttöliittymätestausta, API-pyynnöllä tehtäviä kokeiluja, sekä Gobuster, Wfuzz ja ZAP työkaluilla tehtyjä testauksia.

Käyttäjäroolit:
- Guest (kirjautumaton käyttäjä)
- Reserver (peruskäyttäjä)
- Admin (ylläpitäjä)

---

## 2. Havaitut sivut ja päätepisteet
### KÄyttöliittymän sivut
- Etusivu. Näyttää resurssit, varaukset, kirjautumisen ja rekisteröinnin.
- Kirjautumissivu
- Rekisteröintisivu
- Resurssien lisäyssivu (kirjautuneille)
- Varaussivu (kirjautuneille)

### API-päätepisteet (havaittu UI:n/ZAPin kautta)
- `/api/reservations`
- `/api/reservations/{id}`
- `/api/resources`
- `/api/auth` (sisäinen)
- Ei erillisiä admin-päätepisteitä

### Huomio
Tuntemattomat endpointit palauttavat aina:
`HTTP 303 → status.html`, eivät 404-koodia.  
Hakemisto- tai API-fuzzauksella ei voi löytää piilotettuja reittejä.

---

## 3. Roolikohtaiset oikeudet

### Guest (kirjautumaton käyttäjä)
**Can do:**
- Näyttää etusivun
- Näkee resurssit ja varausten listauksen ilman käyttäjätietoja
- Pääsee kirjautumissivulle, ja rekisteröitymissivulle

**Cannot do:**
- Ei pääsyä resurssien tekemiseen.
- Ei voi luoda varauksia
- Ei admin-toimintoja (varauksien hallinta yms)

**Havaittu ongelma:**
- Guest pystyy näkemään muiden tekemiä varauksia suoraan etusivulta  (**IDOR-haavoittuvuus**)

---
