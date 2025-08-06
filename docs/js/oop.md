# Objektno-Orijentisano Programiranje u JavaScript-u

## Uvod u OOP u JavaScript-u

Objektno-orijentisano programiranje (OOP) u JavaScript-u se značajno razlikuje od klasičnih OOP jezika poput C++. JavaScript OOP je baziran na **prototipovima** umesto na **klasama**, iako je ES6 uveo sintaksu klasa kao sintaksni šećer.

### Ključne razlike od C++:

-   **Dinamičko tipiziranje**: Nema potrebe da se deklarišu tipovi promenljivih
-   **Nasleđivanje bazirano na prototipovima**: Objekti mogu da nasleđuju direktno od drugih objekata
-   **Funkcije su objekti**: Mogu se dodeliti promenljivim, proslediti kao argumenti
-   **Nema višestrukog nasleđivanja**: (ali se može simulirati korišćenjem mixina)

## Objekti i svojstva

### Kreiranje objekata

U JavaScript-u, objekti su kolekcije parova ključ-vrednost. Za razliku od C++ gde se prvo mora definisati klasa, u JS se objekat može kreirati direktno.

```javascript
// Literalni objekat (najčešći način)
const person = {
	name: 'John',
	age: 30,
	city: 'New York',
};

console.log(person.name); // Izlaz: John
console.log(person['age']); // Izlaz: 30
```

### Dinamičko dodavanje/uklanjanje svojstava

Za razliku od C++ gde je struktura klase fiksirana u vreme kompajliranja, JavaScript objekti su dinamički:

```javascript
const car = {
	brand: 'Toyota',
	model: 'Camry',
};

// Dodaj novo svojstvo
car.year = 2020;
car['color'] = 'blue';

console.log(car);
// Izlaz: { brand: "Toyota", model: "Camry", year: 2020, color: "blue" }

// Ukloni svojstvo
delete car.color;
console.log(car);
// Izlaz: { brand: "Toyota", model: "Camry", year: 2020 }
```

## Constructor funkcije (ES5 stil)

> Pre ES6, JavaScript nije imao ključnu reč class, pa su se objekti kreirali pomoću konstruktorskih funkcija. Danas se preporučuje korišćenje ES6 klasa.

Pre ES6 klasa, constructor funkcije su bile osnovni način kreiranja šablona objekata:

```javascript
// Constructor funkcija (primeti konvenciju velikog slova)
function Person(name, age) {
	this.name = name;
	this.age = age;

	// Metoda definisana unutar konstruktora (nije preporučeno za performanse)
	this.greet = function () {
		return `Hello, I'm ${this.name}`;
	};
}

// Dodavanje metoda u prototip (preporučeno)
Person.prototype.introduce = function () {
	return `I'm ${this.name} and I'm ${this.age} years old`;
};

// Kreiranje instanci
const person1 = new Person('Alice', 25);
const person2 = new Person('Bob', 30);

console.log(person1.greet()); // Izlaz: Hello, I'm Alice
console.log(person2.introduce()); // Izlaz: I'm Bob and I'm 30 years old
```


## Klase (ES6+ stil)

ES6 je uveo sintaksu klasa koja je poznatija C++ programerima:

```javascript
class Animal {
	// Constructor metoda
	constructor(name, species) {
		this.name = name;
		this.species = species;
	}

	// Instance metoda
	makeSound() {
		return `${this.name} makes a sound`;
	}

	// Još jedna metoda
	getInfo() {
		return `${this.name} is a ${this.species}`;
	}
}

// Kreiranje instanci
const dog = new Animal('Buddy', 'Dog');
const cat = new Animal('Whiskers', 'Cat');

console.log(dog.makeSound()); // Izlaz: Buddy makes a sound
console.log(cat.getInfo()); // Izlaz: Whiskers is a Cat
```


## Nasleđivanje

### Korišćenje ES6 klasa

```javascript
class Animal {
	constructor(name) {
		this.name = name;
	}

	speak() {
		return `${this.name} makes a sound`;
	}

	move() {
		return `${this.name} moves`;
	}
}

class Dog extends Animal {
	constructor(name, breed) {
		super(name); // Pozovi roditeljski konstruktor (obavezno!)
		this.breed = breed;
	}

	// Override-ovanje roditeljske metode
	speak() {
		return `${this.name} barks`;
	}

	// Nova metoda specifična za Dog
	wagTail() {
		return `${this.name} wags tail`;
	}
}

