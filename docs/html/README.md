# HTML

## Šta je HTML?

HTML (HyperText Markup Language) je standardni markup jezik koji se koristi za kreiranje veb stranica. On opisuje strukturu i sadržaj veb stranice koristeći elemente i tagove. HTML se može zamisliti kao kostur veb stranice - on definiše koji sadržaj ide gde i kako je organizovan.

HTML nije programski jezik; to je markup jezik koji koristi tagove da označi tekst i definiše kako sadržaj treba da bude prikazan u veb pregledaču.

## Osnovna HTML struktura

Svaki HTML dokument prati sledeću osnovnu strukturu:

```html
<!DOCTYPE html>
<html lang="sr">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Naslov Stranice</title>
	</head>
	<body>
		<!-- Sadržaj stranice ide ovde -->
	</body>
</html>
```

### Objašnjenje strukture

-   **`<!DOCTYPE html>`**: Deklariše tip dokumenta
-   **`<html>`**: Glavni element koji sadrži sve ostale elemente
-   **`<head>`**: Sadrži meta podatke o dokumentu (ne prikazuje se na stranici)
-   **`<body>`**: Sadrži vidljivi sadržaj veb stranice

## Razumevanje HTML elemenata i tagova

HTML elementi su osnovni gradivni blokovi HTML stranica. Element se sastoji od:

1. **Otvarajući tag**: `<tagname>`
2. **Sadržaj**: Tekst ili drugi elementi unutar
3. **Zatvarajući tag**: `</tagname>`

```html
<h1>Ovo je naslov</h1>
<p>Ovo je paragraf sa <strong>podebljantim tekstom</strong> unutar.</p>
```

### Samo-zatvarajući tagovi

Neki elementi nemaju sadržaj (img, input, br, ...):

```html
<img src="slika.jpg" alt="Opis" />
<br />
<hr />
<input type="text" />
```

### Atributi

Atributi pružaju dodatne informacije o elementima:

```html
<a href="https://primer.com" target="_blank">Kliknite ovde</a>
<img src="fotografija.jpg" alt="Zalazak sunca" width="300" />
<div class="kontejner" id="glavni-sadrzaj">Sadržaj ovde</div>
```

- `href` - lokacija do koje a element vodi
- `target` - određuje gde će se otvoriti link (npr. `_blank` za novi tab, `_self` za isti prozor)
- `src` - putanja do slike koja se prikazuje
- `alt` - opis slike; prikazuje se ako učitavanje slike ne uspe
- `width` - širina slike
- `class` - CSS klasa kojoj div element pripada
- `id` - jedinstveni identifikator 
- ...

## Osnovni HTML elementi

### Tekstualni elementi

#### Naslovi

HTML pruža šest nivoa naslova, od najvažnijeg (h1) do najmanje važnog (h6):

```html
<h1>Glavni Naslov</h1>
<h2>Naslov Sekcije</h2>
<h3>Naslov Podsekcije</h3>
<h4>Naslov Pod-podsekcije</h4>
<h5>Manji Naslov</h5>
<h6>Najmanji Naslov</h6>
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#EEEEEE;padding:15px">
        <h1>Glavni Naslov</h1>
        <h2>Naslov Sekcije</h2>
        <h3>Naslov Podsekcije</h3>
        <h4>Naslov Pod-podsekcije</h4>
        <h5>Manji Naslov</h5>
        <h6>Najmanji Naslov</h6>
    </div>
</details>

#### Paragrafi i formatiranje teksta

```html
<p>Ovo je običan paragraf teksta.</p>
<p>
	Ovaj paragraf sadrži <strong>podebljan tekst</strong> i
	<em>cursive tekst</em>.
</p>
<p>
	Možete takođe koristiti <b>bold</b> i <i>italic</i>, ali se preporučuje korišćenje strong i em.
