# CSS Flexbox

## Uvod

Flexbox (Flexible Box Layout) je CSS mehanizam za raspoređivanje elemenata koja značajno olakšava kreiranje layout-ova elemenata u redovima ili kolonama. Ova tehnologija je savršena za kreiranje responzivnih layout-ova i poravnavanje sadržaja na različite načine.

**Glavni koncepti:**

-   **Flex kontejner** - element koji ima `display: flex` svojstvo
-   **Flex elementi** - direktna deca flex kontejnera
-   **Glavna osa (main axis)** - osnovna osa duž koje se raspoređuju elementi
-   **Poprečna osa (cross axis)** - osa normalna (pod pravim uglom) na glavnu osu


## Display: flex

Svojstvo `display: flex` pretvara element u flex kontejner, a njegovi direktni potomci postaju flex elementi. Ovo je prvi korak za korišćenje flexbox-a.

<div class="demo-container">
  <h3>Demonstracija Display svojstva</h3>
  <p><strong>Objašnjenje:</strong> Kliknite dugme da vidite razliku između običnog blok raspoređaja i flex raspoređaja. Bez flex-a, elementi su vertikalno složeni, sa flex-om su horizontalno poređani.</p>
  <div class="controls">
    <button onclick="toggleDisplay()">Uključi/isključi display: flex</button>
  </div>
  <div id="display-demo" class="demo-box" style="display: flex; border: 2px solid #333; padding: 10px; margin: 10px 0;">
    <div class="flex-item">Element 1</div>
    <div class="flex-item">Element 2</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutno stanje:</strong> <span id="display-status">flex aktiviran</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 100px;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div class="flex-item">Element 2</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

## Flex Direction (Smer)

Svojstvo `flex-direction` definiše smer glavne ose i određuje kako se flex elementi raspoređuju u kontejneru.

**Opcije:**

-   **row** (red) - elementi se raspoređuju horizontalno, sleva nadesno (podrazumevano)
-   **row-reverse** - elementi se raspoređuju horizontalno, sdesna nalevo
-   **column** (kolona) - elementi se raspoređuju vertikalno, odozgo nadole
-   **column-reverse** - elementi se raspoređuju vertikalno, odozdo nagorе


<div class="demo-container">
  <h3>Demonstracija Flex Direction</h3>
  <p><strong>Objašnjenje:</strong> Flex direction kontroliše u kom smeru se elementi raspoređuju. </p>
  <div class="controls">
    <button onclick="setFlexDirection('row')">red (row)</button>
    <button onclick="setFlexDirection('row-reverse')">obrnut red (row-reverse)</button>
    <button onclick="setFlexDirection('column')">kolona (column)</button>
    <button onclick="setFlexDirection('column-reverse')">obrnuta kolona (column-reverse)</button>
  </div>
  <div id="flex-direction-demo" class="demo-box" style="display: flex; flex-direction: row; border: 2px solid #333; padding: 10px; margin: 10px 0; min-height: 150px;">
    <div class="flex-item">Element 1</div>
    <div class="flex-item">Element 2</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutno:</strong> <span id="flex-direction-current">row</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				flex-direction: row; /* row | row-reverse | column | column-reverse */
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
				min-height: 150px;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 100px;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div class="flex-item">Element 2</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

## Justify Content (Poravnavanje sadržaja)

Svojstvo `justify-content` poravnava flex elemente duž glavne ose i kontroliše kako se rasporedjuje slobodan prostor.

**Opcije:**

-   **flex-start** - elementi na početku kontejnera (podrazumevano)
-   **flex-end** - elementi na kraju kontejnera
-   **center** - elementi u centru kontejnera
-   **space-between** - _The items are evenly distributed within the alignment container along the main axis. The spacing between each pair of adjacent items is the same. The first item is flush with the main-start edge, and the last item is flush with the main-end edge._
-   **space-around** - _The items are evenly distributed within the alignment container along the main axis. The spacing between each pair of adjacent items is the same. The empty space before the first and after the last item equals half of the space between each pair of adjacent items. If there is only one item, it will be centered._
-   **space-evenly** - _The items are evenly distributed within the alignment container along the main axis. The spacing between each pair of adjacent items, the main-start edge and the first item, and the main-end edge and the last item, are all exactly the same._