const myDog = new Dog('Rex', 'German Shepherd');

console.log(myDog.speak()); // Izlaz: Rex barks
console.log(myDog.move()); // Izlaz: Rex moves (nasleđeno)
console.log(myDog.wagTail()); // Izlaz: Rex wags tail
console.log(myDog.breed); // Izlaz: German Shepherd
```

### Razlike od C++ nasleđivanja:

-   **Nema virtual ključnu reč**: Sve metode su "virtual" po default-u
-   **Samo jednostruko nasleđivanje**

## Enkapsulacija

JavaScript nema prave privatne članove kao C++, ali postoji nekoliko pristupa:

### Privatnost bazirana na konvenciji (underscore prefiks)

```javascript
class BankAccount {
	constructor(initialBalance) {
		this.accountNumber = Math.random().toString(36).substr(2, 9);
		this._balance = initialBalance; // Konvencija: _ znači privatno
	}

	deposit(amount) {
		if (amount > 0) {
			this._balance += amount;
			return this._balance;
		}
		throw new Error('Amount must be positive');
	}

	withdraw(amount) {
		if (amount > 0 && amount <= this._balance) {
			this._balance -= amount;
			return this._balance;
		}
		throw new Error('Invalid withdrawal amount');
	}

	getBalance() {
		return this._balance;
	}
}

const account = new BankAccount(1000);
console.log(account.getBalance()); // Izlaz: 1000
console.log(account.deposit(500)); // Izlaz: 1500
// account._balance je dostupan, ali po konvenciji ne bi trebao da se koristi direktno
```

### Privatna polja (nove verzije JavaScript-a)

```javascript
class SecureBankAccount {
	#balance; // Privatno polje
	#accountNumber;

	constructor(initialBalance) {
		this.#balance = initialBalance;
		this.#accountNumber = Math.random().toString(36).substr(2, 9);
	}

	deposit(amount) {
		if (amount > 0) {
			this.#balance += amount;
			return this.#balance;
		}
		throw new Error('Amount must be positive');
	}

	getBalance() {
		return this.#balance;
	}

	#validateAmount(amount) {
		// Privatna metoda
		return amount > 0 && amount <= this.#balance;
	}

	withdraw(amount) {
		if (this.#validateAmount(amount)) {
			this.#balance -= amount;
			return this.#balance;
		}
		throw new Error('Invalid withdrawal amount');
	}
}

const secureAccount = new SecureBankAccount(1000);
console.log(secureAccount.getBalance()); // Izlaz: 1000
// console.log(secureAccount.#balance); // SyntaxError: Private field
```

## Polimorfizam

JavaScript podržava polimorfizam kroz preklapanje metoda i _duck_ typing:

```javascript
class Shape {
	constructor(name) {
		this.name = name;
	}

	area() {
		throw new Error('Area method must be implemented');
	}

	describe() {
		return `This is a ${this.name} with area ${this.area()}`;
	}
}

class Rectangle extends Shape {
	constructor(width, height) {
		super('rectangle');
		this.width = width;
		this.height = height;
	}

	area() {
		return this.width * this.height;
	}
}

class Circle extends Shape {
	constructor(radius) {
		super('circle');
		this.radius = radius;
	}

	area() {
		return Math.PI * this.radius * this.radius;
	}
}

// Polimorfno ponašanje
const shapes = [new Rectangle(5, 3), new Circle(2), new Rectangle(4, 4)];

shapes.forEach((shape) => {
	console.log(shape.describe());
});
```

**Izlaz:**

```
This is a rectangle with area 15
This is a circle with area 12.566370614359172
This is a rectangle with area 16
```

## Statičke metode i svojstva

Statički članovi pripadaju klasi a ne instancema:

```javascript
class MathUtils {
	static PI = 3.14159; // Statičko svojstvo

	static add(a, b) {
		return a + b;
	}

	static multiply(a, b) {
		return a * b;
	}

	static circleArea(radius) {
		return this.PI * radius * radius; // Korišćenje statičkog svojstva
	}
}

// Pozovi statičke metode na klasi, ne na instancama
console.log(MathUtils.add(5, 3)); // Izlaz: 8
console.log(MathUtils.circleArea(5)); // Izlaz: 78.53975
console.log(MathUtils.PI); // Izlaz: 3.14159

