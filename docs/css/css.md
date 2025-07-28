# CSS Pregled

CSS (Cascading Style Sheets) je jezik za stilizovanje koji se koristi za opisivanje prezentacije HTML dokumenata. Kontroliše kako se elementi prikazuju na ekranu, u štampi ili u drugim medijima. CSS razdvaja sadržaj (HTML) od prezentacije, čineći veb sajtove lakšim za održavanje i fleksibilnijim.

Termin "kaskadni" se odnosi na način na koji se stilovi primenjuju - ako postoji više pravila za isti element, CSS koristi hijerarhiju da odredi koje pravilo ima prednost.

## CSS Selektori

Selektori su osnova CSS-a - oni određuju nad kojim HTML elementima se stilovi primenjuju.

### Osnovni Selektori

**Selektor Elementa (Type Selector)**

```css
p {
	color: blue;
}
```

Ovaj selektor bira sve `<p>` elemente na stranici. Koristi se kada želimo da stilizujemo sve elemente određenog tipa.

**Selektor Klase (Class Selector)**

```css
.highlight {
	background-color: yellow;
}
```

Selektor klase počinje tačkom (.) i bira sve elemente koji imaju odgovarajući `class` atribut. Na primer, `<span class="highlight">tekst</span>`. Klase se mogu koristiti više puta na stranici i jedan element može imati više klasa.

```css
/* Element sa više klasa */
.btn.primary.large {
	/* Bira elemente koji imaju sve tri klase */
}

.btn .large .primary {
	/* Bira elemente .primary  koji su unutar .large, a large unutar .btn */
}
```

**Selektor ID-ja (ID Selector)**

```css
#header {
	font-size: 24px;
}
```

Selektor ID-ja počinje znakom # i bira element sa odgovarajućim `id` atributom. ID mora biti jedinstven na stranici. Ima najveću specifičnost među osnovnim selektorima.

**Univerzalni Selektor (Universal Selector)**

```css
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
```

Označava se zvezdicom (\*) i bira SVE elemente na stranici. Često se koristi za reset stilova ili primenu osnovnih stilova nad svim elementima.

### Selektori Atributa (Attribute Selectors)

Ovi selektori omogućavaju biranje elemenata na osnovu njihovih atributa i vrednosti.

```css
/* Elementi sa određenim atributom */
input[required] {
	border: 2px solid red;
}

/* Elementi sa određenom vrednošću atributa */
input[type='email'] {
	border: 2px solid blue;
	background-image: url('email-icon.png');
}

/* Atribut sadrži određenu vrednost */
a[href*='example'] {
	color: red;
	font-weight: bold;
}

/* Atribut počinje određenom vrednošću */
img[src^='https'] {
	border: 1px solid green;
}

/* Atribut završava određenom vrednošću */
a[href$='.pdf'] {
	background-image: url('pdf-icon.png');
}
```

### Kombinatori (Combinators)

Kombinatori omogućavaju kombinovanje selektora da bismo ciljali elemente na osnovu njihovog odnosa u HTML strukturi.

**Descendant Combinator (Razmak)**

```css
article p {
	line-height: 1.6;
	color: #333;
}
```

Bira sve `<p>` elemente koji se nalaze BILO GDE unutar `<article>` elementa, bez obzira na to koliko su duboko ugniježđeni.

**Child Combinator (>)**

```css
nav > ul {
	list-style: none;
	margin: 0;
}

/* Ovo će uticati samo na direktnu decu */
.menu > li {
	display: inline-block;
}
```

Bira elemente koji su DIREKTNA DECA roditeljskog elementa. Mnogo je specifičniji od descendant kombinatora.

**Adjacent Sibling Combinator (+)**

```css
h2 + p {
	font-weight: bold;
	margin-top: 0;
}
```

Bira element koji NEPOSREDNO sledi nakon određenog elementa na istom nivou hijerarhije.

**General Sibling Combinator (~)**

```css
h2 ~ p {
	margin-top: 1em;
	color: #666;
}
```

Bira sve elemente koji slede nakon određenog elementa na istom nivou hijerarhije (ne moraju biti neposredni susedi).