<div class="demo-container">
  <h3>Demonstracija Justify Content</h3>
  <p><strong>Objašnjenje:</strong> Justify content kontroliše kako se elementi pozicioniraju duž glavne ose (horizontalno kad je flex-direction: row).</p>
  <div class="controls">
    <button onclick="setJustifyContent('flex-start')">početak (flex-start)</button>
    <button onclick="setJustifyContent('flex-end')">kraj (flex-end)</button>
    <button onclick="setJustifyContent('center')">centar (center)</button>
    <button onclick="setJustifyContent('space-between')">razmaci između (space-between)</button>
    <button onclick="setJustifyContent('space-around')">razmaci oko (space-around)</button>
    <button onclick="setJustifyContent('space-evenly')">jednaki razmaci (space-evenly)</button>
  </div>
  <div id="justify-content-demo" class="demo-box" style="display: flex; justify-content: flex-start; border: 2px solid #333; padding: 10px; margin: 10px 0; min-height: 100px;">
    <div class="flex-item">Element 1</div>
    <div class="flex-item">Element 2</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutno:</strong> <span id="justify-content-current">flex-start</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				justify-content: flex-start; /* flex-end | center | space-between | space-around | space-evenly */
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
				min-height: 100px;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 100px;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div class="flex-item">Element 2</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

## Align Items (Poravnavanje elemenata)

Svojstvo `align-items` poravnava flex elemente duž poprečne ose (normalno na glavnu osu).

**Opcije:**

-   **stretch** - elementi se rastežu da popune visinu kontejnera (podrazumevano)
-   **flex-start** - elementi se poravnavaju na vrh kontejnera
-   **flex-end** - elementi se poravnavaju na dno kontejnera
-   **center** - elementi se centriraju vertikalno
-   **baseline** - elementi se poravnavaju po osnovnoj liniji teksta



<div class="demo-container">
  <h3>Demonstracija Align Items</h3>
  <p><strong>Objašnjenje:</strong> Align items kontroliše vertikalno poravnavanje elemenata kada je flex-direction: row. PElement 2 ima veći font - baseline opcija će ih poravnati po liniji teksta.</p>
  <div class="controls">
    <button onclick="setAlignItems('stretch')">rastegnuto (stretch)</button>
    <button onclick="setAlignItems('flex-start')">vrh (flex-start)</button>
    <button onclick="setAlignItems('flex-end')">dno (flex-end)</button>
    <button onclick="setAlignItems('center')">centar (center)</button>
    <button onclick="setAlignItems('baseline')">osnovna linija (baseline)</button>
  </div>
  <div id="align-items-demo" class="demo-box" style="display: flex; align-items: stretch; border: 2px solid #333; padding: 10px; margin: 10px 0; height: 150px;">
    <div class="flex-item">Element 1</div>
    <div class="flex-item" style="font-size: 1.5em;">Element 2</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutno:</strong> <span id="align-items-current">stretch</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				align-items: stretch; /* flex-start | flex-end | center | baseline */
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
				height: 150px;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 100px;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div class="flex-item" style="font-size: 1.5em;">Element 2</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

## Flex Wrap (Prebacivanje u novi red)

Svojstvo `flex-wrap` kontroliše da li se flex elementi prebacuju u nove redove kada nema dovoljno mesta.

**Opcije:**

-   **nowrap** - svi elementi ostaju u istom redu (podrazumevano)
-   **wrap** - elementi se prebacuju u nove redove po potrebi
-   **wrap-reverse** - elementi se prebacuju u nove redove, ali u obrnutom redosledu

**Zašto je važno:**

