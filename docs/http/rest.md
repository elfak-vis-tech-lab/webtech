# REST - Detaljno objašnjenje

## Šta je REST?

**REST (_REpresentational State Transfer_)** predstavlja softverski šablon koji je danas postao jedan od najčešće korišćenih pristupa za projektovanje web API-ja (_Application Programming Interfaces_). REST nije protokol, već skup principa - može se implementirati na mnogo različitih načina. API koji poštuje principe i stilove koje definiše REST se naziva **REST API** ili **RESTful API**.

REST je kreirao Roj Filding (Roy Fielding) 2000. godine u svojoj doktorskoj disertaciji. Osnovna ideja je da se web aplikacije projektuju kao skup resursa koji mogu biti identifikovani, pristupljeni i manipulisani putem standardnih HTTP metoda.

## Ključni principi REST-a

### 1. Uniforman interfejs (Uniform Interface)

Ovaj princip zahteva jedinstven način identifikacije i manipulacije resursima kroz ceo sistem. Uniforman interfejs se sastoji od četiri komponente:

- **Identifikacija resursa** - Svaki resurs mora imati jedinstvenu identifikaciju (obično URL)
- **Manipulacija resursa kroz reprezentacije** - Klijent manipuliše resursima slanjem reprezentacija (JSON, XML, HTML)

**Primer:**
```http
GET /api/korisnici/123        # Dobijanje korisnika sa ID 123
POST /api/korisnici           # Kreiranje novog korisnika
PUT /api/korisnici/123        # Ažuriranje korisnika 123
DELETE /api/korisnici/123     # Brisanje korisnika 123
```

### 2. Klijent-Server (Client-Server)

Ovaj princip zahteva jasno razdvajanje odgovornosti između klijenta i servera:

- **Klijent** - Odgovoran za korisnički interfejs i korisničko iskustvo
- **Server** - Odgovoran za skladištenje podataka, poslovnu logiku i obradu zahteva

Ova separacija omogućava:
- Nezavisan razvoj klijenta i servera
- Različite klijente mogu koristiti isti server
- Lakše skaliranje i održavanje

### 3. Stateless (Bez stanja)

Server ne čuva kontekst između zahteva - svaki klijentski zahtev mora sadržavati sve neophodne informacije za njegovu obradu.

**Prednosti:**
- Lakše skaliranje servera
- Veća pouzdanost
- Jednostavnija implementacija

**Nedostaci:**
- Povećan saobraćaj (svaki zahtev mora nositi sve informacije)
- Složeniji klijent

**Primer stateless zahteva:**
```http
GET /api/korisnici/123
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Content-Type: application/json
```

### 4. Keširanje (Cacheable)

Odgovori servera treba da budu označeni kao kešabilni ili ne-kešabilni. Klijent može čuvati (keširati) odgovore servera za kasniju upotrebu.

**HTTP zaglavlja za keširanje:**
- `Cache-Control: max-age=3600` - Kešira se 1 sat
- `Cache-Control: no-cache` - Ne kešira se
- `ETag: "123456"` - Verzija resursa za uslovni keširanje

### 5. Slojevita arhitektura (Layered System)

Sistem može biti organizovan u hierarhijske slojeve, gde svaki sloj može videti samo sloj direktno ispod sebe.

**Primer slojeva:**
- Sloj bezbednosti (autentikacija, autorizacija)
- Sloj keširanja 
- Sloj balansiranja opterećenja
- Aplikacioni sloj

### 6. Kod na zahtev (Code on Demand) - Opciono

Server može poslati izvršni kod klijentu (JavaScript, apleti). Ovo je jedini opcioni princip.

## HTTP metode u REST-u

REST API-ji koriste standardne HTTP metode:

### GET - Čitanje resursa
```http
GET /api/knjige           # Sve knjige
GET /api/knjige/5         # Knjiga sa ID 5
GET /api/knjige?autor=Pekic  # Knjige autora Pekić
```

### POST - Kreiranje novog resursa
```http
POST /api/knjige
Content-Type: application/json

{
  "naslov": "Atlantida",
  "autor": "Borislav Pekić",
  "godina": 1988
}
```