### Pseudo-klase i Pseudo-elementi

**Pseudo-klase** se koriste za stilizovanje određenih stanja elemenata.

```css
/* Stanja linkova */
a:link {
	color: blue;
	text-decoration: none;
}

a:visited {
	color: purple;
}

a:hover {
	color: red;
	text-decoration: underline;
}

a:active {
	color: orange;
}

/* Strukturne pseudo-klase */
li:first-child {
	font-weight: bold;
	border-top: none;
}

li:last-child {
	border-bottom: none;
}

li:nth-child(odd) {
	background-color: #f9f9f9;
}

li:nth-child(3n) {
	/* Svaki treći element */
	background-color: lightblue;
}

/* Pseudo-klase za forme */
input:focus {
	outline: 2px solid blue;
	background-color: lightyellow;
}

input:invalid {
	border-color: red;
}

input:valid {
	border-color: green;
}

/* Pseudo-klase za sadržaj */
p:empty {
	display: none;
}

div:not(.hidden) {
	display: block;
}
```

**Pseudo-elementi** omogućavaju stilizovanje određenih delova elemenata.

```css
/* Kreiranje sadržaja pre i posle elementa */
.quote::before {
	content: "' ";
	font-size: 2em;
	color: #999;
	vertical-align: top;
}

.quote::after {
	content: " '";
	font-size: 2em;
	color: #999;
}

/* Prvi red paragrafa */
p::first-line {
	font-weight: bold;
	color: #333;
}

/* Prvi karakter paragrafa */
p::first-letter {
	font-size: 3em;
	float: left;
	line-height: 1;
	margin-right: 5px;
}

/* Selekcija teksta */
::selection {
	background-color: yellow;
	color: black;
}

/* Placeholder tekst u input poljima */
input::placeholder {
	color: #999;
	font-style: italic;
}
```

### Kombinovanje selektora (napredniji primeri)

1.  `.a + .b.c > .d` - selektuje element koji pripada klasi `d`, koji je direktan potomak elementa koji pripada klasama `b` i `c`, a koji je neposredni sused elementa koji pripada klasi `a`.

    ```html
    <div class="a"></div>
    <div class="b c">
    	<div class="d">Selected!</div>
    </div>
    ```

2.  `ul > li.active + li.highlight > span.badge` - selektuje `span` element sa klasom `badge`, koji je direktan potomak `<li class="highlight">`, a koji je neposredni sused `<li class="active">` , pri čemu su oba `li` elementa direktni potomci `ul` elementa.

    ```html
    <ul>
    	<li class="active"></li>
    	<li class="highlight">
    		<span class="badge">Selected</span>
    	</li>
    </ul>
    ```

3.  `form#login .field.error input:focus` - selektuje `input` element koji je trenutni u fokusus, koji se nalazi unutar elementa koji pripada klasama `field` i `error`, pri čemu se ovaj element nalazi unutar `<form id="login">`.

    ```html
    <form id="login">
    	<div class="field error">
    		<input type="text" />
    	</div>
    </form>
    ```

4.  `nav > ul li.dropdown:hover > ul li > a.active` - selektuje `a` element koji pripada klasi `active`, koji je direktan potomak `li` elementa, a koji se nalazi unutar `ul` elementa, pri čemu je ovaj (`ul`) element direktan potomak `li` elementa sa klasom `dropdown` (sa pseudoklasom `:hover`), koji se nalazi unuar `ul` elementa koji je direktan potomak `nav` elementa.

    ```html
    <nav>
    	<ul>
    		<li class="dropdown">
    			<a>Menu</a>
    			<ul>
    				<li><a class="active">Subitem</a></li>
    			</ul>
    		</li>
    	</ul>
    </nav>
    ```