-   Bez `wrap`, elementi će se sažeti (jer je po default-u flex-shrink postavljen na 1) da stanu u kontejner
-   Sa `wrap`, elementi će zadržati svoju minimalnu širinu i preći u novi red
-   Ključno za responzivni dizajn

**Napomena:** Kontejner u demonstraciji je namerno uzak (300px) da bi se video efekat.

<div class="demo-container">
  <h3>Demonstracija Flex Wrap</h3>
  <p><strong>Objašnjenje:</strong> Flex wrap određuje šta se dešava kada nema dovoljno mesta za sve elemente. Kontejner je ograničen na 300px širine da bi se video efekat.</p>
  <div class="controls">
    <button onclick="setFlexWrap('nowrap')">bez prelaska (nowrap)</button>
    <button onclick="setFlexWrap('wrap')">sa prelaskom (wrap)</button>
    <button onclick="setFlexWrap('wrap-reverse')">obrnut prelazak (wrap-reverse)</button>
  </div>
  <div id="flex-wrap-demo" class="demo-box" style="display: flex; flex-wrap: nowrap; border: 2px solid #333; padding: 10px; margin: 10px 0; width: 300px;">
    <div class="flex-item">Element 1</div>
    <div class="flex-item">Element 2</div>
    <div class="flex-item">Element 3</div>
    <div class="flex-item">Element 4</div>
    <div class="flex-item">Element 5</div>
  </div>
  <p><strong>Trenutno:</strong> <span id="flex-wrap-current">nowrap</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				flex-wrap: nowrap; /* nowrap | wrap | wrap-reverse */
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
				width: 300px;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 100px;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div class="flex-item">Element 2</div>
			<div class="flex-item">Element 3</div>
			<div class="flex-item">Element 4</div>
			<div class="flex-item">Element 5</div>
		</div>
	</body>
</html>
```

</details>

## Align Content (Poravnavanje sadržaja)

Svojstvo `align-content` poravnava redove flex elemenata duž poprečne ose kada ima više redova (kada je `flex-wrap: wrap`). Ovo svojstvo nema efekat kada postoji samo jedan red elemenata.

**Opcije:**

-   **stretch** - redovi se rastežu da popune prostor (podrazumevano)
-   **flex-start** - redovi se grupišu na vrhu
-   **flex-end** - redovi se grupišu na dnu
-   **center** - redovi se centriraju
-   **space-between** - prvi red na vrhu, poslednji na dnu, ostali jednako raspoređeni
-   **space-around** - jednaki razmaci oko svakog reda

**Razlika od align-items:**

-   `align-items` poravnava elemente unutar jednog reda
-   `align-content` poravnava cele redove jedan u odnosu na drugi

<div class="demo-container">
  <h3>Demonstracija Align Content</h3>
  <p><strong>Objašnjenje:</strong> Align content radi samo kada imate više redova elemenata (wrap je aktiviran). Kontroliše kako se ti redovi pozicioniraju u kontejneru. Kontejner je ograničen na 250px širine i 200px visine.</p>
  <div class="controls">
    <button onclick="setAlignContent('stretch')">rastegnuto (stretch)</button>
    <button onclick="setAlignContent('flex-start')">vrh (flex-start)</button>
    <button onclick="setAlignContent('flex-end')">dno (flex-end)</button>
    <button onclick="setAlignContent('center')">centar (center)</button>
    <button onclick="setAlignContent('space-between')">razmaci između (space-between)</button>
    <button onclick="setAlignContent('space-around')">razmaci oko (space-around)</button>
  </div>
  <div id="align-content-demo" class="demo-box" style="display: flex; flex-wrap: wrap; align-content: stretch; border: 2px solid #333; padding: 10px; margin: 10px 0; width: 250px; height: 250px;">
    <div class="flex-item">Element 1</div>
    <div class="flex-item">Element 2</div>
    <div class="flex-item">Element 3</div>
    <div class="flex-item">Element 4</div>
    <div class="flex-item">Element 5</div>
    <div class="flex-item">Element 6</div>
  </div>
  <p><strong>Trenutno:</strong> <span id="align-content-current">stretch</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				flex-wrap: wrap;
				align-content: stretch; /* flex-start | flex-end | center | space-between | space-around */
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
				width: 250px;
				height: 250px;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 100px;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div class="flex-item">Element 2</div>
			<div class="flex-item">Element 3</div>
			<div class="flex-item">Element 4</div>
			<div class="flex-item">Element 5</div>
			<div class="flex-item">Element 6</div>
		</div>
	</body>
</html>
```