// const math = new MathUtils();
// math.add(1, 2); // TypeError: math.add is not a function
```

## Getter-i i Setter-i

Getter-i i setter-i vam omogućavaju da definišete metode kojima se pristupa kao svojstvima:

```javascript
class Osoba {
  constructor(ime) {
    this._ime = ime; // koristimo _ime kao privatnu promenljivu
  }

  // Getter
  get ime() {
    return this._ime;
  }

  // Setter
  set ime(novoIme) {
    if (novoIme.length > 0) {
      this._ime = novoIme;
    } else {
      console.log("Ime ne može biti prazno!");
    }
  }
}

// Primer korišćenja
let osoba = new Osoba("Marko");

console.log(osoba.ime); // koristi getter -> "Marko"

osoba.ime = "Petar"; // koristi setter
console.log(osoba.ime); // "Petar"

osoba.ime = ""; // koristi setter -> ispisuje "Ime ne može biti prazno!"
console.log(osoba.ime); // i dalje "Petar"
```

### Napredniji primer: Konverzija temperature

```javascript
class Temperature {
	constructor(celsius = 0) {
		this._celsius = celsius;
	}

	get celsius() {
		return this._celsius;
	}

	set celsius(value) {
		if (typeof value !== 'number') {
			throw new Error('Temperature must be a number');
		}
		this._celsius = value;
	}

	get fahrenheit() {
		return (this._celsius * 9) / 5 + 32;
	}

	set fahrenheit(value) {
		if (typeof value !== 'number') {
			throw new Error('Temperature must be a number');
		}
		this._celsius = ((value - 32) * 5) / 9;
	}

	get kelvin() {
		return this._celsius + 273.15;
	}
}

const temp = new Temperature(25);
console.log(temp.celsius); // Izlaz: 25
console.log(temp.fahrenheit); // Izlaz: 77
console.log(temp.kelvin); // Izlaz: 298.15

temp.fahrenheit = 100;
console.log(temp.celsius); // Izlaz: 37.77777777777778
```

## Napredni koncepti (opcionalno)

### Mixini

Pošto JavaScript ne podržava višestruko nasleđivanje, mixini pružaju način deljenja funkcionalnosti:

```javascript
// Mixin objekti
const CanFly = {
	fly() {
		return `${this.name} is flying`;
	},
};

const CanSwim = {
	swim() {
		return `${this.name} is swimming`;
	},
};

// Bazna klasa
class Animal {
	constructor(name) {
		this.name = name;
	}
}

// Primeni mixine
Object.assign(Animal.prototype, CanFly, CanSwim);

class Duck extends Animal {
	constructor(name) {
		super(name);
	}
}

const duck = new Duck('Donald');
console.log(duck.fly()); // Izlaz: Donald is flying
console.log(duck.swim()); // Izlaz: Donald is swimming
```

### Ulančavanje metoda

```javascript
class Calculator {
	constructor() {
		this.value = 0;
	}

	add(num) {
		this.value += num;
		return this; // Vrati this za ulančavanje
	}

	subtract(num) {
		this.value -= num;
		return this;
	}

	multiply(num) {
		this.value *= num;
		return this;
	}

	divide(num) {
		if (num !== 0) {
			this.value /= num;
		}
		return this;
	}

	result() {
		return this.value;
	}

	reset() {
		this.value = 0;
		return this;
	}
}

// Ulančavanje metoda
const calc = new Calculator();
const result = calc.add(10).multiply(2).subtract(5).divide(3).result();

console.log(result); // Izlaz: 5
```

### Simulacija apstraktnih klasa

```javascript
class AbstractShape {
	constructor() {
		// this.constructor će biti AbstractShape samo ukoliko pokušamo da instanciramo abstraktnu klasu
		// u suprotnom, biće to konkretna klasa koja je nasleđuje
		if (this.constructor === AbstractShape) {
			throw new Error("Abstract classes can't be instantiated.");
		}
	}

	// Apstraktna metoda
	area() {
		throw new Error("Method 'area()' must be implemented.");
	}

	// Konkretna metoda
	describe() {
		return `This shape has an area of ${this.area()}`;
	}
}

class Rectangle extends AbstractShape {
	constructor(width, height) {
		super();
		this.width = width;
		this.height = height;
	}

	area() {
		return this.width * this.height;
	}
}

// const shape = new AbstractShape(); // Greška: Abstract classes can't be instantiated
const rect = new Rectangle(5, 3);
console.log(rect.describe()); // Izlaz: This shape has an area of 15
```
