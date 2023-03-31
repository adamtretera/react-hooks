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

# Side effects
- při tvorbě aplikace se často chceme (potřebujeme) synchronizovat s externími systémi
- Např.
  - Network requests (api)
  - timeouts / intervals (animace)
  - braní dat nebo zápis dat do `localStorage`
  - poslouchání na globální eventy
- v Reactu jim říkáme side effecty
- jak to dělat správně ? 💡


---


# useEffect()
`useEffect(setup, dependencies?)`
- `setup` - je funkce je umístěná logika celého efketu
- `dependencies` - (nepovinný) - pole závislostí, pokud se změní, tak se spustí `setup` znovu, může obsahovat `props`, `state`  nebo jiné proměnné deifnované v komponentě
- pokud je pole `dependencies` prázdné [], tak se `setup` spustí jen jednou (při mountu komponenty)


---

# Příklad

```js
const [count, setCount] = useState(0);

useEffect(() => {
 document.title = count.toString();
}, [count]);
```

---

# Úkol - reagování na změnu

- vytvořte formulář
```ts
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
```
- v moment kdy se změní jméno nebo heslo vypište ho do konzole

---

# useEffect - on mount
- když chci aby se stalo něco na mount komponenty (zobrazení)
- bacha ve strict modu se provede 2x
```tsx
  useEffect(() => {
    console.log('Aya 👻');
  }, []);
```

---

# Příklad - on mount 

- Focus input na on mount
- https://stackblitz.com/edit/react-ts-yamf3d


---

# Úkol - on mount
- přidat na okno (window) event 
- pomocí funkce `addEventListener`
- event `resize` => který bude volat funkci handleResize, kde změní stav
```jsx
setScreenSize({
  width: window.innerWidth,
  height: window.innerHeight,
});
```
---

# useEffect - clean up

- zavolá se v moment, kdy se komponenta unmountuje (schová se)

```tsx
useEffect(() => {
      return () => console.log('Aya 👻');
}, []);
```

---

# Example - clean up
- https://stackblitz.com/edit/react-ts-yamf3d?file=CleanUp.tsx

---

# Úkol - clean up
- opravte předešlé cvičení
- smažte event listener pomocí funkce `removeEventListener` na onmount komponenty
- vyzkoušejte: přidejte logiku, kdy se komponeta zobrazí. (např. checkbox)


---

# Api
```jsx
let [dogImage, setDogImage] = useState(null)

useEffect(() => {
  fetch("https://dog.ceo/api/breeds/image/random")
          .then(response => response.json())
          .then(data => setDogImage(data.message))
},[])
```



---

# DOM

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

# Custom hooks
- vytvoříme si vlastní hook
```tsx
function useTime() {
  const [time, setTime] = React.useState(
    new Date()
  );
  
  React.useEffect(() => {
    // Effect logic
    const intervalId = window.setInterval(() => {
      setTime(new Date());
    }, 1000);
    
    return () => {
      window.clearInterval(intervalId);
    };
  }, []);
  
  return time;
}
```

---

# Custom hook - cvičení
- vytvořte si custom hook `useToggle`
```tsx
import React from 'react';

function useToggle() {
  // TODO: Fill me in!
}

export default useToggle;


```

- bere jako parametr `initialValue` (boolean)
- shown, toggle, setShown, 

---

# Fetch
- moderní náhrada za `XMLHttpRequest`

- vracení dat
```js
async function getData() {
  const response = await fetch('/api/data');
  const json = await response.json();
  // `json` data jsou vácená ve formátu JSON z API
}
```

- voláme funkci `fetch` s API endpointem => `/api/data`
- fetch je založený na promisech
- čekáme na vrácení response pomocí `await`
- `response` je objekt ve kterým se nachází hlavičky a status cody


---

# Fetch - možnosti requestu
- defaultně je `GET` request
- `GET` `POST` `PUT` `PATCH` `DELETE`
```ts
async function submitData() {
  const response = await fetch('/api/data', {
    method: 'POST',
  });
  const json = await response.json();
}
```