</details>

## Gap (Razmak)

Svojstvo `gap` postavlja razmak između flex elemenata. Ovo je svojstvo koje je mnogo praktičnije od korišćenja margin-a za kreiranje razmaka.

**Prednosti gap svojstva:**

-   Automatski kreira razmake između elemenata
-   Ne dodaje razmak na spoljašnjim stranama
-   Radi sa wrap-om - razmaci se automatski kreiranje između redova
-   Možete koristiti i `row-gap` i `column-gap` zasebno

**Alternativno pisanje:**

```css
gap: 20px; /* isti razmak u oba smera */
gap: 20px 10px; /* 20px vertikalno, 10px horizontalno */
row-gap: 20px; /* samo vertikalni razmak */
column-gap: 10px; /* samo horizontalni razmak */
```

<div class="demo-container">
  <h3>Demonstracija Gap</h3>
  <p><strong>Objašnjenje:</strong> Gap svojstvo kreira razmake između elemenata bez uticaja na spoljašnje margine. Ovo je najčišći način kreiranja razmaka u flexbox rasporedu.</p>
  <div class="controls">
    <button onclick="setGap('0px')">0px</button>
    <button onclick="setGap('10px')">10px</button>
    <button onclick="setGap('20px')">20px</button>
    <button onclick="setGap('30px')">30px</button>
  </div>
  <div id="gap-demo" class="demo-box" style="display: flex; gap: 0px; border: 2px solid #333; padding: 10px; margin: 10px 0;">
    <div class="flex-item">Element 1</div>
    <div class="flex-item">Element 2</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutno:</strong> <span id="gap-current">0px</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				gap: 0px; /* 10px | 20px | 30px */
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 100px;
			}
		</style>
	</head>
	<body>
		<div id="gap-demo" class="demo-box">
			<div class="flex-item">Element 1</div>
			<div class="flex-item">Element 2</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

## Svojstva flex elemenata

Sledeća svojstva se primenjuju na individualne flex elemente (potomke flex kontejnera), a ne na sam kontejner.

### Flex Grow (Rast)

Svojstvo `flex-grow` definiše koliko flex element treba da raste u odnosu na ostale elemente kada ima dostupnog prostora.

**Kako funkcioniše:**

-   Vrednost 0 znači da element neće rasti (podrazumevano)
-   Vrednost 1 znači da će element uzeti deo dostupnog prostora
-   Veće vrednosti znače veći udeo prostora

**Intuitivno:**
Ako imate tri elementa sa flex-grow: 1, 2, 1 - srednji element će biti dvostruko veći od prva dva.



<div class="demo-container">
  <h3>Demonstracija Flex Grow</h3>
  <p><strong>Objašnjenje:</strong> Flex grow kontroliše kako element raste da popuni dostupan prostor. Element 2 (žuti) ima flex-grow svojstvo, dok ostali imaju podrazumevanu vrednost 0.</p>
  <div class="controls">
    <label>Element 2 flex-grow: </label>
    <button onclick="setFlexGrow(0)">0</button>
    <button onclick="setFlexGrow(1)">1</button>
    <button onclick="setFlexGrow(2)">2</button>
    <button onclick="setFlexGrow(3)">3</button>
  </div>
  <div class="demo-box" style="display: flex; border: 2px solid #333; padding: 10px; margin: 10px 0;">
    <div class="flex-item">Element 1</div>
    <div id="flex-grow-item" class="flex-item" style="flex-grow: 0; background-color: #ffeb3b;">Element 2 (flex-grow)</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutni flex-grow:</strong> <span id="flex-grow-current">0</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 60px;
			}

			#flex-grow-item {
				flex-grow: 0;
				background-color: #ffeb3b;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div id="flex-grow-item" class="flex-item">
				Element 2 (flex-grow)
			</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