5.  `.table > tbody > tr:nth-child(odd) > td:first-child` - selektuje prvi `td` element koji je direktan potomak neparnog `tr` elementa unutar `tbody` elementa, koji je direktan potomak elementa sa klasom `table`.

        ```html
        <table class="table">
        	<tbody>
        		<tr><td>Row 1</td></tr>
        		<tr><td>Row 2</td></tr>
        	</tbody>
        </table>

        ```

    <style>
    	.table > tbody > tr:nth-child(odd) > td:first-child {
      background: #00ff1aff;
    }
    </style>
    <table class="table">
    	<tbody>
    		<tr><td>(1,1)</td><td>(1,2)</td><td>(1,3)</td></tr>
    		<tr><td>(2,1)</td><td>(2,2)</td><td>(2,3)</td></tr>
    		<tr><td>(3,1)</td><td>(3,2)</td><td>(3,3)</td></tr>
    		<tr><td>(4,1)</td><td>(4,2)</td><td>(4,3)</td></tr>
    	</tbody>
    </table>

## Tipovi Prikaza: Inline vs Block

### Block Elementi

Block elementi zauzimaju punu dostupnu širinu i počinju u novom redu. Ponašaju se kao "blokovi" koji se slažu jedan ispod drugog.

```css
/* Prirodno block elementi */
div,
p,
h1,
h2,
h3,
section,
article,
header,
footer,
nav {
	display: block;
}

.block-example {
	width: 300px;
	height: 100px;
	background-color: lightblue;
	margin: 10px 0;
	padding: 20px;
	border: 2px solid navy;
}

/* Karakteristike block elemenata: */
.block-characteristics {
	/* Mogu imati širinu i visinu */
	width: 100%;
	height: 200px;

	/* Margin i padding rade na svim stranama */
	margin: 20px;
	padding: 15px;

	/* Počinju u novom redu */
	display: block;
}
```

### Inline Elementi

Inline elementi zauzimaju samo potrebnu širinu i ne započinju novi red. Ponašaju se kao reči u rečenici.

```css
/* Prirodno inline elementi */
span,
a,
em,
strong,
code,
small {
	display: inline;
}

.inline-example {
	background-color: lightgreen;
	padding: 5px 10px; /* Vertikalni padding može izazvati neočekivano ponašanje */
	margin: 0 5px; /* Vertikalni margin se ignoriše */
}

/* Ograničenja inline elemenata */
.inline-limitations {
	/* Ne mogu imati širinu i visinu */
	width: 200px; /* Ovo se ignoriše */
	height: 100px; /* I ovo se ignoriše */

	/* Vertikalni margin i padding mogu izazivati neočekivano ponašanje */
	margin-top: 20px; /* Može se ignorisati */
	padding-top: 15px; /* Može preklapati druge elemente */
}
```

### Inline-Block

Kombinuje karakteristike inline i block elemenata - elementi se ponašaju kao inline u tekstu, ali mogu imati dimenzije kao block elementi.

```css
.inline-block-example {
	display: inline-block;
	width: 150px;
	height: 75px;
	background-color: lightyellow;
	margin: 5px;
	padding: 10px;
}
```

### Ostali Tipovi Prikaza

```css
/* Sakriva element potpuno */
.hidden {
	display: none; /* Element se uklanja iz dokumenta */
}

/* Element postaje nevidljiv ali zadržava prostor */
.invisible {
	visibility: hidden; /* Element zadržava svoj prostor */
}

/* Tabelarni prikaz */
.table-display {
	display: table;
}

.table-row {
	display: table-row;
}

.table-cell {
	display: table-cell;
	padding: 10px;
	border: 1px solid #ccc;
}
```

## Box Model

Svaki element u CSS-u se posmatra kao pravougaonik koji se sastoji od sadržaja (content), padding-a, border-a i margin-a.

```css
.box-model-example {
	/* Sadržaj (content) - unutrašnji deo elementa */
	width: 300px;
	height: 200px;

	/* Padding - prostor između sadržaja i border-a */
	padding: 20px; /* Svi pravci */
	/* ili specifično: */
	padding-top: 10px;
	padding-right: 15px;
	padding-bottom: 10px;
	padding-left: 15px;
	/* ili skraćeno: padding: 10px 15px; (vertikalno horizontalno) */

	/* Border - granica oko padding-a i sadržaja */
	border: 5px solid #333;
	/* ili detaljnije: */
	border-width: 5px;
	border-style: solid;
	border-color: #333;

	/* Margin - prostor van border-a */
	margin: 15px;

	background-color: lightcoral;

	/* Ukupna širina = width + padding-left + padding-right + border-left + border-right */
	/* U ovom slučaju: 300px + 40px + 10px = 350px */
}
```

