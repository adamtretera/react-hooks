---
theme: geist
highlighter: shiki
title: React basics
---

# React ? 
- React je Javascriptová knihovna pro vytváření UI
- Co je **UI** ?
<div className="flex justify-center">
<img className="w-1/2 rounded-sm" src="/images/what-is-ui.png"/>
</div>


---
layout: center

---

# User Interface UI
- <span class="text-pink-600">UI</span> myslíme všechny elementy, které uživatel vidí a interaguje.
<div className="flex justify-center ">
<img className="w-1/2 rounded-sm" src="/images/ui-components.png"/>
</div>

---

# User Experience UX 
- <span class="text-pink-600">UX</span> uživatelská zkušenost průchodem webu
- cíl: spokojený uživatel s interakcí na webu
- často se používá wireframe (kostra webu)
<div className="flex justify-center ">
<img className="w-1/4 rounded-sm" src="/images/ux-design-wireframe.png"/>
</div>

---

# Rendering UI
- když se podíváte na jakoukoliv stránku
- na Devtools network tab, uvidíte příchozí HTML dokument
- **browser** vezme HTML ⇒ pak ukáže javascriptu **DOM**, aby jste s ním mohli manipulovat a měnit ( a přidat tím interaktivitu vašim stránkám)
<div className="flex justify-center">
  <img className="w-1/2 rounded-md	" src="/images/html-to-dom.png"/>
</div>

---

# Co je DOM ?
- Je vlastně objektový model **HTML elementů.**
- Je to takový prostředník mezi **HTML** a **UI**

*Stromová struktura (měli by jste znát z Datových struktur)*

- Slouží nám k tomu, aby jsme mohli měnit styly, strukturu a obsah stránek
- nebo poslouchat na nějké eventy
- 
# Vyzkoušet ? ✍️  
- To co vidíte v devtools je DOM


---

# DOM manipulace
- HTML
```html
<html>
  <body>
    <div id="app"></div>
    <script type="text/javascript"></script>
  </body>
</html>
```

- JavaScript
```ts
  const app = document.getElementById('app');
  const header = document.createElement('h1');
  const headerContent = document.createTextNode('React je nejlepší!');
  header.appendChild(headerContent);
  app.appendChild(header);
```
---

# Cvičení 1. 🧪
- Vytvořte html soubor a do něj `<body>` s `div` nesoucí `id` root
- vložte script tag 
```html
<script type="module"> // nebo defer atribut (aby script počkal na načtení DOMu)
```

- pomocí JS vytvořte `<div>` do něj vložte text `"Ahoj DOMe"`
- vložte k němu třídu `card`
- a pak ho přidejte do DOMu
- [DOM manipulace](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents)



---

# Rozdíl mezi DOM vs source kód
- Otevřete DEVtools (f12)
- networku vidíte html - které přišlo (není kompletí)
- při zobrazení DOM v tabu Elements mužeme vidět rozdíl
<div className="flex justify-center">
  <img className="w-1/2 rounded-md	" src="/images/source-code.png"/>
</div>

---