</p>
<p>Za kod, koristite <code>console.log('Zdravo')</code> u liniji.</p>
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#EEEEEE;padding:15px">
        <p>Ovo je običan paragraf teksta.</p>
        <p>
            Ovaj paragraf sadrži <strong>podebljan tekst</strong> i
            <em>kurziv tekst</em>.
        </p>
        <p>
            Možete takođe koristiti <b>bold</b> i <i>italic</i>, ali preporučuje korišćenje strong i em.
        </p>
        <p>Za kod, koristite <code>console.log('Zdravo')</code> u liniji.</p>
    </div>
</details>

#### Prelomi redova i horizontalne linije

```html
<p>Prvi red<br />Drugi red nakon preloma</p>
<hr />
<!-- Kreira horizontalnu liniju -->
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#EEEEEE;padding:15px">
        <p>Prvi red<br />Drugi red nakon preloma</p>
<hr style="background-color:black;height:2px" color="black"/>
    </div>
</details>

### Liste

#### Neuređene (unordered) liste 

```html
<ul>
	<li>Prva stavka</li>
	<li>Druga stavka</li>
	<li>Treća stavka</li>
</ul>
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#EEEEEE;padding:15px">
        <ul>
            <li>Prva stavka</li>
            <li>Druga stavka</li>
            <li>Treća stavka</li>
        </ul>
    </div>
</details>

#### Uređene (ordered) liste

```html
<ol>
	<li>Prvi korak</li>
	<li>Drugi korak</li>
	<li>Treći korak</li>
</ol>
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#EEEEEE;padding:15px">
<ol>
	<li>Prvi korak</li>
	<li>Drugi korak</li>
	<li>Treći korak</li>
</ol>
    </div>
</details>


### Linkovi

```html
<!-- Spoljašnji link -->
<a href="https://www.primer.com">Posetite Primer.com</a><br/>

<!-- Unutrašnji link -->
<a href="o-nama.html">O Nama</a><br/>

<!-- Email link -->
<a href="mailto:kontakt@primer.com">Pošaljite Email</a><br/>

<!-- Link ka sekciji na istoj stranici -->
<a href="#sekcija1">Idite na Sekciju 1</a><br/>
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#EEEEEE;padding:15px">
        <a href="https://www.primer.com">Posetite Primer.com</a><br/>        
        <!-- Unutrašnji link -->
        <a href="o-nama.html">O Nama</a><br/>
        <!-- Email link -->
        <a href="mailto:kontakt@primer.com">Pošaljite Email</a><br/>
        <!-- Link ka sekciji na istoj stranici -->
        <a href="#sekcija1">Idite na Sekciju 1</a><br/>
    </div>
</details>

### Slike

```html
<img src="slika.jpg" alt="Opis slike" width="300" height="200" />
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#EEEEEE;padding:15px">
        <img src="/html/slika.jfif" alt="Opis slike" width="200" height="200" />
    </div>
</details>

`alt` atribut je ključan za _accessibility_ i _SEO_.

### Tabele

```html
<table>
	<thead>
		<tr>
			<th>Ime</th>
			<th>Godine</th>
			<th>Grad</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Marko</td>
			<td>25</td>
			<td>Beograd</td>
		</tr>
		<tr>
			<td>Ana</td>
			<td>30</td>
			<td>Novi Sad</td>
		</tr>
	</tbody>
</table>
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#FAFAFA;padding:15px">
<table>
	<thead>
		<tr>
			<th>Ime</th>
			<th>Godine</th>
			<th>Grad</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Marko</td>
			<td>25</td>
			<td>Beograd</td>
		</tr>
		<tr>
			<td>Ana</td>
			<td>30</td>
			<td>Novi Sad</td>
		</tr>
	</tbody>
</table>
    </div>
</details>

### Forme