---

# Fetch - možnosti requestu
- druhý argument nám slouží k nastavení ruzných možností


```ts
async function submitData() {
  const response = await fetch('/api/data', {
    method: 'POST',
    headers: {
      'Authorization': 'bearer abc123',
      // nastavení hlavičky (authetication)
    },
  });
  const json = await response.json();
}
```

---

# Fetch - query params
- když provádíme requesty na API, tak se často používají query params
- často pro `GET` requesty
- query params jsou v url za `?` a oddělené `&` (key=value)
```ts
async function search({ name, city }) {
  const url = `/api/search?name=${name}&city=${city}`;

  const response = await fetch(url);
  const json = await response.json();
}
```

---

# Fetch - body params
- často pro POST/PUT/PATCH/DELETE requesty
```ts
async function login({ username, password }) {
  const response = await fetch(`/api/login`, {
    method: 'POST',
    body: JSON.stringify({
      username,
      password,
    }),
  });

  const json = await response.json();
}

```
- musíme nejdříve převést data na string (protože můžeme posílat po síti pouze stringy)
- `JSON.stringify` převede objekt na string
- `JSON.parse` převede string na objekt - toto palk použije Backend (server)

---

# React fetch - on event

```ts
  const [email, setEmail] = React.useState('');
  const [message, setMessage] = React.useState('');
  
  const [status, setStatus] = React.useState('idle');
  
  async function handleSubmit(event) {
    event.preventDefault();
    setStatus('loading');

    const response = await fetch(ENDPOINT, {
      method: 'POST',
      body: JSON.stringify({
        email,
        message,
      }),
    });
    const json = await response.json();

    if (json.ok) { setStatus('success'); setMessage(''); } else {
      setStatus('error');
    }}
  
```

---

# React fetch - on mount

```tsx
  const [data, setData] = React.useState(null);
  const [error, setError] = React.useState(null);
  const [loading, setLoading] = React.useState(false);

  React.useEffect(() => {
    async function fetchData() {
      setLoading(true);
      try {
        const response = await fetch(ENDPOINT);
        const json = await response.json();
        setData(json);
      } catch (error) {
        setError(error);
      } finally {
        setLoading(false);
      }
    }

    fetchData();
  }, []);
```


# React fetch - production ready

```tsx
  const [data, setData] = React.useState(null);
  const [error, setError] = React.useState(null);
  const [loading, setLoading] = React.useState(false);

  React.useEffect(() => {
    async function fetchData() {
      setLoading(true);
      try {
        const response = await fetch(ENDPOINT);
        const json = await response.json();
        setData(json);
      } catch (error) {
        setError(error);
      } finally {
        setLoading(false);
      }
    }

    fetchData();
  }, []);
```

---

# React fetch - useSWR()

```tsx
  const { data, error } = useSWR(ENDPOINT, fetcher);

  console.log(data, error);

return (
        <p>
          Current temperature:
          {typeof data?.temperature === 'number' && (
                  <span className="temperature">
          {data.temperature}°C
        </span>
          )}
        </p>
);
```

---

# React fetch - useSWR() - fetcher

```ts
// fetcher 
async function fetcher(endpoint) {
  const response = await fetch(endpoint);
  const json = await response.json();
  
  return json;
}
```

---

# Úkol - fetch
- pokédex :)) 
- vytvořte applikaci - kde se vypíšou pokemoni v kartičkách
- na každé kartičce bude obrázek, jméno a typ
- po kliknutí na kartičku se zobrazí detail pokémona (nový route)
- detail pokémona bude obsahovat obrázek, jméno, typy, výšku, váhu, popis
- použijte API https://pokeapi.co/
- vytovřte nový projekt - (nextjs) - uložte na github
- Bonus - přidejte možnost vyhledávání pokémonů (v navbaru)




---

# Opakování - useEffect()

