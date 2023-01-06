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
  const [numberOfLikes, setNumberOfLikes] = useState(0);
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
  padding: "2rem 1rem"
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