```html
<form action="/posalji" method="post">
	<label for="ime">Ime:</label><br/>
	<input type="text" id="ime" name="ime" required /><br/>

	<label for="email">Email:</label><br/>
	<input type="email" id="email" name="email" required /><br/>

	<label for="poruka">Poruka:</label><br/>
	<textarea id="poruka" name="poruka" rows="4"></textarea><br/>

	<label for="zemlja">Zemlja:</label><br/>
	<select id="zemlja" name="zemlja">
		<option value="rs">Srbija</option>
		<option value="hr">Hrvatska</option>
		<option value="ba">Bosna i Hercegovina</option>
	</select><br/>

	<input type="checkbox" id="newsletter" name="newsletter" />
	<label for="newsletter">Pretplatite se na newsletter</label><br/>

	<input type="submit" value="Pošaljite" />
</form>
```

<details>
<summary style="cursor:pointer;">👆 Rezultat</summary>
    <div style="background-color:#EEEEEE;padding:15px">
    <form action="/posalji" method="post">
	<label for="ime">Ime:</label>
    <br/>
	<input type="text" id="ime" name="ime" required />
    <br/>
	<label for="email">Email:</label>
    <br/>
	<input type="email" id="email" name="email" required />
    <br/>
	<label for="poruka">Poruka:</label>
    <br/>
	<textarea id="poruka" name="poruka" rows="4"></textarea>
    <br/>
	<label for="zemlja">Zemlja:</label>
    <br/>
	<select id="zemlja" name="zemlja">
		<option value="rs">Srbija</option>
		<option value="hr">Hrvatska</option>
		<option value="ba">Bosna i Hercegovina</option>
	</select>
    <br/>
	<input type="checkbox" id="newsletter" name="newsletter" />
	<label for="newsletter">Pretplatite se na newsletter</label>
    <br/>
	<input type="submit" value="Pošaljite" />
</form> 
    </div>
</details>

## Semantički HTML elementi

Semantički HTML koristi elemente koji jasno opisuju svoje značenje i svrhu. Ovo poboljšava _accessibility_, SEO i održivost koda.

<p style="align:center;">
    <img src="/html/semantic.jpg" height="300" style="display:block; margin-left:auto; margin-right:auto;" />
</p>


### Header (zaglavlje)

Header element označava zaglavlje stranice ili sekcije i obično sadrži navigaciju, logo ili naslov sajta.

```html
<header>
	<h1>Naslov Veb Sajta</h1>
	<nav>
		<ul>
			<li><a href="#pocetna">Početna</a></li>
			<li><a href="#o-nama">O nama</a></li>
			<li><a href="#kontakt">Kontakt</a></li>
		</ul>
	</nav>
</header>
```


### Navigation (navigacija)

Nav element označava navigacioni meni koji omogućava korisnicima da se kreću kroz sajt.

```html
<nav>
	<ul>
		<li><a href="/">Početna</a></li>
		<li><a href="/proizvodi">Proizvodi</a></li>
		<li><a href="/kontakt">Kontakt</a></li>
	</ul>
</nav>
```


### Main (glavni sadržaj)
    
Main element označava glavni sadržaj stranice koji je jedinstven i centralni za tu specifičnu stranicu.

```html
<main>
	<h1>Dobrodošli na naš veb sajt</h1>
	<p>Ovo je glavna oblast sadržaja.</p>
</main>
```


### Section (sekcija) i article (članak)

Section element grupiše semantički povezan sadržaj i obično ima svoj naslov.

Article element predstavlja nezavisan sadržaj poput članka ili blog posta.

```html
<section>
	<h2>Najnovije Vesti</h2>
	<article>
		<h3>Važna Vest</h3>
		<p>Sadržaj vesti...</p>
		<footer>
			<p>Objavljeno <time datetime="2024-03-15">15. marta 2024.</time></p>
		</footer>
	</article>
</section>
```

### Aside (bočni sadržaj)

Aside element označava sadržaj koji je povezan sa glavnim sadržajem ali može postojati nezavisno, poput bočne trake.