### Detaljno o Padding-u

```css
.padding-examples {
	/* Različiti načini definisanja padding-a */
	padding: 20px; /* Svi pravci */
	padding: 10px 20px; /* vertikalno horizontalno */
	padding: 10px 15px 20px; /* vrh, horizontalno, dno */
	padding: 10px 15px 20px 25px; /* vrh, desno, dno, levo (clockwise) */

	/* Individualno */
	padding-top: 10px;
	padding-right: 15px;
	padding-bottom: 20px;
	padding-left: 25px;
}
```

### Detaljno o Border-u

```css
.border-examples {
	/* Osnovno */
	border: 2px solid red;

	/* Različite strane */
	border-top: 3px dashed blue;
	border-right: 1px dotted green;
	border-bottom: 5px double purple;
	border-left: 2px groove orange;

	/* Border radius za zaobljene uglove */
	border-radius: 10px;
	border-radius: 10px 15px 20px 25px; /* vrh-levo, vrh-desno, dno-desno, dno-levo */

	/* Stilovi border-a */
	border-style: solid; /* puna linija */
	border-style: dashed; /* isprekidana linija */
	border-style: dotted; /* tačkasta linija */
	border-style: double; /* dupla linija */
}
```

### Detaljno o Margin-u

```css
.margin-examples {
	/* Margin radi isto kao padding */
	margin: 20px;
	margin: 10px 20px;
	margin: 10px 15px 20px;
	margin: 10px 15px 20px 25px;

	/* Centiranje elementa */
	margin: 0 auto; /* Centrira horizontalno */

	/* Negativni margin */
	margin-top: -10px; /* Pomera element naviše */

	/* Margin collapse - važno razumeti! */
	margin-bottom: 20px; /* Ako sledeći element ima margin-top: 15px, */
	/* ukupan razmak neće biti 35px već 20px (veći od dva) */
}
```

### Box-Sizing Svojstvo

Kontroliše kako se računaju ukupna širina i visina elementa.

```css
/* Default ponašanje - content-box */
.content-box {
	box-sizing: content-box;
	width: 200px;
	padding: 20px;
	border: 5px solid black;
	/* Ukupna širina = 200px + 40px (padding) + 10px (border) = 250px */
}

/* Border-box - uključuje padding i border u širinu */
.border-box {
	box-sizing: border-box;
	width: 200px;
	padding: 20px;
	border: 5px solid black;
	/* Ukupna širina = 200px (sadržaj se smanjuje da stane) */
	/* Širina sadržaja = 200px - 40px - 10px = 150px */
}

/* Globalno postavljanje border-box (preporučeno) */
* {
	box-sizing: border-box;
}
```

<style>
.content-box {
    box-sizing: content-box;
    width: 200px;
    padding: 20px;
    border: 5px solid black;
    /* Ukupna širina = 200px + 40px (padding) + 10px (border) = 250px */
}
/* Border-box - uključuje padding i border u širinu */
.border-box {
    box-sizing: border-box;
    width: 200px;
    padding: 20px;
    border: 5px solid black;
    /* Ukupna širina = 200px (sadržaj se smanjuje da stane) */
    /* Širina sadržaja = 200px - 40px - 10px = 150px */
}
</style>
<div class="content-box" style="background: lightblue; margin-bottom: 10px;">
  Content-box (ukupno 250px širine)
</div>
<div class="border-box" style="background: lightgreen;">
  Border-box (ukupno 200px širine)
</div>

## Pozicioniranje

CSS pozicioniranje kontroliše gde se elementi pojavljuju na stranici u odnosu na normalan tok dokumenta.