### Flex Shrink (Skupljanje)

Svojstvo `flex-shrink` definiše koliko flex element treba da se skupi u odnosu na ostale elemente kada nema dovoljno prostora.

**Kako funkcioniše:**

-   Vrednost 1 znači normalno skupljanje (podrazumevano)
-   Vrednost 0 znači da element neće da se skupi
-   Veće vrednosti znače brže skupljanje

**Važna napomena:**
U demonstraciji svi elementi imaju minimalnu širinu od 100px, ali kontejner je samo 200px širok, što primorava elemente da se skupljaju.

**Praktični slučajevi:**

-   Sprečavanje skupljanja važnih elemenata (logo u navigaciji)
-   Kontrola kako se sadržaj prilagođava na malim ekranima

<div class="demo-container">
  <h3>Demonstracija Flex Shrink</h3>
  <p><strong>Objašnjenje:</strong> Flex shrink kontroliše kako se element skuplja kada nema dovoljno prostora. Svi elementi imaju min-width 100px, ali kontejner je 200px širok. Element 2 (žuti) ima kontrolisano flex-shrink svojstvo.</p>
  <div class="controls">
    <label>Element 2 flex-shrink: </label>
    <button onclick="setFlexShrink(0)">0 (neće da se skupi)</button>
    <button onclick="setFlexShrink(1)">1 (normalno)</button>
    <button onclick="setFlexShrink(2)">2 (brže skupljanje)</button>
    <button onclick="setFlexShrink(3)">3 (najbrže skupljanje)</button>
  </div>
  <div class="demo-box" style="display: flex; border: 2px solid #333; padding: 10px; margin: 10px 0; width: 200px;">
    <div class="flex-item" style="min-width: 100px;">Element 1 (100px min)</div>
    <div id="flex-shrink-item" class="flex-item" style="flex-shrink: 1; min-width: 100px; background-color: #ffeb3b;">Element 2 (flex-shrink)</div>
    <div class="flex-item" style="min-width: 100px;">Element 3 (100px min)</div>
  </div>
  <p><strong>Trenutni flex-shrink:</strong> <span id="flex-shrink-current">1</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
				width: 200px;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 100px;
			}

			#flex-shrink-item {
				flex-shrink: 1; /* 0 | 1 | 2 | 3 */
				min-width: 100px;
				background-color: #ffeb3b;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1 (100px min)</div>
			<div id="flex-shrink-item" class="flex-item">
				Element 2 (flex-shrink)
			</div>
			<div class="flex-item">Element 3 (100px min)</div>
		</div>
	</body>
