---
layout: page
title: React - Prop children
---

# 📘 React — A prop especial `children`

## 📌 O que é a prop `children`?

No React, **`children` é uma prop especial** que **não precisa ser declarada explicitamente**.  
Ela é **automaticamente passada** para todo componente customizado e representa **o conteúdo que fica entre a tag de abertura e fechamento do componente**.

---

## 🧩 Exemplo de uso

### Uso do componente no App

```jsx
<Modal>
  <h2>Warning</h2>
  <p>Do you want to delete this file?</p>
</Modal>
```

➡️ Tudo que está dentro de `<Modal>...</Modal>` será automaticamente enviado para o componente via `props.children`.

### ⚙️ Implementação do componente Modal

```jsx
function Modal(props) {
  return (
    <div id="modal">
      {props.children}
    </div>
  );
}
```

**O que acontece aqui?**

- `props.children` recebe: `<h2>Warning</h2>` e `<p>Do you want to delete this file?</p>`
- O componente não precisa saber previamente quais elementos vai renderizar
- Ele apenas exibe o conteúdo recebido, funcionando como um wrapper (contêiner)

---

## 🔁 Fluxo de funcionamento

1. **Componente pai (App)** → Usa `<Modal>` e define o conteúdo interno
2. **React** → Detecta conteúdo entre as tags e injeta em `props.children`
3. **Componente filho (Modal)** → Renderiza `{props.children}` no local desejado

---

## 🎯 Por que children é tão importante?

### ✅ Benefícios

- ✨ Reutilização de componentes
- 🎨 Layouts flexíveis
- 📦 Separação de responsabilidades
- 🔌 Componentes genéricos e desacoplados

### Exemplos comuns de uso

- Modais
- Cards
- Layouts
- Containers
- Wrappers de autenticação

---

## 🧠 Regra mental

**Tudo que fica entre as tags de um componente vira `props.children`.**

---

## 📌 Exemplo adicional

```jsx
<Card>
  <h3>Título</h3>
  <p>Descrição do conteúdo</p>
</Card>

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}
```

---

## ✨ Boas práticas

**Prefira desestruturar `children`:**

```jsx
function Modal({ children }) {
  return <div>{children}</div>;
}
```

**Use `children` quando:**

- O conteúdo interno varia
- O componente é mais estrutural do que específico
