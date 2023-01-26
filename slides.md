---
theme: geist
highlighter: shiki
title: React hooks
---

# React hooks 🪝
- pomocné funkce v Reactu (doslova funkce :) )

---

# useState()
- slouží k zapamatování a updatování nějkého stavu v komponentě
```tsx
import { useState } from 'react';
```

- musí být použit ve komponentě !!!
```tsx
function Card() {
  const [numberOfLikes, setNumberOfLikes] = useState(0);}
```

- `numberOfLikes` (první hodnota) - je hodnota stavu  
- `setNumberOfLikes` (první hodnota) - funkce pro změnu stavu
- (`0`) (hodnota v závorách) - je prvotní hodnota
  
---

# useState() - zobrazení stavu

```tsx
import { useState } from 'react';

function Card() {
  const [numberOfLikes, setNumberOfLikes] = useState(0);

  return (
    <article>
      <h4>{numberOfLikes}</h4>
    </article>
  )
}


```

  <article>
      <h4>0</h4>
  </article>

--- 

# useState() - změna stavu

```tsx
function Card() {
  const [numberOfLikes, setNumberOfLikes] = useState(0);

  // Funkce, kterou zavoláme pro změnu stavu (může být i inline)
  const handleClick = () => {
    setNumberOfLikes(numberOfLikes + 1)
  }

  return (
    <article>
      <h4>{numberOfLikes}</h4>
      <button onClick={handleClick}>Like</button>
    </article>
  )
}
```

---

# useState() - ukázka




<Stackblitz source="react-ts-bdfysz" :openFiles="[`components/Like.tsx`]" />

---

# Úkol 🧪
- vytvořte Input, který když do něj budete psát bude zobrazovat délku slova na dalším řádku
- input bere funkci onChange (stejně jako onClick u buttonu)
- pokud nevíte podívejte se na lekci v React Basics - Eventy
```ts
function handleOnChange(event: React.ChangeEvent<HTMLInputElement>) {
  // event při onChange stavu
}

```

---

# useState - posílání stavu

```tsx
export default function MyApp() {
  const [count, setCount] = React.useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Společný stav</h1>
      <Button count={count} onClick={handleClick} />
      <Button count={count} onClick={handleClick} />
    </div>
  );
}

```

---

# useState - ukázka

<Stackblitz source="react-ts-nsbzpm" :openFiles="[`App.tsx`]" />

---

# Dobrovolný úkol na známku (15%)
- vyvořte aplikaci, která bude zobrazovat list filmů
- každý film bude mít svůj vlast stav na počet hvězdiček (1-5) (nelekejte se berte je jako tlačítka)
- nastyljte - můžete použít co chcete (nemusí vypadat jako vzor)
  
<div className="flex justify-center">
<img className="w-1/2 rounded-sm" src="/images/movies.png"/>
</div>

---

# Next.js

```bash
npx create-next-app@latest --ts

```