- api s kterým budete pracovat [api](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
```tsx
// Uložení do localstorage
window.localStorage.set('is-dark-mode');

// Vrácení hodnoty
window.localStorage.getItem('is-dark-mode');
```

- Hodnota `isDarkMode` by měla být uložena v local storage pokaždé když se změní pomocí `useEffectu`
- Prvotní hodnota `isDarkMode` by se měla brát z `localstorage` (nebo nastavená na `false` pokud nemá žádnou hodnotu)
- klíč v `localstorage` může být například `"is-dark-mode”`

---

# Opakování - localStorage (ukol nebude fungovat v Nextu - z důvodu, že je server side rendered)
- Položky uložené v `localStorage` jsou vždy uloženy jako řetězec. Budete muset převést uloženou hodnotu zpět na boolean. To můžete udělat pomocí `JSON.parse()`
```jsx
<div className="wrapper">
      <button
        style={{
          border: 'none',
          backgroundColor: isDarkMode ? 'black' : 'white',
          color: isDarkMode ? 'white' : 'black',
        }}
        aria-label="Dark Mode"
        // TODO: onClick={}
      >
        Toggle
        {isDarkMode ? ' 🌑' : ' 🔆'}
      </button>
    </div>
```

---

# useContext
- `useContext` umožňuje vnořeným komponentám přístup k datům (tzv. kontextu), které jsou poskytovány rodičovskou komponentou.
- Kontext může být použit pro předání dat, které jsou společné pro několik komponent v hierarchii.

```tsx
const ThemeSwitcher = () => {
  const { theme } = useContext(ThemeContext);
  
  return (
    <div>
      <p>Current theme: {theme}</p>
    </div>
  );
};
```

---

# useContext - řešení prop drillingu
- Použitím useContext můžeme předcházet tzv. "prop drilling", což je situace, kdy musíme předávat data z rodičovských komponent do vnořených komponent pomocí 

```jsx
          <div>
            <h1>My App</h1>
            <UserProfile data={userData} />
            <UserSettings
                    data={userData}
                    handleNameChange={handleNameChange}
                    handleAgeChange={handleAgeChange}
            />
          </div>
```


---

# useContext - příklad (vytvoření kontextu)
- nejprve typy vytvoříme kontext
```tsx
type AppContextType = {
  user: User | null;
  setUser: (user: User | null) => void;
};

export const AppContext = createContext<AppContextType>({
  user: null,
  setUser: () => {},
});
```

---

# useContext - příklad (vytvoření provideru)

```tsx
import React, { useState } from "react";
import { AppContext } from "./AppContext";

function AppProvider({ children }: { children: React.ReactNode }) {
  const [user, setUser] = useState<User | null>(null);

  return (
    <AppContext.Provider value={{ user, setUser }}>
      {children}
    </AppContext.Provider>
  );
}
```

---


# useContext - příklad (použití provideru)

`<AppContext.Provider>` musí být nad komponentou, která používá volání useContext(). 
```tsx
function MyPage() {
  return (
          <AppProvider>
            <App /> // Tady nyní můžu používat 
          </AppProvider>
  );
}
```


---

# useContext - příklad (použití)

```tsx
import React, { useContext } from "react";
import { AppContext } from "./AppContext";

const ProfileCard = () => {
  const { user } = useContext(AppContext);

  return (
    <div>
      {user ? (
        <>
          <h2>{user.name}</h2>
          <p>Age: {user.age}</p>
          <p>Email: {user.email}</p>
        </>
      ) : (
        <p>No user found.</p>
      )}
    </div>
  );
};
```

---

# Další příklad použití

```tsx
import { useContext } from 'react';

function Button() {
  const theme = useContext(ThemeContext)
  // rest of the component
}


function MyPage() {
  return (
          <ThemeContext.Provider value="dark">
            <SubmitForm /> 
            // Tady můžu používat tlačítko
          </ThemeContext.Provider>
  );
}
```




---

# Úkol - useContext

- `ThemeContext`, který obsahuje objekt `theme` a funkci `setTheme`
- `useTheme`, který získává hodnoty `theme` a `setTheme` z kontextu a vrací je jako objekt

---



# useReducer 

- `useReducer` je hook v Reactu, který umožňuje spravovat stav aplikace pomocí reduceru.
- Reducer je funkce, která bere aktuální stav a akci a vrací nový stav.
- Použitím `useReducer` můžeme oddělit správu stavu od komponenty a snížit tak závislost na životním cyklu Reactu.

---

# useReducer - Jak ho použít (typy) ?

```tsx
type StateType = {
  todos: { id: number; text: string; done: boolean }[];
};

type ActionType =
  | { type: "add"; text: string }
  | { type: "toggle"; id: number }
  | { type: "delete"; id: number };
```

---

# useReducer - Jak ho použít (reducer) ?

```tsx
const reducer = (state: StateType, action: ActionType): StateType => {
  switch (action.type) {
    case "add":
      return {
        todos: [
          ...state.todos,
          { id: Date.now(), text: action.text, done: false },
        ],
      };
    case "toggle":
      return {
        todos: state.todos.map((todo) =>
          todo.id === action.id ? { ...todo, done: !todo.done } : todo
        ),
      };
    case "delete":
      return {
        todos: state.todos.filter((todo) => todo.id !== action.id),
      };
    default:
      throw new Error("Unexpected action");
  }
};
```


---

# useReducer - Jak ho použít (použití) ?
- bere jako první argument funkci reduceru a jako druhý argument počáteční stav.
- `useReducer` vrací dva prvky: aktuální stav a funkci pro dispatchování akcí.

```tsx
const [state, dispatch] = useReducer(reducer, { todos: [] });
```


--- 

# useReducer - vytvoření dispatch funkcí

```tsx
const handleAddTodo = () => {
  if (newTodo !== "") {
    dispatch({ type: "add", text: newTodo });
    setNewTodo("");
  }
};

const handleToggleTodo = (id: number) => {
  dispatch({ type: "toggle", id });
};

const handleDeleteTodo = (id: number) => {
  dispatch({ type: "delete", id });
};
```
---

# useReducer - v komponentě

```tsx
return (
  <div>
    <ul>
      {state.todos.map((todo) => (
        <li
          key={todo.id}
          onClick={() => handleToggleTodo(todo.id)}
          style={{ textDecoration: todo.done ? "line-through" : "none" }}
        >
          {todo.text}
          <button onClick={() => handleDeleteTodo(todo.id)}>Delete</button>
        </li>
      ))}
    </ul>
    <input
      type="text"
      value={newTodo}
      onChange={(e) => setNewTodo(e.target.value)}
    />
    <button onClick={handleAddTodo}>Add Todo</button>
  </div>
);
```

# useReducer 

```tsx
import { useReducer } from 'react';

type State = {
  age: number;
};

type Action = {
  type: 'incremented_age';
};

function reducer(state: State, action: Action): State {
  if (action.type === 'incremented_age') {
    return {
      age: state.age + 1
    };
  }
  throw new Error('Unknown action.');
}

export default function Counter() {
  const [state, dispatch] = useReducer(reducer, { age: 42 });

  return (
    <>
      <button onClick={() => {
        dispatch({ type: 'incremented_age' })
      }}>
        Increment age
      </button>
      <p>Hello! You are {state.age}.</p>
    </>
  );
}

```


---


# Úkol - useReducer
- Postavte aplikaci košíku na nákupy: Sestavte e-commerce aplikaci košíku na nákupy pomocí Reactu a Reduceru. Aplikace by měla umožňovat uživatelům přidávat položky do košíku, upravovat množství a přejít k objednávce. Pomocí Reduceru spravujte stav košíku.
- akceptační kritéria:
- přidávání, odebírání, množství, typ, smazat vše...




