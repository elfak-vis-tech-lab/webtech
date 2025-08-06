# Osnove JavaScript-a

Ova lekcija pokriva osnove JavaScript-a, uz fokus na to kako se JavaScript razlikuje od C-familije jezika i na njegove jedinstvene karakteristike.

## Promenljive i deklaracija

JavaScript ima tri načina za deklarisanje varijabli, ali danas se gotovo uvek koriste `let` i `const`. Ovo je važna razlika u odnosu na C/C++ gde se tip eksplicitno deklariše - u JavaScript-u se tipovi dodeljuju **dinamički, u toku izvršenja**.

```javascript
// Blok-ograničena, promenljiva
let godine = 25;
godine = 26; // OK

// Blok-ograničena, nepromenjiva veza
const ime = 'Ana';
// ime = "Marko"; // Greška! Ne možemo ponovo dodeliti

// Funkcijski-ograničena (legacy, izbegavati u modernom kodu)
// var može izazvati neočekivana ponašanja, jer ima drugačiji scope u odnosu na let i const
// Scope kod let i const je ograničen na nivou bloka, kao kod većine programskih jezika.
var stariStil = 'izbegavati ovo';
```

**Ključna razlika u odnosu na C-familiju:** JavaScript promenljive su dinamički tipizovane - tip se ne deklariše eksplicitno.

## Tipovi podataka

JavaScript ima nekoliko primitivnih tipova i objekte. Za razliku od jezika kao što su C++ ili Java, JavaScript ima samo jedan numerički tip (ne pravi se razlika između celih i decimalnih brojeva).

### Primitivni tipovi