- jednoduchý file based route systém
- automatický code spliting
- pre-rendering (o tom později)
- [next dokumentace](https://nextjs.org/)

---

# Routes

- v nextu je stránka, kalasická react komponenta, která je ve složce `pages`
- např. `pages/moje-portfolio.tsx` 
- nyní bude v aplikaci dostupný /moje-portfolio
- `pages/index.tsx` je pro `/`


```tsx
export default function MojePortfolio() {
  return <h1>Moje projekty</h1>
}

```

---

# Link

- slouží pro přechod z jedné stránky na jinou

```tsx
  <Link href="/">Home</Link>
```



```tsx
import Link from 'next/link'

function Navbar() {
  return (
    <div>
      <Link href="/">Dashbaord</Link>
      <Link href="/eshop">Eshop</Link>
    </div>
  )
}
```

---


# Úkol - vytvořte next appku
- vytvořte next appku
- s navigací mezi stránkami 
- `About`, `Projects`, `Contact`

  
---

# Stylování

- co jsme si ukázali (inline)
- CSS in JS
- modules
- tailwind 

---

# CSS in JS
- pro reagování na stav komponenty
- atomické třídy
- předcházení kolizí
- DX 

---

# Zástupci
- [styled-components](https://styled-components.com/docs/basics) 💅 
  - nejrozšířenější
- [emotion](https://emotion.sh/docs/introduction)
- [stitchescss](https://stitches.dev/)
  - můj oblíbenec 
- [felacss](https://fela.js.org/)

---

# Styled coponents

```jsx
const Button = styled.button`
  /* Adapt the colors based on primary prop */
  background: ${props => props.primary ? "palevioletred" : "white"};
  color: ${props => props.primary ? "white" : "palevioletred"};

  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

render(
  <div>
    <Button>Normal</Button>
    <Button primary>Primary</Button>
  </div>
);

```

---

# Stitches

```jsx
const Button = styled('button', {
  padding: "2rem 1rem",
  //... base styles

  variants: {
    color: {
      violet: {
        backgroundColor: 'blueviolet',
        color: 'white',
      },
      gray: {
        backgroundColor: 'gainsboro',
      },
    },
  },
});

() => <Button color="violet">Button</Button>;
```

--- 

# Modules CSS
- dobré na začátky
- klasické css, jen modulární (neřešíte překrývání)
- lokální scope vlastností
- nemusíte nic stahovat je přímov v nextu [css-modules](https://github.com/css-modules/css-modules)
---

# Příklad

- Button.tsx
- `Button.module.css`

```css
.error {
  color: white;
  background-color: red;
}
```

- `Input.module.css`

```css
.error {
  color: red;
  background-color: white;
}
```

--- 


# Použití v komponentě

```tsx
import styles from './Button.module.css'

export function Button() {
  return (
    <button
      type="button"
      className={styles.error}
    >
      Remove
    </button>
  )
}
```
---

# Tailwind CSS

- atomické třídy
- co vlastnost, to třída (vlastní config na barvy atp)
- just in time compiler (co za třídy napíšete do budete mít v bundlu)
```html
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Button
</button>
```
---

# UI knihovny
- když vás nezajíma design
- nebo váš osobní projekt


# Obecné UI knihovny
- [antd design](https://ant.design/)
- [mantine](https://mantine.dev/)
- [Chakra](https://chakra-ui.coma)
- MUI

---

# Primitives (headless) komponenty
- nenastylované komponenty pouze (accessible) - podle aria
- težší na začátek, ale vyplatí se při custom appce
- [Radix UI](https://www.radix-ui.com/)
- [React aria](https://react-spectrum.adobe.com/react-aria/)
- Reach UI


---

# Formuláře
- velmi neoblíbená část frontendového vývoje
- ale velmi důležitá (Google.com, Facebook.com) 
- je zde hodně balíčků, které vám usnadní práci (formik, react-hook-form, react-final-form), ale nejsou nezbytné


---

# Ukázka formuláře

```jsx
<form>
  <label>
    Name:
    <input type="text" name="name" />
  </label>
    <label>
    
        Heslo:
        <input type="password" name="password" />
    </label>
  <input type="submit" value="Submit" />
</form>
```

- typy [inputů](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) (file, text, number, checkbox, radio, date, email, password

---

# Uncontrolled forms
- nenastavujeme `value`
- pomocí `useRef()`
  <Stackblitz source="react-ts-jgrqas" :openFiles="[`components/App.tsx`]" />

---

# useRef()
- `const ref = useRef(initialValue)`
- pro přístup k DOM elementům (jejich referenci)
- ale muže sloužit k jakékoliv vaší vlastní referenci (funkce, objekty)
<Stackblitz source="react-ts-jgrqas" :openFiles="[`UseRefExample.tsx`]" />

---


# Kontrolované formuláře 
- pomocí `useState("")` - vždy musí obsahovat defaultní hodnotu
- kontrolované přímo react - pro nás více důležité
<Stackblitz source="react-ts-yyzrj8" :openFiles="[`components/App.tsx`]" />

  
---

# Úkol
- vytvořte přihlašovací formulář (kontrolovaný) (email, heslo, potvrzení hesla, checkbox)
- pokud uživatel nebude souhlasit s podminkami - nedovolte mu odeslat formulář
- pokud  heslo a potvrzení hesla nebudou stejná - nedovolte mu odeslat formulář
- vytvořte select (výběrové menu) - (volby: vyberte, muž, žena, jiné)


---

# Kontrolvané formuláře vs Nekontrolvané formuláře

- pokud nastavujeme `value` na inputu, tak je to kontrolvaný formulář (react kontroluje jeho hodnotu)
- pokud ne, tak je to nekontrolvaný formulář
- Komponenta by měla vždy být buď kontrolovaná nebo nekontrolovaná, nikdy oběma způsoby


--- 

# Častá chyba
- pokud je formulář kontrolvaný, tak `useState()` musí mít defaultní hodnotu
```jsx
function SignupForm() {
  const [username, setUsername] = React.useState();   // Bez defualtní hodnoty : hodí error (A component is changing an uncontrolled input to be controlled.)
    
    return (
    <form>
      <label htmlFor="username">
        Select a username:
      </label>
      <input
        type="text"
        id="username"
        value={username}
        onChange={event => {
          setUsername(event.target.value);
        }}
      />
    </form>
  );
}
```

---

# Proč ? 
- je to z toho důvodu, že je to jako kdyby jsme do `value` dávali `undefined`
- pokud nastavíme hodnotu na `undefined`, tak je to jako kdyby jsme jí vůbec nenastavili (nekontrolovaný formulář)
```jsx
const username = undefined; 

<input
  type="text"
  id="username"
  value={username}
  onChange={event => {
    setUsername(event.target.value);
  }}
/>
```
--- 

# Submit formuláře
- mám formulář
```tsx
export function ClickForm({ onSearch }: ISearchFormProps) {
  const [searchTerm, setSearchTerm] = useState('');

  return (
    <section>
      <input
        type="text"
        value={searchTerm}
        onChange={(event) => {
          setSearchTerm(event.target.value);
        }}
      />
      <button>Hledej!</button> {/* Chci aby se spustila funkce onSearch */}
    </section>
  );
}


```

---

# Pomocí onClick ?

```tsx
<button onClick={() => onSearch(searchTerm)}>Search!</button>
```
- co když ale budu chtít, aby se odeslal na `Enter` ? 

```tsx
<>
<input
    type="text"
    value={searchTerm}
    onChange={(event) => {
        setSearchTerm(event.target.value);
    }}
    onKeyDown={(event) => {
        if (event.key === 'Enter') {
            onSearch(searchTerm);
        }
    }}
/>
</>
```
- to by šlo, ale budeme vytvářet něco co už prohlížeč dávno umí


---

# onSubmit
- `onSubmit` je event, který se spustí, když se odesílá formulář
- `event.preventDefault()` - zabrání odeslání formuláře (a tím i refreshu stránky) - dříve takto prohlížeče odkazovaly na stránku, kde byla dostupna stránka s novými daty

```tsx
const handleSubmit = (event: SyntheticEvent) => {
    event.preventDefault();
    onSearch(searchTerm);
};
return (
    <form onSubmit={handleSubmit}>
        <input
            type="text"
            value={searchTerm}
            onChange={(event) => {
                setSearchTerm(event.target.value);
            }}
        />
        <button>Hledat!</button>
    </form>
)
```

---

# Props vs State
- props - vlastnosti komponenty, které jsou nastaveny z vnějšku (podobně jako atributy v HTML)
```jsx
<Button variant="secondary">
```
- state - pokud chceme aby se něco měnilo
```jsx
<Button disabled={isAdmin}>
```
- nikdy nemodifikujeme přímo state (pokud chceme změnit stav, tak použijeme `setState`)


---

# Props vs State

<Stackblitz source="vitejs-vite-tnte6p" :openFiles="[`src/components/PropsVsState.tsx`]" />



---

# Examples
- https://stackblitz.com/edit/vitejs-vite-tnte6p
- https://stackblitz.com/edit/vitejs-vite-pafk6p (pro pokročilé - přidat funkci na přidání barvy)

---

# Lifting state up
- pokud chceme mít `state` ve více komponentách - musíme ho přesunout ve struktuře nad ty komponenty pro kterého ho chceme použít
- přesouváme `state` do komponenty, která je nejvyšší v hierarchii
```jsx
<>
      <header>
        <a className="logo" href="/">
            My Fruits
        </a>
        <SearchForm />
      </header>
      <main>
        <SearchResults />
      </main>
</>
```

--- 

# Lifting state up

```jsx
function App() {
    const [searchTerm, setSearchTerm] = React.useState('');

    return (
        <>
            <header>
                <a className="logo" href="/">
                    My Fruits
                </a>
                <SearchForm
                    searchTerm={searchTerm}
                    setSearchTerm={setSearchTerm}
                />
            </header>
            <main>
                <SearchResults searchTerm={searchTerm} />
            </main>
        </>
    );
}
```

---

# Úkol - cookie clicker
- akceptační kritéria
- vytvořit komponentu `CookieClicker`, která bude zvětšovat counter, který se bude nacházet v jiné komponentě
- obrázek si zvolte sami, ale po najetí myší se obrázek zvětší - použijte `:hover` pseudo selector (transform: scale(1.05);)

<img src="/images/img.png" alt="drawing" width="200"/>


---
 
# Example
- https://stackblitz.com/edit/vitejs-vite-z41dfz

---

# useEffect()
`useEffect(setup, dependencies?)`
- `setup` - je funkce je umístěná logika celého efketu
- `dependencies` - (nepovinný) - pole závislostí, pokud se změní, tak se spustí `setup` znovu, může obsahovat `props`, `state`  nebo jiné proměnné deifnované v komponentě
- pokud je pole `dependencies` prázdné [], tak se `setup` spustí jen jednou (při mountu komponenty)




```jsx

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useEffect(() => {
  	const connection = createConnection(serverUrl, roomId);
    connection.connect();
  	return () => {
      connection.disconnect();
  	};
  }, [serverUrl, roomId]);
}


```

---

---

# Použití

- network requesty
- browser DOM
- časovač pomocí setInterval() and clearInterval().
- eventy typu -  window.addEventListener() and window.removeEventListener()
- animace z externích knihoven


```jsx

  useEffect(() => {
    function handleMove(e) {
      setPosition({ x: e.clientX, y: e.clientY });
    }
    window.addEventListener('pointermove', handleMove);
    return () => {
      window.removeEventListener('pointermove', handleMove);
    };
  }, []);

```
---



# Sledování kurzoru

<Stackblitz source="react-ts-lpj3ry" :openFiles="[`components/App.tsx`]" />

---