# Proč ? 
- React je nejpoužívanější framwork, ale under the hood stále používá základní [API](https://github.com/facebook/react/blob/48907797294340b6d5d8fecfbcf97edf0691888d/packages/react-dom/src/client/ReactDOMComponent.js#L416) jako vy 
- React přináší více declarativní přístup než imperativní browser api
- **Deklarativní** Co ? - řeším jen výsledek
```js
array.map() 
```

- **Imperativním** Jak ? (step by step) - řeším celý proces
- 
```js
for(let i = 0; i < array.length; i++)
```

- [Declarativní vs Imperativní](https://ui.dev/imperative-vs-declarative-programming)
- říkáme Reactu co dělat a on to za nás udělá = Declarativní přístup
---

# Abstrakce pomocí React
- na začátek přidáme React pomocí
```html
<script src="https://unpkg.com/react@18.1.0/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@18.1.0/umd/react-dom.development.js"></script>
```
DOM operace
```js
const elementProps = {id: 'mujNadpis', children: 'Ahoj Reacte! 👋'}
const elementType = 'h2'
const reactElement = React.createElement(elementType, elementProps)
const root = ReactDOM.createRoot(rootElement)
root.render(reactElement)
```

---

# Cvičení 2
- Překopírujte kód ze cvičení 1.
- pomocí Reactu upravte 
- nechte pouze rootElement pro vypsání do DOMu


--- Cvičení 2.

# WTF ? je to delší ?

- mohli by jsme zkusit udělat něco jako
```js
root.render(<h1>Ahoj Reacte! 👋</h1>); // hodí error
```

- tady příjde na řadu **JSX**
- **JSX** je jazyk pomocí kterého zapisujeme UI podobně jako v HTML
- každopádně browser nerozumí JSX
- proto to potřebujeme přeložit (transform) k tomu slouží nástroj [Babel](https://babeljs.io/repl#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie_mob%2011&build=&builtIns=App&corejs=3.21&spec=false&loose=false&code_lz=MYewdgzgLgBArgSxgXhgHgLYEMFgHxoQAOW-AEgKYA2VIaA9MaXuk_gOogBOVAJg2wL1suPACggA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=false&presets=react&prettier=true&targets=&version=7.19.6&externalPlugins=&assumptions=%7B%7D) 
- na linku můžete vidět jak **JSX** se převede do **JS**

```html
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

---

# Takže můžu udělat něco takového ?

```html
    <!-- Přidávat babel link -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <link rel="stylesheet" href="styles.css" />
    <!-- Tady se přidal type JSX -->
    <script type="text/jsx"> 
      const rootElement = document.getElementById('root');
      const root = ReactDOM.createRoot(rootElement)
      root.render(<h1>Ahoj Reacte! 👋</h1>); 
    </script>
```
Důležité je pochopit, že se jedná o JSX element 
```jsx
<h1>Ahoj Reacte! 👋</h1> // je jsx element
const jsxElement = <h1>Ahoj Reacte! 👋</h1>
root.render(jsxElement); 
```

---

# JSX
- JSX extesion pro psaní JavaScriptu
- je jenom více intuitivní zápis pro React API a jednoduší na čtení
- Musí vracet pouze jeden root element
- 3 pravidla oproti HTML

```js
const ui = <h1 id="nadpis1">Super stránka</h1>

// ↓ ↓ ↓ ↓ compiles to ↓ ↓ ↓ ↓

const ui = React.createElement('h1', {id: 'nadpis1', children: 'Super stránka'})
```

- normálně by jste vzali všechen kód a nechali ho při build time  ⏱️  compliovat do javascriptu

---

# 1. JSX pravidlo - vracet pouze jeden element
- pro vrácení více elemetů ho vždy musíte obalit, tak aby root elemebt byl pouze jeden

```jsx
// Obaluju h1 a img do elemetu div
<div> 
  <h1>Moje super stránka</h1>
  <img src="https://placekitten.com/g/200/300" alt="Adam Tretera">
</div>
```

nebo pokud nechci obalovat do **div** mužu použít takzvaný react fragment 
```jsx
// Obaluju h1 a img do fragmentu 
<> 
  <h1>Moje super stránka</h1>
  <img src="https://placekitten.com/g/200/300" alt="Adam Tretera">
</>
```

---

# 2. JSX pravidlo - zavirat všechny tagy
- samozavírací tagy např. `<img> ==> <img/>`
```jsx
<> 
  <img src="https://placekitten.com/g/200/300" alt="Adam Tretera"/>
</>
```


---

# 3. JSX pravidlo - většinu věcí psát camelCase
- camelCase je adamTretera, mujSuperKomponent
- jiný zápis `class` ==> `className`
```jsx
  <img 
    src="https://placekitten.com/g/200/300" 
    alt="Kočka" 
    onClick=""
    className="photo"
  />
```
---


# Cvičení 3.
- vytvořte jsxElement a vypište ho pomocí funkce `render`

```jsx
  <h1>První stránka v Reactu! 👋</h1>
  <img src="https://placekitten.com/g/200/300" alt="Kočička">
  <ul>
    <li>Java</li>
    <li>Typescript</li>
  </ul>
```

--- 

# React 3 klíčové kocepty
- Komponenty (`Components`) 
- Stav (`state`)
- Vlastnosti (`props`)

---

# Komponenty
- základní stavební jednotka v Reactu
- snažím se kód rozdělit do co nejvíce logických celků
<div className="flex justify-center">
  <img className="w-1/2 rounded-md	" src="/images/components.png"/>
</div>


---

# Komponenty v Reactu
- funkce které vrací JSX element
- musejí začínat velkým písmenem
  
```tsx
function List() {
  return (
    <ul>
      <li>React</li>
      <li>Angualr</li>
    </ul>;
 )
}
// Musím zavírat všechny tagy (JSX pravidlo 2.)
root.render(<List/>)

```
---

# Vnoření komponent

```tsx
function Button() {
  return <button>Click me 🙌</button>
}

function Menu() {
  return (
    <section>
      <Button/>
      <Button/>
      <Button/>
    </section>;
 )
}

```

--- 

# Cvičení 4.
- toto odevzdejte na konci hodiny nebo dodělejte doma
- nestylujte, pouze vytvořte jednoduché JSX komponenty a pak je vykreslete na stránku
<div className="flex justify-center">
  <img className="w-1/2 mt-4 rounded-md	" src="/images/kittens-components.png"/>
</div>
---

# Vytvoření realného projektu
- Pokud nemáte node nainstalujte si [Node](https://nodejs.org/en/download/)
- Ze začátku budeme používat CRU (create-react-app) 
- později [Next.js](https://nextjs.org/)
- vytvořte si složku v pc např. `react-projects` 
- v příkazovém řádku běžte do té složky

```
npx create-react-app nazevMeAppky --template typescript
```
- po dokončení otevřte složku `nazevMeAppky` podle toho jak jste si jí pojmenovali v nějakém IDE (vs-code, WebStorm)
- `npm start` - pomoci příkazu spustíte applikaci
- pokud vše v pořádku aplikace běží na `http://localhost:3000/`


--- 

# Vyčištění projektu
- projdeme si na hodině
- smažte soubory `reportWebVitals.ts`, `App.test.tsx`, `setupTests.tsx`
```tsx
import React from 'react';
import './App.css';

function App() {
  return (
    <div>
        <h1>Ahoj Reacte</h1>
    </div>
  );
}

export default App;
```

---

# Vlastnosti (`props`)
- první parametr React komponentu (funkce)
- můžou být cokoliv (čísla, pole, objekty..)

```tsx
function Add(props) {
  return (
    <div>
      {props.n1} + {props.n2} = {props.n1 + props.n2}
    </div>
  )
}
```

- podobně jako v javascriptu
```ts
add(2,4)
<Add n1={2} n2={3} />
```

---

# Jak to může vypadat ? 

- modifikátory komponenty
 
```tsx

// Komponenta
function Person(props) {
  return <h1>{props.title}</h1>;
}

export default function App() {
  return (
    <main>
      <Person title="Petr Rychlý" />
      <Person title="Mike Ross" />
      <Person title="Harvy Specter" />
    </main>
  );
}

```

---

# Více props

```tsx
function Cat(props) {
  return (
    <div>
      <h1>{props.name}</h1>
      <img src={props.imageUrl} alt={props.name} />
    </div>
  );
}

```
- použití
```tsx
    <Cat name="Petr" imageUrl="http://placekitten.com/200/300" />
    <Cat name="Mike" imageUrl="http://placekitten.com/200/200" />
```

--- 

# Zjednodušení

```tsx
// Komponenta
function Cat(props) {
  let name = props.name;
  let imageUrl = props.imageUrl;

  return (
    <div>
      <h1>{name}</h1>
      <img src={imageUrl} alt={name} />
    </div>
  );
}
```


---

# Použití v praxi

- [destruktulizovat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Unpacking_fields_from_objects_passed_as_a_function_parameter) už v parametru funkce
```tsx
function Cat({ name, imageUrl }) {
  // ...
}

- defaultní hodnota
function Cat({ name = "Anonymní kočička", imageUrl }) {
  // ...
}
```
- v moment, kdy použiju funkci a nespecifikuju `name`, použije se jako defaultní argument tato hodnota
  
```tsx
    <Cat imageUrl="http://placekitten.com/200/300" />
```

---

# Použití s typescriptem

```tsx
// vytvořím interface s názvem CatPropsTypes
interface CatPropsTypes {
  name: string;
  imageUrl: string;
}

// Funguje stejně jako v klasickém typescriptu
function Cat({ name, imageUrl }: CatPropsTypes) {
  return (
    <div>
      <h1>{name}</h1>
      <img src={imageUrl} alt={name} />
    </div>
  );
}

```

---

# Children (obalování jiných komponent)

```tsx
function Card({ children }) {
  return (
    <article className="card">
      {children}
    </article>
  );
}
```

- přidáme typescript

```tsx
import type { ReactNode } from "react"
// ReactNode není primitvní typ jedná se o typ, přímo z knihovny React

interface CardPropsTypes {
  children: ReactNode
}

function Card({ children }: CardPropsTypes) {
// ...
}

```


---

# Úkol 
- Vytvořte novou React aplikaci (pokud nemáte)
- vytvořte komponentu `Card`, která bude jen obalovat všechny vaše kartičky
- dále vytvořte komponentu `UserCard`
- dále vytvořte kompnentu `BookCard` 
- stylování řešit nemusíte
<div className="flex justify-center">
  <img className="w-1/2 rounded-md	" src="/images/ukol-knihovna.png"/>
</div>


---

# Tips

- template literal
```tsx
function Header({ title }) {
  return <h1>{`Cool ${title}`}</h1>;
}
```

- funkce mimo komponentu
  
```tsx
function generateRandomName(title) {
//... logika pro vrácení náhodného jména
}

function UserProfil() {
  return <h1>{generateRandomName()}</h1>;
}
```

---

# Zpracování pole v Reactu
- velmi důležité
- často vám přijde ze serveru hodně dat, toto jsou z 90% pole
- v `Reactu` chceme např. pro každou položku v poli vykreslit komponent


```tsx
const users = ["Petr", "Lukáš", "Šimon", "Jenda"];
```

- cílem je vykresil několik komponent

```tsx 
function UserList() {
  return (
    <section>
      <h1>Soupis uživatelů</h1>
      {users.map((name) => (
        <h5>{name}</h5>
      ))}
    </section>
  );
}
```

---

# Pomocí komponenty

```tsx
const users = ["Petr", "Lukáš", "Šimon", "Jenda"];

function User({ name }) {
  return <h1>{`Epic ${name}`}</h1>;
}
```

```tsx 
function UserList() {
  return (
    <section>
      <h1>Soupis uživatelů</h1>
      {users.map((user) => <User name={name}/>)}
    </section>
  );
}
```

---

# Array of Objects

```tsx
const users = [
  {
    name: "Mike Ross",
    age: 13,
    img: "https://placem.at/people?w=200"
  },
  {
    name: "Petr Mára",
    age: 49,
    img: "https://placem.at/people?w=200"
  }
];

```

- velmi časté

```tsx
 <section>
      <h1>Soupis uživatelů</h1>
      {users.map((user) => <User name={user.name} age={user.age}/>)}
      {/* Nyní je user objekt */}
 </section>
```

---


# Nebo


```tsx
function UserList() {
  return (
  <section>
        <h1>Soupis uživatelů</h1>
        {users.map(({name, age}) => <User name={name} age={age}/>)}
        {/* Nyní je user objekt */}
  </section>
  )
}

```

```tsx
function UserList() {
  return (
  <section>
        <h1>Soupis uživatelů</h1>
        {users.map((user) => <User {...user}/>)}
        {/* Nyní je user objekt */}
  </section>
  )
}

```

---


# Úkol 
- předělejte aplikaci knihovny pomocí `props`
- nestylujte
- odevzdejte na classroom