```css
/* Static - default pozicioniranje */
.static-position {
	position: static; /* default vrednost */
	/* top, right, bottom, left se ignorišu */
}

/* Relative - pozicionirano u odnosu na normalnu poziciju */
.relative-position {
	position: relative;
	top: 10px; /* pomera 10px na dole od normalne pozicije */
	left: 20px; /* pomera 20px u desno od normalne pozicije */
	z-index: 1; /* kontrola slojeva */

	/* Element i dalje zauzima svoj originalni prostor u toku dokumenta */
}

/* Absolute - pozicionirano u odnosu na najbliži pozicionirani predak */
.absolute-position {
	position: absolute;
	top: 50px; /* 50px od vrha roditeljskog elementa */
	right: 30px; /* 30px od desne strane roditeljskog elementa */

	/* Element je uklonjen iz normalnog toka dokumenta */
	/* Ne utiče na poziciju drugih elemenata */
}

/* Fixed - pozicionirano u odnosu na viewport (ekran) */
.fixed-position {
	position: fixed;
	bottom: 20px;
	right: 20px;
	z-index: 1000;

	/* Element ostaje na istoj poziciji čak i kad se skroluje */
	/* Idealno za navigaciju, dugme za povratak na vrh, itd. */
}

/* Sticky - kombinacija relative i fixed */
.sticky-position {
	position: sticky;
	top: 0; /* kada element dodirne vrh viewport-a, postaje "zalepljen" */

	/* Ponaša se kao relative dok ne dodje do navedene pozicije */
	/* Onda postaje fixed */
	background-color: white;
	z-index: 10;
}

/* Primer sticky navigacije */
.sticky-nav {
	position: sticky;
	top: 0;
	background-color: white;
	box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
	z-index: 100;
}
```

<style>
/* Static - default pozicioniranje */
.static-position {
    position: static; /* default vrednost */
    /* top, right, bottom, left se ignorišu */
}

/* Relative - pozicionirano u odnosu na normalnu poziciju */
.relative-position {
    position: relative;
    top: 10px; /* pomera 10px na dole od normalne pozicije */
    left: 20px; /* pomera 20px u desno od normalne pozicije */
    z-index: 1; /* kontrola slojeva */
    
    /* Element i dalje zauzima svoj originalni prostor u toku dokumenta */
}

/* Absolute - pozicionirano u odnosu na najbliži pozicionirani predak */
.absolute-position {
    position: absolute;
    top: 50px; /* 50px od vrha roditeljskog elementa */
    right: 30px; /* 30px od desne strane roditeljskog elementa */
    
    /* Element je uklonjen iz normalnog toka dokumenta */
    /* Ne utiče na poziciju drugih elemenata */
}

/* Fixed - pozicionirano u odnosu na viewport (ekran) */
.fixed-position {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 1000;
    
    /* Element ostaje na istoj poziciji čak i kad se skroluje */
    /* Idealno za navigaciju, dugmad za povratak na vrh, itd. */
}

/* Sticky - kombinacija relative i fixed */
.sticky-position {
    position: sticky;
    top: 0; /* kada element dodirne vrh viewport-a, postaje "zakucana" */
    
    /* Ponaša se kao relative */
    /* Onda postaje fixed */
    background-color: white;
    z-index: 10;
}

/* Primer sticky navigacije */
.sticky-nav {
    position: sticky;
    top: 0;
    background-color: white;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    z-index: 100;
}

</style>
<div style="position: relative; border: 2px dashed gray; height: 300px; padding: 10px; margin-bottom: 10px; overflow: auto;">
  <b>Roditeljski element (position: relative)</b>
  <div class="static-position" style="background: #eee;">Static (default)</div>
  <div class="relative-position" style="background: lightblue;">
    Relative (pomeren 10px dole, 20px desno od svoje normalne pozicije)
  </div>
  <p>Ovaj tekst se pomera da napravi mesto za relative element.</p>
  <div class="absolute-position" style="background: lightcoral; padding: 5px; z-index:20;">
    Absolute (u odnosu na isprekidani okvir)
  </div>
<div class="fixed-position" style="background: gold; padding: 10px; z-index: 100;">position: fixed</div>
<div class="sticky-position" style="background: lightgreen; padding: 10px;">
  Ovaj element će postati "lepljiv" na vrhu kada skrolujete.
</div>
<div style="height: 500px; background: #f0f0f0; margin-top: 10px;">
  Prazan prostor za skrolovanje...

Skrolujte...

