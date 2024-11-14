# Lektion-11-14

### Manipulation
 Fortsättning...

#### classList

classList är en attribute som har ett array-liknande value. Det innehåller alla klasser som är tilldelat till elemenetet. Men det kallas `DOMTokenList`. En speciell typ av object i JS. Visar alla klasser när man console.log

```js
const header = document.querySelector("header");
console.log(header.classList);
// => ['header', 'brown', 'container', value: header brown container]
```

Många metoder till classList men 3 viktiga:

- `add()`: lägger till en token i classList.
- `remove()`: tar bort en token från classList.
- `contains()`: kollar om det finns en token i classList. Skickar tillbaka en boolen för en if-check exempelvis.

```js
header.classList.add("brown", "container");
```

Koden lägger till två klasser till elementet. Med andra ord, två tokens till DOMTokenList.

#### getAttribute( attribute )

Denna metod används för att returna en specifik attribute på ett element.

```html
<img class ="santa" src="some-image" alt="rödtomte" />
```

Vi tar denna image tag och får värdet av alt attributen.

```js
const image = document.querySelector(".santa")
const altText = image.getAttribute("alt");
```

#### setAttribute( attribute, newValue ) => void / ingetting

Vi ska uppdatera `alt`- värdet på santa img till annan text.

```js
image.setAttribute("alt", "bara en vanlig tomte");
const altText = image.getAttribute("alt");
console.log(altText);
```
removeAttribute( attribute ) => void

Tar bort en attribute på ett element. Tar en parameter som är attributen som ska tas bort.

Tar bort `alt` från ovan

```js
image.removeAttribute("alt");
```

#### insertAdjacentElement( position, element ) => void

Fungerar som `appendChild` men tillåter oss att välja position vart vi vill lägga elementet i deras parent.

Två parametrar, en för positionen, och en för elementet som ska in.

Positionerna kan ha 4 värden:

- `beforebegin`: detta kommer lägga elementet innan parent elementet. Med andra ord ett syskon element till elementet metoden tillades på.

- `afterend`: detta kommer lägga elementet efter parent elementet. Blir också syskon element till elementet metoden tillades på.

- `afterbegin`: detta kommer lägga elementet som första child element på parent elementet.

- `beforeend`: detta kommer lägga elementet som sista child element på parent elementet. Samma som `appendChild()` metoden gör.


```js
const section = document.createElement("section");
section.innerText = "This is a section";

// Vi vill lägga section i en main tag som redan finns i HTML dokumentet.

const main = document.querySelector("main");
main.insertAdjacentElement("beforebegin", section);

// Blir ett syskon element med main. Alltså innan <main>
```

```js
main.insertAdjacentElement("afterend", section);

// Blir nu istället också syskon element. Fast positionen efter <main>.
```

Kommer flytta variablen två gånger om man lägger dessa metoder efter varandra. Det är `reference data type`. Det blir alltså inte duplicerat.

#### innerHTML

Att skapa html element från grunden kan vara drygt. Först måste vi skapa elementet, byta innerText, sen lägga till kanske classes, ID och andra attributer. Många metoder att kalla och lång kod.

Denna metod ger oss möjligheten att skapa HTML som en string, och låter browser göra resten för att skapa elementet.

Om man använder det på ett befintligt element så ersätts det med metoden. Exempelvis om main hade haft 3 `<p>` taggar så hade de försvunnit och ersätts av en `<article>` om man gör som nedan:

```js
const main = document.querySelector("main");
const articleAsAString = "<article>This is an article</article>";

// ersätter main's innehåll med bara articleAsAString
main.innerHTML = articleAsAString;
```

Om man gör så här fungerar det att lägga till på befintligt element utan att ta bort de 3 `<p>` taggarna som försvann ovanifrån. Kommer läggas till som `appendChild`. Alltså sista child i `main`.

```js
// plusar på befintlig main's innehåll med articleAsAString
main.innerHTML += articleAsAString;
```

#### insertAdjacentHTML()

Fungerar nästan som insertAdjacentElement men accepterar en string som argument istället för ett HTML element. 

```js
// Multi-line strings fungerar BARA med ` backticks. Användbart i detta fallet istället för en lång string utan utrymme.
const section = 
`<section class="section">
    <p>This is a paragraf inside the section</p>
</section>`;


const main = document.querySelector("main");
main.insertAdjacentHTML("beforebegin", section);

// I detta fallet under blir det duplicerat och flyttar inte bara.

main.insertAdjacentHTML("afterend", section);
```

Strängen blir tillagd som syskon innan `main` elementet.

Om man lägger till `insertAdjacentHTML` två gånger så dupliceras elementet istället för att flytta det. Som det gjorde i `insertAdjacentElement`. Det händer eftersom string variablen är en string, inte en `reference type`. Värdet av stringen är inne i variablen. 