</html>
```

</details>

### Flex Basis (Osnovna veličina)

Svojstvo `flex-basis` definiše početnu veličinu flex elementa pre nego što se distribuira slobodan prostor kroz `flex-grow` i `flex-shrink`.

**Opcije:**

-   **auto** - koristi prirodnu širinu/visinu elementa (podrazumevano)
-   **Pikesli (px)** - fiksna veličina u pikselima
-   **Procenti (%)** - procenat od kontejnera
-   **0** - ignoriše sadržaj, kreće od nule

**Redosled prioriteta:**

1. `flex-basis` (ako nije auto)
2. `width` ili `height` (zavisno od smera)
3. Prirodna veličina sadržaja

**Napomena:**
`flex-basis` je kao `width`, ali samo početna vrednost - element može da raste ili se skuplja od te tačke.

<div class="demo-container">
  <h3>Demonstracija Flex Basis</h3>
  <p><strong>Objašnjenje:</strong> Flex basis postavlja početnu veličinu elementa pre nego što flex-grow i flex-shrink počnu da rade. Element 2 (žuti) ima kontrolisano flex-basis svojstvo.</p>
  <div class="controls">
    <label>Element 2 flex-basis: </label>
    <button onclick="setFlexBasis('auto')">auto (prirodna veličina)</button>
    <button onclick="setFlexBasis('50px')">50px</button>
    <button onclick="setFlexBasis('100px')">100px</button>
    <button onclick="setFlexBasis('200px')">200px</button>
  </div>
  <div class="demo-box" style="display: flex; border: 2px solid #333; padding: 10px; margin: 10px 0;">
    <div class="flex-item">Element 1</div>
    <div id="flex-basis-item" class="flex-item" style="flex-basis: auto; background-color: #ffeb3b;">Element 2 (flex-basis)</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutni flex-basis:</strong> <span id="flex-basis-current">auto</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 60px;
			}

			#flex-basis-item {
				flex-basis: auto; /* 50px | 100px | 200px */
				background-color: #ffeb3b;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div id="flex-basis-item" class="flex-item">
				Element 2 (flex-basis)
			</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

### Align Self (Samoporavnavanje)

Svojstvo `align-self` omogućava individualnom flex elementu da poništi `align-items` vrednost postavljena na kontejneru.

**Opcije:**

-   **auto** - koristi vrednost iz kontejnera (podrazumevano)
-   **flex-start** - poravnava na početak poprečne ose
-   **flex-end** - poravnava na kraj poprečne ose
-   **center** - centrira duž poprečne ose
-   **stretch** - rastegne se duž poprečne ose
-   **baseline** - poravnava po osnovnoj liniji


<div class="demo-container">
  <h3>Demonstracija Align Self</h3>
  <p><strong>Objašnjenje:</strong> Align self omogućava pojedinačnom elementu da se poravna drugačije od ostalih. Kontejner ima align-items: flex-start, a Element 2 (žuti) može da se poravna nezavisno.</p>
  <div class="controls">
    <label>Element 2 align-self: </label>
    <button onclick="setAlignSelf('auto')">auto (kao kontejner)</button>
    <button onclick="setAlignSelf('flex-start')">vrh (flex-start)</button>
    <button onclick="setAlignSelf('flex-end')">dno (flex-end)</button>
    <button onclick="setAlignSelf('center')">centar (center)</button>
    <button onclick="setAlignSelf('stretch')">rastegnuto (stretch)</button>
  </div>
  <div class="demo-box" style="display: flex; align-items: flex-start; border: 2px solid #333; padding: 10px; margin: 10px 0; height: 120px;">
    <div class="flex-item">Element 1</div>
    <div id="align-self-item" class="flex-item" style="align-self: auto; background-color: #ffeb3b;">Element 2 (align-self)</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutni align-self:</strong> <span id="align-self-current">auto</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				align-items: flex-start;
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
				height: 120px;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 60px;
			}

			#align-self-item {
				align-self: auto; /* auto | flex-start | flex-end | center | baseline | stretch */
				background-color: #ffeb3b;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div id="align-self-item" class="flex-item">
				Element 2 (align-self)
			</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

### Order (Redosled)

Svojstvo `order` kontroliše redosled pojavljivanja flex elemenata bez menjanja HTML strukture.

**Kako funkcioniše:**

-   Podrazumevana vrednost je 0
-   Elementi sa manjim brojem se pojavljuju prvi
-   Mogu se koristiti i negativni brojevi
-   Elementi sa istom vrednošću se ređaju prema HTML redosledu

**Praktične situacije:**

-   Prebacivanje sadržaja na mobilnim uređajima
-   Kreiranje različitih raspoređaja za različite ekrane
-   Prikazivanje važnog sadržaja prvo bez menjanja HTML-a


<div class="demo-container">
  <h3>Demonstracija Order</h3>
  <p><strong>Objašnjenje:</strong> Order svojstvo menja vizuelni redosled elemenata bez menjanja HTML koda. Element 2 (žuti) može da se pozicionira na različita mesta u redosledu.</p>
  <div class="controls">
    <label>Element 2 order: </label>
    <button onclick="setOrder(-1)">-1 (prvi)</button>
    <button onclick="setOrder(0)">0 (normalno)</button>
    <button onclick="setOrder(1)">1 (treći)</button>
    <button onclick="setOrder(2)">2 (poslednji)</button>
  </div>
  <div class="demo-box" style="display: flex; border: 2px solid #333; padding: 10px; margin: 10px 0;">
    <div class="flex-item">Element 1</div>
    <div id="order-item" class="flex-item" style="order: 0; background-color: #ffeb3b;">Element 2 (order)</div>
    <div class="flex-item">Element 3</div>
  </div>
  <p><strong>Trenutni order:</strong> <span id="order-current">0</span></p>
</div>

<details>
  <summary style="cursor:pointer;">👉 Kod</summary>

```html
<html>
	<head>
		<style>
			.demo-box {
				background-color: #e0e0e0;
				border-radius: 3px;
				display: flex;
				border: 2px solid #333;
				padding: 10px;
				margin: 10px 0;
			}

			.flex-item {
				background-color: #4caf50;
				color: white;
				padding: 15px;
				margin: 2px;
				border-radius: 3px;
				text-align: center;
				min-width: 60px;
			}

			#order-item {
				order: 0; /* Vrednosti: -1, 0, 1, 2 */
				background-color: #ffeb3b;
			}
		</style>
	</head>
	<body>
		<div class="demo-box">
			<div class="flex-item">Element 1</div>
			<div id="order-item" class="flex-item">Element 2 (order)</div>
			<div class="flex-item">Element 3</div>
		</div>
	</body>
