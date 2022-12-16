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


