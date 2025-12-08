# Authorization Testing Report, Booking System (Phase 3)

## 1. Johdanto
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
### Gobuster
Gobusterilla tehty hakemisto- ja tiedostohaku ei tuottanut yhtään todellista lisäpolkua.
ChatGPT:n avulla syyksi ilmeni seuraavat tekijät:
- Kaikki tuntemattomat URL-osoitteet palauttavat saman `HTTP 303` -uudelleenohjauksen.
- Sovellus ei koskaan palauta `404 Not Found` -vastetta.

Tämän vuoksi Gobuster näytti löytävän suuren määrän vääriä positiivisia tuloksia, jotka olivat kaikki samaa 303-uudelleenohjausta. Todellisia, olemassa olevia polkuja ei löytynyt.  
**Johtopäätös:** Sovelluksessa ei ole piilotettuja hakemistoja tai endpointteja, eikä Gobusterin avulla voi löytää uusia reittejä tästä sovelluksesta.

### Wfuzz
#### Yleiset endpointit
Myös Wfuzz palautti lähes kaikista poluista identtisen 303-uudelleenohjauksen.  
Koska sovellus ei erottele virheellisiä ja oikeita URL-osoitteita HTTP-statuskoodeilla, Wfuzz ei pystynyt tunnistamaan todellisia reittejä.

**Johtopäätös:** Wfuzz ei löytänyt piilotettuja sivuja tai API-päätepisteitä, koska sovellus ei anna tarkoituksenmukaisia virhekoodeja (404).

#### API-idarointi, IDOR (Insecure Direct Object Reference)
Testissä haettiin `/api/reservations/{id}` eri ID-arvoilla.  
Tulos:
- Varaus-ID:t 3 ja 5 palauttivat `HTTP 200` -vastauksen.
- Pyyntö onnistui ilman kirjautumista.

Tämä tarkoittaa:
- Varaustietoja voi lukea pelkän ID:n perusteella  
- Autorisointia ei tarkasteta backendissä  
- Kyseessä on vakava IDOR -haavoittuvuus

**Johtopäätös:** Varausten yksittäinen hakeminen on täysin suojaamatonta, ja mikä tahansa käyttäjä (myös Guest) voi lukea muiden varauksia, jos arvaa ID:n. Tämä on sovelluksen suurin tietoturvapuutteista.

### Yhteenveto
- Sovellus ei palauta 404-koodia → fuzzing-työkalut eivät löydä piilotettuja polkuja  
- Gobuster ja Wfuzz eivät tunnistaneet uusia endpointteja   
- ID-fuzzing paljasti merkittävän autorisointivirheen (IDOR)
  
---

## 5. ZAP, yhteenveto

ZAP-skannaus suoritettiin sovelluksen tunnistettujen sivujen ja API-kutsujen analysoimiseksi. Skannauksen tavoitteena oli löytää piilotettuja endpointteja, tarkastaa autorisoinnin toteutus ja havaita mahdollisia syötehaavoittuvuuksia.

ZAP ei löytänyt uusia tai piilotettuja reittejä. Kaikki tuntemattomat URL-osoitteet johtavat 303-uudelleenohjaukseen, mikä estää ZAPia tunnistamasta todellisia virhekoodeja. ZAPin havainnot tukevat manuaalista testausta: backend ei tee selkeitä roolipohjaisia tarkistuksia, ja osa API-pyynnöistä vaikuttaa palauttavan sisältöä ilman kunnollista autorisointia. ZAP ei havainnut XSS-, SQL Injection- tai muita syötteen käsittelyyn liittyviä haavoittuvuuksia.

Täydellinen ZAP-raportti löytyy tiedostosta **zap_report_round4.md**.
[Katso ZAP-raportti](./zap_report_round4.md)

---

## 6. Loppuyhteenveto
Testauksen perusteella Booking System (Phase 3) -sovelluksessa on useita vakavia autorisointiin ja tietosuojaan liittyviä puutteita.  
Merkittävin löydös on IDOR-haavoittuvuus, jonka vuoksi kuka tahansa voi hakea varausten sisältöä ilman kirjautumista. Lisäksi kaikki varaukset näkyvät etusivulla käyttäjästä riippumatta, mikä rikkoo GDPR:n vaatimusta henkilötietojen minimoinnista.

Admin-rooli on toteutettu vain osittain eikä vastaa järjestelmän spesifikaatioita. Admin ei voi hallita käyttäjiä ja resurssien hallinta on vajaa (voi vain lisätä), eikä backendissä ole roolipohjaista autorisointia.  
Reserver-rooli taas sisältää liikaa oikeuksia (kuten resurssien luonnin), eikä estä muiden varausten tarkastelua.

Fuzzing-työkalut eivät löytäneet uusia endpointteja, koska sovellus ei palauta 404-koodeja. Niiden avulla löydetty IDOR vahvisti kuitenkin, että backend ei tee asianmukaisia autorisointitarkastuksia.

Sovellus ei tällä hetkellä täytä Privacy by Design -periaatteita eikä asiakkaan vaatimuksia. Autorisointi vaatii merkittävän uudistuksen sekä UI- että API-tasolla.