```javascript
// Brojevi (nema zasebnih int/float kao u C/Java) - tip je "number"
let ceobroj = 42;
let decimalni = 3.14;
let eksponencijalni = 2.5e6; // 2,500,000

// Stringovi (nepromenjivi, za razliku od C++ std::string) - tip je "string"
let pozdrav = 'Zdravo';
let sablon = `Zdravo ${pozdrav}!`; // Koristimo backticks (`) umesto navodnika (' ili ")
// pozdrav[0] = 'z'; // Neće raditi! Stringovi su nepromenjivi

// Boolean vrednosti - tip je "boolean"
let jeAktivan = true;
let jeZavrsen = false;

// Specijalne vrednosti
let nista = null; // Null predstavlja validnu vrednost, ali bez sadržaja
let nijeDefinisano = undefined; // promenljiva postoji ali nema vrednost
let nijeBroj = NaN; // Rezultat nevalidnih matematičkih operacija

console.log(typeof 42); // "number"
console.log(typeof 'zdravo'); // "string"
console.log(typeof true); // "boolean"
console.log(typeof undefined); // "undefined"
```

Obratiti pažnju na razlike u ponašanju između `null` i `undefined`. `null` je eksplicitna vrednost koja označava "nema vrednosti", dok `undefined` znači da promenljiva nije inicijalizovana.

### Pretvaranje tipova i jednakost

JavaScript ima "slabu" (`==`) i strogu (`===`) jednakost. Ovo je jedna od najvažnijih razlika u odnosu na C-familiju jezika gde `==` uvek poredi vrednosti bez konverzije tipova.

```javascript
// Slaba jednakost (vrši konverziju tipova)
console.log(5 == '5'); // true (string konvertovan u broj)
console.log(true == 1); // true (boolean konvertovan u broj)
console.log(null == undefined); // true (specijalan slučaj)

// Stroga jednakost (bez konverzije tipova)
console.log(5 === '5'); // false
console.log(true === 1); // false
console.log(null === undefined); // false

// Isto važi i za nejednakost
console.log(5 != '5'); // false
console.log(5 !== '5'); // true
```

**Najbolja praksa:** Uvek koristiti `===` i `!==` da bi se izbeglo neočekivano ponašanje.

**Primer _čudnog_ ponašanja prilikom korišćenja `==`:**

```javascript
console.log(0 == ''); // true
console.log(0 == '0'); // true
console.log('' == '0'); // false
```

## Scope

JavaScript koristi blok scope za `let` i `const`. Ovo je slično C++ blok scope-u. Ovo ne važi i za `var` (zbog toga je poželjno izbegavati).

```javascript
function demonstrirajScope() {
	const globalnaVar = 'Ja sam u scope-u funkcije';

	if (true) {
		let blokVar = 'Ja sam u blok scope-u';
		const josBlokovaVar = 'I ja takođe';
		console.log(globalnaVar); // Dostupno
		console.log(blokVar); // Dostupno
	}

	// console.log(blokVar);         // Greška! Nije dostupno
	console.log(globalnaVar); // I dalje dostupno

	for (let i = 0; i < 3; i++) {
		// i je dostupno samo unutar ove petlje
	}
	// console.log(i);              // Greška! i nije dostupno
}

demonstrirajScope();
```

**Izlaz:**

```
Ja sam u scope-u funkcije
Ja sam u blok scope-u
Ja sam u scope-u funkcije
```

## Funkcije

JavaScript funkcije se ponašaju kao objekti, što znači da mogu biti smeštene u promenljive, prosleđene kao argumenti i vraćene iz drugih funkcija. Ovo je značajna razlika u odnosu na C/C++ gde su funkcije samo pokazivači.

```javascript
// Deklaracija funkcije
function pozdravi(ime) {
	return `Zdravo, ${ime}!`;
}

// Funkcija kao izraz (funkcija dodeljena varijabli)
const oprosti = function (ime) {
	return `Zbogom, ${ime}!`;
};

// Arrow funkcije (ES6+)
const dobrodosli = (ime) => {
	return `Dobrodošli, ${ime}!`;
};

// Kompaktna arrow funkcija (implicitni return)
const vikni = (ime) => `HEJ ${ime.toUpperCase()}!`;

console.log(pozdravi('Ana')); // Zdravo, Ana!
console.log(oprosti('Marko')); // Zbogom, Marko!
console.log(dobrodosli('Petar')); // Dobrodošli, Petar!
console.log(vikni('milice')); // HEJ MILICE!
```

**Izlaz:**

```
Zdravo, Ana!
Zbogom, Marko!
Dobrodošli, Petar!
HEJ MILICE!
```

## Petlje

JavaScript podržava poznate konstrukte petlji sa nekim jedinstvenim varijacijama. `for...of` i `for...in` petlje su specifične za JavaScript i razlikuju se od običnih for petlji.

```javascript
// Tradicionalna for petlja
for (let i = 0; i < 3; i++) {
	console.log(`Tradicionalna: ${i}`);
}

// for...of petlja (iterira preko vrednosti)
const boje = ['crvena', 'zelena', 'plava'];
for (const boja of boje) {
	console.log(`Boja: ${boja}`);
}

// for...in petlja (iterira preko ključeva/indeksa)
for (const indeks in boje) {
	console.log(`Indeks ${indeks}: ${boje[indeks]}`);
}

// while petlja
let brojac = 0;
while (brojac < 2) {
	console.log(`While: ${brojac}`);
	brojac++;
}
```

**Izlaz:**

```
Tradicionalna: 0
Tradicionalna: 1
Tradicionalna: 2
Boja: crvena
Boja: zelena
Boja: plava
Indeks 0: crvena
Indeks 1: zelena
Indeks 2: plava
While: 0
While: 1
```

## Objekti

JavaScript objekti su kolekcije ključ-vrednost parova, slično mapama ili rečnicima (dictionary) u drugim jezicima. Za razliku od C++ struktura ili klasa, JavaScript objekti su potpuno dinamički. Metode i svojstva se mogu dodavati ili menjati u toku izvršavanja.

```javascript
// Literal sintaksa objekta
const osoba = {
	ime: 'Ana',
	godine: 30,
	jeZaposlena: true,
	// Metode
	pozdravi: function () {
		return `Ćao, ja sam ${this.ime}`;
	},
	// Skraćena sintaksa metode
	predstaviSe() {
		return `Ja sam ${this.ime}, imam ${this.godine} godina`;
	},
};

console.log(osoba.ime); // Ana
console.log(osoba['godine']); // 30 (uglaste zagrade notacija)
console.log(osoba.pozdravi()); // Ćao, ja sam Ana
console.log(osoba.predstaviSe()); // Ja sam Ana, imam 30 godina

// Dodavanje svojstava dinamički
osoba.grad = 'Beograd';
osoba['zemlja'] = 'Srbija';

console.log(osoba.grad); // Beograd
```

**Izlaz:**

```
Ana
30
Ćao, ja sam Ana
Ja sam Ana, imam 30 godina
Beograd
```

## Nizovi

JavaScript nizovi su dinamički i mogu sadržavati mešovite tipove, što je drugačije od statičkih nizova u C/C++. Veličina niza se ne mora specificirati unapred i može se menjati tokom izvršavanja.

```javascript
// Kreiranje niza
const brojevi = [1, 2, 3, 4, 5];
const mesovito = [1, 'zdravo', true, null, { kljuc: 'vrednost' }];

console.log(brojevi.length); // 5
console.log(mesovito[1]); // zdravo

// Nizovi su objekti
console.log(typeof brojevi); // object
console.log(Array.isArray(brojevi)); // true
```

**Izlaz:**

```
5
zdravo
object
true
```

### Ugrađene metode nizova

JavaScript nizovi dolaze sa velikim setom ugrađenih metoda koje čine rad sa njima mnogo lakšim nego u C/C++.

```javascript
const voce = ['jabuka', 'banana', 'trešnja'];

// Dodavanje elemenata
voce.push('urma'); // Dodaj na kraj
voce.unshift('kajsija'); // Dodaj na početak
console.log(voce); // ["kajsija", "jabuka", "banana", "trešnja", "urma"]

// Uklanjanje elemenata
const poslednjeVoce = voce.pop(); // Ukloni sa kraja
const prvoVoce = voce.shift(); // Ukloni sa početka
console.log(poslednjeVoce); // urma
console.log(prvoVoce); // kajsija
console.log(voce); // ["jabuka", "banana", "trešnja"]

// Pronalaženje elemenata
console.log(voce.indexOf('banana')); // 1
console.log(voce.includes('grožđe')); // false

// Isecanje (ne menja originalni niz)
const isecak = voce.slice(1, 3); // Od indeksa 1 (inkluzivno) do 3 (ekskluzivno)
console.log(isecak); // ["banana", "trešnja"]
console.log(voce); // ["jabuka", "banana", "trešnja"] (nepromenjeno)

// Kopiranje niza
const kopija = [...voce]; // Spread operator
// const kopija = voce.slice(); // Drugi način
console.log(kopija); // ["jabuka", "banana", "trešnja"]

// Spajanje nizova
const drugiNiz = ['grožđe', 'breskva'];
const spojeniNiz = [...voce, ...drugiNiz];
// const spojeniNiz = voce.concat(drugiNiz); // Drugi način
console.log(spojeniNiz); // ["jabuka", "banana", "trešnja", "grožđe", "breskva"]

// Niz unutar niza
const ugnjezdeniNiz = [voce, drugiNiz]; // nije isto što i [...voce, ...drugiNiz]
console.log(ugnjezdeniNiz); // [["jabuka", "banana", "trešnja"], ["grožđe", "breskva"]]
```

### Operacije nad nizovima bez ugrađenih metoda

U nastavku slede implementacije čestih operacija nad nizovima bez korišćenja ugrađenih metoda:

```javascript
// Pronađi maksimalnu vrednost
function nadjiMaks(niz) {
	if (niz.length === 0) return undefined;

	let maks = niz[0];
	for (let i = 1; i < niz.length; i++) {
		if (niz[i] > maks) {
			maks = niz[i];
		}
	}
	return maks;
}

// Obrni niz (menjamo postojeći niz, ne kreiramo novi)
function obrniNiz(niz) {
	for (let i = 0; i < Math.floor(niz.length / 2); i++) {
		const temp = niz[i];
		niz[i] = niz[niz.length - 1 - i];
		niz[niz.length - 1 - i] = temp;
	}
	return niz;
}

// Filtriraj parne brojeve
function filtrirajParne(niz) {
	const rezultat = [];
	for (let i = 0; i < niz.length; i++) {
		if (niz[i] % 2 === 0) {
			rezultat[rezultat.length] = niz[i]; // Isto kao rezultat.push(niz[i])
		}
	}
	return rezultat;
}

// Ukloni duplikate iz niza
function ukloniDuplikate(niz) {
	const rezultat = [];

	for (let i = 0; i < niz.length; i++) {
		let postoji = false;

		// Proveravamo da li se element već nalazi u rezultatu
		for (let j = 0; j < rezultat.length; j++) {
			if (niz[i] === rezultat[j]) {
				postoji = true;
				break;
			}
		}

		// Ako ne postoji, dodajemo ga u rezultat
		if (!postoji) {
			rezultat.push(niz[i]);
		}
	}

	return rezultat;
}

const testNiz = [3, 1, 4, 1, 5, 9, 2, 6];
console.log('Originalni:', testNiz);
console.log('Maks:', nadjiMaks(testNiz)); // 9
console.log('Parni brojevi:', filtrirajParne(testNiz)); // [4, 2, 6]

const zaOkretanje = [1, 2, 3, 4, 5];
console.log('Pre okretanja:', zaOkretanje);
console.log('Posle okretanja:', obrniNiz([...zaOkretanje])); // [5, 4, 3, 2, 1]

const niz = [1, 2, 2, 3, 4, 4, 5];
const bezDuplikata = ukloniDuplikate(niz);
console.log(bezDuplikata); // [1, 2, 3, 4, 5]
```

## Osnove funkcionalnog programiranja

JavaScript podržava paradigme funkcionalnog programiranja sa funkcijama višeg reda.

### Map, Filter, Reduce

Map, Filter i Reduce su tri metode za rad sa nizovima koje se često navode kao osnove funkcionalnog programiranja u JavaScript-u i omogućavaju elegantnu obradu podataka.

-   `map` transformiše svaki element niza. Kao argument prihvata funkciju koja se primenjuje nad svakim elementom.
-   `filter` selektuje elemente koji zadovoljavaju određeni uslov. Kao argument prihvata funkciju koja vraća `true` ili `false`.
-   `reduce` kombinuje sve elemente niza u jednu vrednost. Kao argument prihvata funkciju koja prima akumulator i trenutni element, i vraća novu vrednost akumulatora.

Ove metode se mogu ulančavati, što omogućava elegantno i čitljivo pisanje koda. Svaka od ovih metoda **ne menja originalnu, već vraća novi niz**.

```javascript
const brojevi = [1, 2, 3, 4, 5];

// Map: transformiši svaki element
const duplirani = brojevi.map((x) => x * 2);
console.log('Duplirani:', duplirani); // [2, 4, 6, 8, 10]

// Filter: selektuj elemente koji zadovoljavaju kriterijum
const parni = brojevi.filter((x) => x % 2 === 0);
console.log('Parni:', parni); // [2, 4]

// Reduce: kombinuj sve elemente u jednu vrednost
const suma = brojevi.reduce((acc, curr) => acc + curr, 0);
console.log('Suma:', suma); // 15

// Ulančavanje operacija (zbir kvadrata svih brojeva većih od 2)
const rezultat = brojevi
	.filter((x) => x > 2) // [3, 4, 5]
	.map((x) => x * x) // [9, 16, 25]
	.reduce((acc, curr) => acc + curr, 0); // 50

console.log('Ulančani rezultat:', rezultat); // 50
```


### Funkcije višeg reda (napredniji primeri)

Funkcije višeg reda su funkcije koje primaju druge funkcije kao parametre ili vraćaju funkcije kao rezultat. Ovo omogućava kreiranje fleksibilnih i ponovo upotrebljivih funkcija. Map, Filter i Reduce su primeri funkcija višeg reda.

```javascript
// Funkcija koja vraća funkciju
function kreirajMnozilac(faktor) {
	return function (broj) {
		return broj * faktor;
	};
}

const dupliraj = kreirajMnozilac(2);
const utrostruci = kreirajMnozilac(3);

console.log(dupliraj(5)); // 10
console.log(utrostruci(4)); // 12

// Funkcija koja prima funkciju kao parametar
function ponoviOperaciju(puta, operacija) {
	let rezultat = 1;
	for (let i = 0; i < puta; i++) {
		rezultat = operacija(rezultat);
	}
	return rezultat;
}

const dodajJedan = (x) => x + 1;
const pomnoziSaDva = (x) => x * 2;

console.log(ponoviOperaciju(3, dodajJedan)); // 4 (1+1+1+1)
console.log(ponoviOperaciju(3, pomnoziSaDva)); // 8 (1*2*2*2)
```


## Ključne razlike u odnosu na C

### Nepromenjivost stringova

Za razliku od C++ gde možete direktno menjati karaktere string-a, JavaScript stringovi su nepromenjivi. Ovo znači da svaka "izmena" stringa stvara novi string.

```javascript
let str = 'zdravo';
// str[0] = 'Z'; // Ovo neće raditi!

// Umesto toga, kreiraj novi string
str = 'Z' + str.slice(1); // "Zdravo"
console.log(str); // Zdravo
```

### Dinamička tipizacija

Promenljive mogu menjati tipove tokom izvršavanja programa, što je značajna razlika u odnosu na statičko tipizovane jezike poput C/C++.

```javascript
let promenljiva = 42; // broj
promenljiva = 'zdravo'; // sada string
promenljiva = [1, 2, 3]; // sada niz
console.log(typeof promenljiva); // object
```

### Truthy/Falsy vrednosti

JavaScript ima implicitnu boolean konverziju, što znači da se vrednosti automatski tretiraju kao true ili false u boolean kontekstu.

```javascript
// Falsy vrednosti: false, 0, "", null, undefined, NaN
if (0) console.log('Neće se ispisati');
if ('') console.log('Neće se ispisati');
if (null) console.log('Neće se ispisati');

// Truthy vrednosti: sve ostalo
if (1) console.log('Ispisaće se'); // Ispisaće se
if ('zdravo') console.log('Ispisaće se'); // Ispisaće se
if ([]) console.log('Ispisaće se'); // Ispisaće se (prazan niz je truthy!)
```