```html
<aside>
	<h3>Povezani Linkovi</h3>
	<ul>
		<li><a href="#">Link 1</a></li>
		<li><a href="#">Link 2</a></li>
	</ul>
</aside>
```


### Footer

Footer element označava podnožje stranice ili sekcije i obično sadrži autorske informacije, linkove ili kontakt podatke.

```html
<footer>
	<p>&copy; 2024 Naziv Kompanije. Sva prava zadržana.</p>
	<address>
		Kontaktirajte nas na
		<a href="mailto:info@kompanija.com">info@kompanija.com</a>
	</address>
</footer>
```


### Figure i figcaption

Figure element označava samostalan sadržaj poput slike, dijagrama ili koda koji se može pomeriti bez uticaja na tok dokumenta.

Figcaption pruža opis ili naslov za figure element.

```html
<figure>
	<img src="grafikon.png" alt="Grafikon prodajnih podataka" />
	<figcaption>Performanse prodaje za Q1 2024</figcaption>
</figure>
```


### Details i summary 

Details element kreira interaktivni widget koji korisnik može otvoriti i zatvoriti.

Summary pruža vidljivi naslov ili rezime za details element.


```html
<details>
	<summary>Kliknite da proširite</summary>
	<p>Ovaj sadržaj je po default-u sakriven i prikazuje se kada se klikne.</p>
</details>
```


## Generički kontejnerski elementi

### Div i span

#### Div (blok kontejner)

```html
<div class="kontejner">
	<div class="kartica">
		<h3>Naslov Kartice</h3>
		<p>Sadržaj kartice ide ovde.</p>
	</div>
</div>
```

#### Span (Inline Kontejner)

```html
<p>
	Ovo je normalan tekst sa
	<span class="istaknut">istaknutim delom</span> unutar.
</p>
```

## Kako HTML Funkcioniše u Pregledaču

### Model Objekta Dokumenta (DOM)

Kada pregledač učita HTML dokument, kreira Model Objekta Dokumenta (DOM) - struktura nalik na stablo koja predstavlja sve elemente na stranici. Svaki HTML element postaje čvor u ovom stablu.

### Proces Renderovanja

1. **Parsiranje**: Pregledač čita HTML i kreira DOM
2. **Stilizovanje**: CSS se primenjuje na DOM elemente
3. **Layout**: Pregledač izračunava pozicije i veličine elemenata
4. **Crtanje**: Elementi se crtaju na ekranu

### Developer Tools Pregledača

Svi moderni pregledači uključuju developer alate koji vam omogućavaju da:

-   Inspekctirate HTML elemente
-   Menjate sadržaj u realnom vremenu
-   Debug-ujete CSS i JavaScript
-   Pratite mrežne zahteve

Pristupite im pritiskom na F12 ili desni klik i izbor "Inspect Element."

## Najbolje Prakse

### Pristupačnost

1. **Koristite semantičke elemente** na odgovarajući način
2. **Obezbedite alt tekst** za slike
3. **Koristite pravilnu hijerarhiju naslova** (ne preskačite nivoe)
4. **Jasno označite form polja**
5. **Osigurajte dobar kontrast boja**

### SEO (Optimizacija za Pretražnice)

1. **Koristite opisne naslove** i meta opise
2. **Strukturirajte sadržaj** sa pravilnim naslovima
3. **Koristite semantički HTML** za bolje razumevanje sadržaja
4. **Optimizujte slike** sa opisnim alt tekstom
5. **Kreirajte čist, valjan HTML**

### Organizacija Koda

1. **Uvlačite kod** konzistentno
2. **Koristite komentare** da objasnite složene sekcije
3. **Držite linije razumno kratke**
4. **Zatvorite sve tagove** pravilno
5. **Koristite mala slova** za sve HTML elemente i atribute

### Performanse

1. **Optimizujte slike** (kompresujte i koristite odgovarajuće formate)
2. **Minimizujte HTTP zahteve**
3. **Koristite semantičke elemente** umesto prekomernih div-ova
4. **Validirajte vaš HTML** da uhvatite greške