</div>
</div>

### Z-Index

```css
.layer-example {
	position: relative; /* potrebno za z-index */
	z-index: 10; /* veći broj = viši sloj */
}
```

## Media Queries

Media queries omogućavaju responzivni dizajn primenom različitih stilova za različite veličine ekrana i uređaje.

```css
/* Mobile first pristup - počinjemo sa mobilnim stilovima */
.responsive-container {
	width: 100%;
	padding: 10px;
	background-color: lightblue;
	font-size: 14px;
}

/* Tablet stilovi - 768px i veće */
@media screen and (min-width: 768px) {
	.responsive-container {
		width: 750px;
		margin: 0 auto; /* centriranje */
		padding: 20px;
		background-color: lightgreen;
		font-size: 16px;
	}
}

/* Desktop stilovi - 1024px i veće */
@media screen and (min-width: 1024px) {
	.responsive-container {
		width: 1000px;
		padding: 30px;
		background-color: lightcoral;
		font-size: 18px;
	}
}

/* Veliki ekrani - 1200px i veće */
@media screen and (min-width: 1200px) {
	.responsive-container {
		width: 1170px;
	}
}

/* Range media queries - između određenih širina */
@media screen and (min-width: 768px) and (max-width: 1023px) {
	.tablet-only {
		display: block;
	}
}

/* Visina viewport-a */
@media screen and (min-height: 600px) {
	.tall-screen-layout {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
	}
}

/* Orijentacija uređaja */
@media screen and (orientation: landscape) {
	.landscape-layout {
		display: flex;
		flex-direction: row;
	}
}

@media screen and (orientation: portrait) {
	.portrait-layout {
		display: flex;
		flex-direction: column;
	}
}

/* Gustina piksela (retina ekrani) */
@media screen and (-webkit-min-device-pixel-ratio: 2),
	screen and (min-resolution: 192dpi) {
	.high-res-image {
		background-image: url('image@2x.png');
		background-size: contain;
	}
}

/* Print stilovi */
@media print {
	.no-print {
		display: none; /* sakriva elemente pri štampanju */
	}

	body {
		font-size: 12pt;
		color: black;
		background: white;
	}

	a[href]:after {
		content: ' (' attr(href) ')'; /* prikazuje URL-ove linkova */
	}
}

/* Prefers-color-scheme - sistemska tema */
@media (prefers-color-scheme: dark) {
	.auto-theme {
		background-color: #2d3748;
		color: #f7fafc;
	}
}

@media (prefers-color-scheme: light) {
	.auto-theme {
		background-color: #f7fafc;
		color: #2d3748;
	}
}
```

## Prelazi i Animacije

