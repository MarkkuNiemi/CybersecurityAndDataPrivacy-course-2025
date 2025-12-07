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
`HTTP 303 status.html`, eivät 404-koodia.  
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

### Reserver (peruskäyttäjä)
**Can do:**
- Kirjautua ja tehdä varauksia
- Näyttää resurssit
- Voi luoda resursseja
  
**Cannot do:**
- Käyttäjien poisto
- Muiden kuin omien resurssien hallinta

**Havaitut ongelmat:**
- Reserver näkee kaikkien käyttäjien varaukset etusivulla. **Tietosuojan rikkominen**
- Reserver voi luoda uusia resursseja. **Ei roolien mukaista**
- Reserver voi myös hakea kenen tahansa varauksia ID:llä. **IDOR**

### Admin (ylläpitäjä)
**Odotus spekseissä:** Lisätä/poistaa/muokata resursseja ja varauksia, hallita käyttäjiä.

**Todellinen toiminnallisuus:**
- Adminilla ei ole erillistä näkymää tai toiminnallisuutta
- Admin pystyy kirjautumaan sisään ja tekemään varauksia kuten tavallinen käyttäjä.
- Admin pystyy varaamaan resursseja ja hallitsemaan muiden varauksia.
- Admin ei pysty hallinnoimaan käyttäjiä.
- Admin ei pysty poistamaan resursseja

**Havaitut ongelmat:**
- Admin-rooli ei ole toteutettu spesifikaation edellyttämällä tavalla.  
  Käytännössä rooli on lähes sama kuin peruskäyttäjällä, muutamalla lisäoikeudella.
- Varsinaisia admin-päätepisteitä ei ole olemassa, ja UI ei tarjoa hallintatoimintoja.
  
---

## 4. Gobuster ja Wfuzz -testauksen tulokset