## Česti HTML Atributi

### Globalni Atributi (Dostupni na Svim Elementima)

-   **`id`**: Jedinstveni identifikator za element
-   **`class`**: CSS imena klasa za stilizovanje
-   **`style`**: Inline CSS stilovi
-   **`title`**: Tekst tooltip-a
-   **`lang`**: Jezik sadržaja elementa
-   **`data-*`**: Prilagođeni data atributi

### Primeri Specifičnih Atributa

```html
<!-- Linkovi -->
<a href="url" target="_blank" rel="noopener">Link</a>

<!-- Slike -->
<img src="slika.jpg" alt="Opis" loading="lazy" />

<!-- Forme -->
<input
	type="text"
	name="korisnicko_ime"
	placeholder="Unesite korisničko ime"
	required
/>

<!-- Tabele -->
<td colspan="2" rowspan="3">Sadržaj ćelije</td>
```

## Kompletan Primer: Semantička HTML Stranica

```html
<!DOCTYPE html>
<html lang="sr">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta
			name="description"
			content="Kompletan primer semantičkog HTML-a"
		/>
		<title>Primer Semantičkog HTML-a</title>
	</head>
	<body>
		<header>
			<h1>Moj Blog</h1>
			<nav>
				<ul>
					<li><a href="#pocetna">Početna</a></li>
					<li><a href="#o-meni">O meni</a></li>
					<li><a href="#kontakt">Kontakt</a></li>
				</ul>
			</nav>
		</header>

		<main>
			<section>
				<h2>Najnoviji Članci</h2>

				<article>
					<header>
						<h3>Razumevanje HTML Semantike</h3>
						<p>
							Objavljeno
							<time datetime="2024-03-15">15. marta 2024.</time>
						</p>
					</header>

					<p>
						Semantički HTML je ključan za kreiranje pristupačnih i
						SEO-friendly veb sajtova...
					</p>

					<figure>
						<img
							src="semanticki-html.png"
							alt="Dijagram koji prikazuje semantičku HTML strukturu"
						/>
						<figcaption>
							Primer semantičke HTML strukture
						</figcaption>
					</figure>

					<blockquote>
						<p>
							"Semantički HTML čini web više pristupačnim za sve
							korisnike."
						</p>
						<footer>
							— <cite>Web Accessibility Initiative</cite>
						</footer>
					</blockquote>

					<footer>
						<p>
							Tagovi: <span class="tag">HTML</span>,
							<span class="tag">Web Development</span>
						</p>
					</footer>
				</article>
			</section>

			<aside>
				<h3>O Autoru</h3>
				<p>
					Web developer sa 5 godina iskustva u kreiranju modernih,
					pristupačnih veb sajtova.
				</p>

				<address>
					<p>
						Kontakt:
						<a href="mailto:autor@blog.com">autor@blog.com</a>
					</p>
				</address>
			</aside>
		</main>

		<footer>
			<p>&copy; 2024 Moj Blog. Sva prava zadržana.</p>
			<details>
				<summary>Više informacija</summary>
				<p>
					Ovaj sajt je kreiran koristeći semantički HTML i moderne web
					standarde.
				</p>
			</details>
		</footer>
	</body>
</html>
```

## Sledeći Koraci

Nakon što savladate HTML, razmislite o učenju:

1. **CSS** - Za stilizovanje i layout
2. **JavaScript** - Za interaktivnost i dinamično ponašanje
3. **Responsive Design** - Za mobile-friendly veb sajtove
4. **Web Accessibility** - Za inkluzivni dizajn
5. **Moderni Framework-ovi** - Poput React, Vue ili Angular

Zapamtite, HTML je osnova web developmenta. Solidno razumevanje semantičkog HTML-a će vas učiniti boljim web developerom i pomoći vam da kreirate pristupačnije, održivije veb sajtove.