```css
/* Prelazi (Transitions) */
.transition-example {
	width: 100px;
	height: 100px;
	background-color: blue;
	border-radius: 0;
	transform: scale(1) rotate(0deg);

	/* Definisanje prelaza */
	transition: all 0.3s ease-in-out;
	/* ili pojedinačno: */
	transition-property: width, height, background-color, transform;
	transition-duration: 0.3s, 0.5s, 0.2s, 0.4s;
	transition-timing-function: ease-in-out, linear, ease, cubic-bezier(0.25, 0.1, 0.25, 1);
	transition-delay: 0s, 0.1s, 0.2s, 0.3s;
}

.transition-example:hover {
	width: 150px;
	height: 150px;
	background-color: red;
	border-radius: 50%;
	transform: scale(1.2) rotate(45deg);
}

/* Različite timing funkcije */
.timing-functions {
	transition-timing-function: linear; /* konstantna brzina */
	transition-timing-function: ease; /* sporije početak i kraj */
	transition-timing-function: ease-in; /* spori početak */
	transition-timing-function: ease-out; /* spori kraj */
	transition-timing-function: ease-in-out; /* spori početak i kraj */
	transition-timing-function: cubic-bezier(
		0.68,
		-0.55,
		0.265,
		1.55
	); /* custom */
}

/* Keyframe animacije */
@keyframes slideIn {
	from {
		transform: translateX(-100%);
		opacity: 0;
	}
	to {
		transform: translateX(0);
		opacity: 1;
	}
}

/* Detaljnija keyframe animacija */
@keyframes complexAnimation {
	0% {
		transform: translateX(0) scale(1);
		background-color: red;
		border-radius: 0;
	}
	25% {
		transform: translateX(100px) scale(1.2);
		background-color: yellow;
	}
	50% {
		transform: translateX(100px) translateY(50px) scale(0.8);
		background-color: green;
		border-radius: 50%;
	}
	75% {
		transform: translateX(0) translateY(50px) scale(1.1);
		background-color: blue;
	}
	100% {
		transform: translateX(0) scale(1);
		background-color: purple;
		border-radius: 0;
	}
}

.animated-element {
	animation: slideIn 0.5s ease-out;
	/* ili detaljnije: */
	animation-name: complexAnimation;
	animation-duration: 2s;
	animation-timing-function: ease-in-out;
	animation-delay: 0.5s;
	animation-iteration-count: infinite; /* ili broj */
	animation-direction: alternate; /* normal, reverse, alternate, alternate-reverse */
	animation-fill-mode: both; /* none, forwards, backwards, both */
	animation-play-state: running; /* running, paused */
}

/* Popularne animacije */
@keyframes bounce {
	0%,
	20%,
	53%,
	80%,
	100% {
		transform: translate3d(0, 0, 0);
	}
	40%,
	43% {
		transform: translate3d(0, -30px, 0);
	}
	70% {
		transform: translate3d(0, -15px, 0);
	}
	90% {
		transform: translate3d(0, -4px, 0);
	}
}

.bounce {
	animation: bounce 1s infinite;
}
```

<style>
    /* Prelazi (Transitions) */
.transition-example {
	width: 100px;
	height: 100px;
	background-color: blue;
	border-radius: 0;
	transform: scale(1) rotate(0deg);

	/* Definisanje prelaza */
	transition: all 0.3s ease-in-out;
	/* ili specifično: */
	transition-property: width, height, background-color, transform;
	transition-duration: 0.3s, 0.5s, 0.2s, 0.4s;
	transition-timing-function: ease-in-out, linear, ease, cubic-bezier(0.25, 0.1, 0.25, 1);
	transition-delay: 0s, 0.1s, 0.2s, 0.3s;
}

.transition-example:hover {
	width: 150px;
	height: 150px;
	background-color: red;
	border-radius: 50%;
	transform: scale(1.2) rotate(45deg);
}

/* Različite timing funkcije */
.timing-functions {
	transition-timing-function: linear; /* konstantna brzina */
	transition-timing-function: ease; /* sporije početak i kraj */
	transition-timing-function: ease-in; /* spori početak */
	transition-timing-function: ease-out; /* spori kraj */
	transition-timing-function: ease-in-out; /* spori početak i kraj */
	transition-timing-function: cubic-bezier(
		0.68,
		-0.55,
		0.265,
		1.55
	); /* custom */
}

/* Keyframe animacije */
@keyframes slideIn {
	from {
		transform: translateX(-100%);
		opacity: 0;
	}
	to {
		transform: translateX(0);
		opacity: 1;
	}
}

/* Detaljnija keyframe animacija */
@keyframes complexAnimation {
	0% {
		transform: translateX(0) scale(1);
		background-color: red;
		border-radius: 0;
	}
	25% {
		transform: translateX(100px) scale(1.2);
		background-color: yellow;
	}
	50% {
		transform: translateX(100px) translateY(50px) scale(0.8);
		background-color: green;
		border-radius: 50%;
	}
	75% {
		transform: translateX(0) translateY(50px) scale(1.1);
		background-color: blue;
	}
	100% {
		transform: translateX(0) scale(1);
		background-color: purple;
		border-radius: 0;
	}
}

.animated-element {
	animation: slideIn 0.5s ease-out;
	/* ili detaljnije: */
	animation-name: complexAnimation;
	animation-duration: 2s;
	animation-timing-function: ease-in-out;
	animation-delay: 0.5s;
	animation-iteration-count: infinite; /* ili broj */
	animation-direction: alternate; /* normal, reverse, alternate, alternate-reverse */
	animation-fill-mode: both; /* none, forwards, backwards, both */
	animation-play-state: running; /* running, paused */
}

