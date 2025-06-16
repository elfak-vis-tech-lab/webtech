# JSON format - Detaljno objašnjenje

## Šta je JSON?

**JSON (_JavaScript Object Notation_)** je format za razmenu podataka koji je lako čitljiv i za ljude i za mašine. Uprkos tome što potiče iz JavaScript-a, JSON je potpuno nezavisan od programskog jezika i koristi se u gotovo svim modernim programskim jezicima.

## Osnovna sintaksa JSON-a

JSON se zasniva na dva osnovna elementa:
- **Kolekcija parova naziv/vrednost** (kao objekti, mape ili rečnici)
- **Uređena lista vrednosti** (kao nizovi ili liste)

### Osnovna pravila sintakse:
- Podaci su u dati parovima naziv/vrednost (engl. _key/value_)
- Podaci su razdvojeni zarezima
- Objekti su u vitičastim zagradama `{}`
- Nizovi su u uglastim zagradama `[]`
- Stringovi moraju biti u dvostrukim navodnicima `""`

## JSON tipovi podataka

### 1. String (Tekst)
```json
{
  "ime": "Marko",
  "prezime": "Petrović",
  "opis": "Ovo je string sa \"navodnicima\" i \\ backslash"
}
```

### 2. Number (Broj)
```json
{
  "godine": 25,
  "visina": 1.75,
  "temperatura": -5,
  "naucniBroj": 1.23e-4,
  "velikiBroj": 1.23E+10
}
```

JSON podržava:
- Cele brojeve: `42`, `-17`
- Decimalne brojeve: `3.14`, `-0.001`
- Eksponencijalni zapis: `1e-10`, `1.23E+4`

### 3. Boolean (Logička vrednost)
```json
{
  "aktivan": true,
  "obrisan": false,
  "verifikovan": true
}
```

### 4. null (Prazna vrednost)
```json
{
  "srednjeIme": null,
  "datumBrisanja": null
}
```

### 5. Object (Objekat)
```json
{
  "korisnik": {
    "id": 123,
    "ime": "Ana",
    "kontakt": {
      "email": "ana@example.com",
      "telefon": "+381641234567"
    }
  }
}
```

### 6. Array (Niz)
```json
{
  "brojevi": [1, 2, 3, 4, 5],
  "imena": ["Marko", "Ana", "Petar"],
  "mesani": [1, "tekst", true, null],
  "objekti": [
    {"ime": "Marko", "godine": 25},
    {"ime": "Ana", "godine": 30}
  ]
}
```

## Složeni primer JSON strukture

```json
{
  "kompanija": {
    "naziv": "Tech Solutions d.o.o.",
    "osnovana": 2015,
    "sediste": {
      "adresa": "Knez Mihailova 42",
      "grad": "Beograd",
      "postanskiBroj": "11000",
      "zemlja": "Srbija"
    },
    "zaposleni": [
      {
        "id": 1,
        "ime": "Marko",
        "prezime": "Petrović",
        "pozicija": "Senior Developer",
        "plata": 120000,
        "aktivan": true,
        "vestine": ["JavaScript", "Python", "React"],
        "projekti": [
          {
            "naziv": "E-commerce platforma",
            "status": "završen",
            "budžet": 50000
          },
          {
            "naziv": "Mobile aplikacija",
            "status": "u toku",
            "budžet": 75000
          }
        ],
        "kontakt": {
          "email": "marko@techsolutions.rs",
          "telefon": "+381641234567",
          "linkedIn": "https://linkedin.com/in/markop"
        }
      },
      {
        "id": 2,
        "ime": "Ana",
        "prezime": "Nikolić",
        "pozicija": "UX Designer",
        "plata": 90000,
        "aktivan": true,
        "vestine": ["Figma", "Adobe XD", "Sketch"],
        "projekti": [
          {
            "naziv": "Redesign web sajta",
            "status": "planiran",
            "budžet": 25000
          }
        ],
        "kontakt": {
          "email": "ana@techsolutions.rs",
          "telefon": "+381651234567",
          "linkedIn": null
        }
      }
    ],
    "finansije": {
      "prihod2023": 500000,
      "rashod2023": 350000,
      "dobít": 150000,
      "porezi": {
        "pdv": 20,
        "porezNaDobit": 15
      }
    },
    "aktivna": true,
    "sertifikati": ["ISO 9001", "ISO 27001"]
  }
}
```

## Prednosti JSON-a

### 1. Jednostavnost
- Lako čitljiv i za ljude i za mašine
- Minimalna sintaksa
- Intuitivna struktura

### 2. Lakoća korišćenja
- Nativna podrška u JavaScript-u
- Biblioteke dostupne za sve programske jezike
- Brzo parsiranje i serijalizacija

### 3. Kompaktnost
- Manji od XML-a (20-30% manje)
- Efikasniji prenos preko mreže

### 4. Fleksibilnost
- Podržava složene strukture podataka
- Može reprezentovati većinu struktura podataka
- Lako se proširuje

### 5. Široka podrška
- Podržan u svim modernim jezicima
- Standardizovan (RFC 7159, ECMA-404)
- De facto standard za web API-je

## Najbolje prakse

### 1. Imenovanje ključeva
```json
// ✓ Dobro - camelCase
{
  "firstName": "Marko",
  "lastName": "Petrović",
  "phoneNumber": "+381641234567"
}

// ✓ Takođe dobro - snake_case (konzistentnost je ključna)
{
  "first_name": "Marko",
  "last_name": "Petrović", 
  "phone_number": "+381641234567"
}

// ✗ Loše - mešanje stilova
{
  "firstName": "Marko",
  "last_name": "Petrović",
  "phone-number": "+381641234567"
}
```

### 2. Struktura podataka
```json
// ✓ Dobro - jasna hijerarhija
{
  "korisnik": {
    "licniPodaci": {
      "ime": "Marko",
      "prezime": "Petrović"
    },
    "kontakt": {
      "email": "marko@example.com",
      "telefon": "+381641234567"
    }
  }
}

// ✗ Loše - ravna struktura
{
  "korisnikIme": "Marko",
  "korisnikPrezime": "Petrović",
  "korisnikEmail": "marko@example.com",
  "korisnikTelefon": "+381641234567"
}
```

### 3. Formatiranje za čitljivost
```json
// ✓ Dobro - formatiran JSON
{
  "korisnik": {
    "id": 123,
    "ime": "Marko",
    "aktivni_projekti": [
      {
        "id": 1,
        "naziv": "Web aplikacija"
      },
      {
        "id": 2,
        "naziv": "Mobile app"
      }
    ]
  }
}

// ✗ Loše - neformatiran JSON
{"korisnik":{"id":123,"ime":"Marko","aktivni_projekti":[{"id":1,"naziv":"Web aplikacija"},{"id":2,"naziv":"Mobile app"}]}}
```

## Zaključak

JSON je danas nezamenljiv format za razmenu podataka u modernim aplikacijama. Njegova jednostavnost, čitljivost i široka podrška čine ga idealnim izborom za web API-je, konfiguracije i skladištenje podataka.

Ključ uspešnog korišćenja JSON-a leži u razumevanju njegovih mogućnosti i ograničenja, kao i u primeni najboljih praksi za strukturiranje, validaciju i bezbednost podataka. Uprkos svojim nedostacima, JSON ostaje dominantan format za razmenu podataka u web razvoju.