### PUT - Ažuriranje resursa
```http
PUT /api/knjige/5
Content-Type: application/json

{
  "naslov": "Atlantida - novo izdanje",
  "autor": "Borislav Pekić", 
  "godina": 2020
}
```

### DELETE - Brisanje resursa
```http
DELETE /api/knjige/5
```

## Prednosti REST-a

1. **Jednostavnost** - Koristi postojeće HTTP protokol i metode
2. **Skalabilnost** - Stateless priroda omogućava lakše skaliranje
3. **Fleksibilnost** - Podržava različite formate podataka (JSON, XML, HTML)
4. **Interoperabilnost** - Platformski nezavisan
5. **Keširanje** - Ugrađena podrška za keširanje
6. **Razdvojene odgovornosti** - Jasna separacija klijent-server

## Nedostaci REST-a

1. **Over-fetching/Under-fetching** - Možda dobijete više ili manje podataka nego što vam treba
2. **Više poziva** - Ponekad potrebno više API poziva za kompleksne operacije  
3. **Nekonzistentnost** - Različite implementacije mogu biti nekonzistentne
4. **Ograničenost HTTP metoda** - Samo nekoliko standardnih operacija

## Najbolje prakse

### 1. Korišćenje imenica za resurse
```
/api/korisnici      # DOBRO
/api/getKorisnici   # LOŠE
```

### 2. Hijerarhijski URL-ovi
```
/api/korisnici/123/narudzbine/456
```

### 3. Verzioniranje API-ja
```
/api/v1/korisnici
/api/v2/korisnici
```

### 4. Filtriranje i sortiranje
```
/api/knjige?autor=Pekic&sortBy=godina&order=desc
```

### 5. Paginacija
```
/api/knjige?page=2&limit=10
```

## Zaključak

REST je danas dominantan pristup za kreiranje web API-ja zbog svoje jednostavnosti, fleksibilnosti i široke podrške. Iako ima svoja ograničenja, REST principi pružaju solidnu osnovu za dizajniranje skalabilnih i održivih web servisa. Razumevanje REST-a je ključno za moderne web developere i arhitekte softverskih sistema.

## Primer za vežbu: Mini društvena mreža

![Šema baze podataka](rest-example.png)

Pravimo serverski REST API za malu društvenu mrežu. U bazi čuvamo sledeće podatke (tabele):
- Users (korisnici)
- Posts (objave)
- Comments (komentari)

Svaki korisnik može da ima više objava i svaka objava može da ima više komentara.

Svaki podatak u bazi je resurs:
- Lista korisnika mreže
- Informacije o Petru Petroviću
- Objave Petra Petrovića
- Komentari na objavu čiji je ID=573
- ...

Potrebno je obezbediti da se svim resursima pristupa na jedinstven i uniforman način. Ovo se obezbeđuje dodeljivanjem jedinstvenog URL-a svakom resursu, pri čemu se slanjem odgovarajućeg zahteva na određeni URL interaguje sa njim. Na primer:
- Slanjem GET zahteva na URL nekog korisnika dobijamo podatke o njemu
- Slanjem POST zahteva na URL objave možemo kreirati novu objavu
- Slanjem PUT zahteva na URL objave menjamo njen sadržaj
- Slanjem DELETE zahteva na URL komentara ga brišemo

![Struktura REST URL-a](rest-url.png)

### Primeri

```sh
GET https://nasamreza.com/users             # lista svih korisnika
GET https://nasamreza.com/users/1           # korisnik sa ID=1
POST https://nasamreza.com/users            # kreiranje novog korisnika (podaci u telu poruke)
PUT https://nasamreza.com/users/1           # ažuriranje informacija o korisniku sa ID=1
GET https://nasamreza.com/users/1/posts     # lista svih postova korisnika sa ID=1
GET https://nasamreza.com/posts             # lista svih postova 
POST https://nasamreza.com/posts            # kreiranje novog posta
POST https://nasamreza.com/posts/1/comments # dodavanje komentara na post sa ID=1
DELETE https://nasamreza.com/comments/2     # brisanje komentara sa ID=2

```