/* Popularne animacije */
@keyframes bounce {
	0%,
	20%,
	53%,
	80%,
	100% {
		transform: translate3d(0, 0, 0);
	}
	40%,
	43% {
		transform: translate3d(0, -30px, 0);
	}
	70% {
		transform: translate3d(0, -15px, 0);
	}
	90% {
		transform: translate3d(0, -4px, 0);
	}
}

@keyframes fadeInUp {
	from {
		opacity: 0;
		transform: translate3d(0, 100%, 0);
	}
	to {
		opacity: 1;
		transform: translate3d(0, 0, 0);
	}
}

@keyframes pulse {
	0% {
		transform: scale3d(1, 1, 1);
	}
	50% {
		transform: scale3d(1.005, 1.5, 1.5);
	}
	100% {
		transform: scale3d(1, 1, 1);
	}
}

.bounce {
	animation: bounce 1s infinite;
}
.fade-in-up {
	animation: fadeInUp 0.6s ease-out;
}
.pulse {
	animation: pulse 2s infinite;
}

</style>
<div class="transition-example" style="margin-bottom: 20px; color: white; display: grid; place-items: center;">
  transition-example (hover mišem)
</div>

<div class="animated-element" style="margin-bottom: 40px; width:200px; height: 100px; padding: 30px">
  animated-element
</div>

<div class="bounce">bounce animacija</div>

## CSS Promenljive (CSS Variables)

CSS varijable omogućavaju definisanje vrednosti koje se mogu koristiti kroz ceo CSS kod.

```css
/* Globalne varijable u :root */
:root {
	/* Boje */
	--primary-color: #3498db;
	--secondary-color: #2ecc71;
	--accent-color: #e74c3c;
	--text-color: #2c3e50;
	--background-color: #ecf0f1;
	--border-color: #bdc3c7;

	/* Tipografija */
	--font-family-primary: 'Helvetica Neue', Arial, sans-serif;
	--font-family-heading: 'Georgia', serif;
	--font-size-small: 14px;
	--font-size-base: 16px;
	--font-size-large: 18px;
	--font-size-xl: 24px;
	--line-height-base: 1.6;

	/* Razmaci */
	--spacing-xs: 0.25rem;
	--spacing-sm: 0.5rem;
	--spacing-md: 1rem;
	--spacing-lg: 2rem;
	--spacing-xl: 3rem;

	/* Sence */
	--shadow-light: 0 2px 4px rgba(0, 0, 0, 0.1);
	--shadow-medium: 0 4px 6px rgba(0, 0, 0, 0.1);
	--shadow-heavy: 0 10px 15px rgba(0, 0, 0, 0.1);

	/* Border radius */
	--border-radius-sm: 4px;
	--border-radius-md: 8px;
	--border-radius-lg: 12px;

	/* Breakpoint-ovi */
	--breakpoint-sm: 576px;
	--breakpoint-md: 768px;
	--breakpoint-lg: 992px;
	--breakpoint-xl: 1200px;
}

/* Korišćenje varijabli */
.variable-example {
	color: var(--text-color);
	background-color: var(--background-color);
	font-family: var(--font-family-primary);
	font-size: var(--font-size-base);
	line-height: var(--line-height-base);
	padding: var(--spacing-md);
	margin: var(--spacing-lg);
	border: 1px solid var(--border-color);
	border-radius: var(--border-radius-md);
	box-shadow: var(--shadow-light);

	/* Izračunavanje sa varijablama */
	width: calc(100% - var(--spacing-lg) * 2);
	padding: calc(var(--spacing-md) * 2);
}

/* Fallback vrednosti */
.fallback-example {
	color: var(
		--undefined-color,
		#333
	); /* ako --undefined-color ne postoji, koristi #333 */
	font-size: var(
		--custom-size,
		var(--font-size-base, 16px)
	); /* ugnežđeni fallback */
}

/* Responzivne varijable */
@media (min-width: 768px) {
	:root {
		--font-size-base: 18px;
		--spacing-md: 1.5rem;
	}
}
```