</html>
```

</details>

## Praktični saveti i najbolje prakse

### Kada koristiti Flexbox

-   Navigacione menuje
-   Card komponente
-   Forme sa labelima i input poljima
-   Centriranje sadržaja (horizontalno i vertikalno)
-   Galerije

### Česti problemi i rešenja

**Problem: Elementi se neočekivano skupljaju**

-   **Uzrok:** `flex-shrink: 1` je podrazumevano
-   **Rešenje:** Koristite `flex-shrink: 0` ili postavite `min-width`

**Problem: Flex elementi imaju različite visine**

-   **Uzrok:** `align-items: stretch` je podrazumevano, ali sadržaj može da utiče
-   **Rešenje:** Eksplicitno postavite `align-items: stretch` ili koristite `min-height`

### Flexbox skraćenice

**flex svojstvo** - kombinuje grow, shrink i basis:

-   `flex: 1;` = `flex: 1 1 0%;` (rasti, skupljaj se, kreći od 0)
-   `flex: auto;` = `flex: 1 1 auto;` (rasti, skupljaj se, kreći od prirodne veličine)
-   `flex: none;` = `flex: 0 0 auto;` (ne rasti, ne skupljaj se)

**flex-flow svojstvo** - kombinuje direction i wrap:

-   `flex-flow: column wrap;` = `flex-direction: column; flex-wrap: wrap;`

<style>
* {
  transition: all 0.3s ease;
}

.demo-container {
  margin: 10px 0;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.demo-container h3 {
  margin-top: 10px;
}

.demo-box {
  background-color: #e0e0e0;
  border-radius: 3px;
}

.flex-item {
  background-color: #4CAF50;
  color: white;
  padding: 15px;
  margin: 2px;
  border-radius: 3px;
  text-align: center;
  min-width: 60px;
}

.controls {
  margin-bottom: 10px;
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}

.controls button {
  margin: 2px;
  padding: 5px 10px;
  background-color: #2196F3;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  font-size: 12px;
}

.controls button:hover {
  background-color: #1976D2;
}

.controls label {
  font-weight: bold;
  margin-right: 10px;
  align-self: center;
}

h1, h2, h3 {
  color: #333;
}

code {
  background-color: #f0f0f0;
  padding: 2px 4px;
  border-radius: 3px;
  font-family: 'Courier New', monospace;
}

pre {
  background-color: #f0f0f0;
  padding: 10px;
  border-radius: 5px;
  overflow-x: auto;
}

strong {
  color: #333;
}

p {
  line-height: 1.6;
}

ul {
  line-height: 1.6;
}

details summary {
  font-size: 1.2em;
  padding: 6px 0;
}
</style>

<script>
// Display toggle
let isFlexDisplay = true;
function toggleDisplay() {
  const demo = document.getElementById('display-demo');
  const status = document.getElementById('display-status');
  isFlexDisplay = !isFlexDisplay;
  demo.style.display = isFlexDisplay ? 'flex' : 'block';
  status.textContent = isFlexDisplay ? 'flex aktiviran' : 'flex deaktiviran';
}

// Flex Direction
function setFlexDirection(value) {
  const demo = document.getElementById('flex-direction-demo');
  const current = document.getElementById('flex-direction-current');
  demo.style.flexDirection = value;
  current.textContent = value;
}

// Justify Content
function setJustifyContent(value) {
  const demo = document.getElementById('justify-content-demo');
  const current = document.getElementById('justify-content-current');
  demo.style.justifyContent = value;
  current.textContent = value;
}

// Align Items
function setAlignItems(value) {
  const demo = document.getElementById('align-items-demo');
  const current = document.getElementById('align-items-current');
  demo.style.alignItems = value;
  current.textContent = value;
}

// Flex Wrap
function setFlexWrap(value) {
  const demo = document.getElementById('flex-wrap-demo');
  const current = document.getElementById('flex-wrap-current');
  demo.style.flexWrap = value;
  current.textContent = value;
}

// Align Content
function setAlignContent(value) {
  const demo = document.getElementById('align-content-demo');
  const current = document.getElementById('align-content-current');
  demo.style.alignContent = value;
  current.textContent = value;
}

// Gap
function setGap(value) {
  const demo = document.getElementById('gap-demo');
  const current = document.getElementById('gap-current');
  demo.style.gap = value;
  current.textContent = value;
}

// Flex Grow
function setFlexGrow(value) {
  const item = document.getElementById('flex-grow-item');
  const current = document.getElementById('flex-grow-current');
  item.style.flexGrow = value;
  current.textContent = value;
}

// Flex Shrink
function setFlexShrink(value) {
  const item = document.getElementById('flex-shrink-item');
  const current = document.getElementById('flex-shrink-current');
  item.style.flexShrink = value;
  current.textContent = value;
}

// Flex Basis
function setFlexBasis(value) {
  const item = document.getElementById('flex-basis-item');
  const current = document.getElementById('flex-basis-current');
  item.style.flexBasis = value;
  current.textContent = value;
}

// Align Self
function setAlignSelf(value) {
  const item = document.getElementById('align-self-item');
  const current = document.getElementById('align-self-current');
  item.style.alignSelf = value;
  current.textContent = value;
}

// Order
function setOrder(value) {
  const item = document.getElementById('order-item');
  const current = document.getElementById('order-current');
  item.style.order = value;
  current.textContent = value;
}

window.setFlexDirection=setFlexDirection;
window.toggleDisplay = toggleDisplay;
window.setJustifyContent = setJustifyContent;
window.setAlignItems = setAlignItems;
window.setFlexWrap = setFlexWrap;
window.setAlignContent = setAlignContent;
window.setGap = setGap;
window.setFlexGrow = setFlexGrow;
window.setFlexShrink = setFlexShrink;
window.setFlexBasis = setFlexBasis;
window.setAlignSelf = setAlignSelf;
window.setOrder = setOrder;

</script>
