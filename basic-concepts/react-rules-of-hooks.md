---
layout: page
title: React - Rules of Hooks
---

# 📘 React Hooks — Regras Fundamentais (Rules of Hooks)

## 📌 O que são Hooks?

Hooks são funções especiais do React que permitem:
- Usar **estado** (`useState`)
- Trabalhar com **ciclo de vida** (`useEffect`)
- Compartilhar lógica reutilizável entre componentes

> ⚠️ Hooks só funcionam corretamente quando algumas regras são respeitadas.

---

## ⚠️ Rules of Hooks

O React define **duas regras principais** para o uso de Hooks.  
Essas regras garantem que o React consiga **controlar corretamente o estado e o ciclo de vida** dos componentes.

---

## 1️⃣ Only call Hooks inside of Component Functions

> **Hooks só podem ser chamados dentro de componentes React ou hooks customizados.**

### ✅ Correto

```jsx
function App() {
  const [val, setVal] = useState(0);
}
```

- O Hook está dentro da função do componente
- O React consegue associar corretamente o estado ao componente

### ❌ Incorreto

```jsx
const [val, setVal] = useState(0);

function App() {
  // ...
}
```

- O Hook está fora do componente
- O React não sabe a qual componente esse estado pertence

### 📌 Regra prática

- ❌ Não chame Hooks fora de componentes React
- ✅ Sempre use Hooks dentro de componentes ou hooks customizados

---

## 2️⃣ Only call Hooks on the top level

Hooks devem ser chamados sempre no nível mais alto da função.

Eles não podem estar dentro de:
- `if`
- `for`
- `while`
- funções internas
- blocos condicionais

### ✅ Correto

```jsx
function App() {
  const [val, setVal] = useState(0);

  if (val > 0) {
    // lógica condicional
  }
}
```

- O Hook é chamado em toda renderização
- A ordem de execução permanece consistente

### ❌ Incorreto

```jsx
function App() {
  if (someCondition) {
    const [val, setVal] = useState(0);
  }
}
```

- O Hook pode ou não ser executado
- Isso quebra a ordem interna dos Hooks no React

---

## 🧠 Por que essa regra existe?

O React **não identifica Hooks pelo nome**, mas **pela ordem em que são chamados**.

### Exemplo simplificado:

```
1º → useState()
2º → useEffect()
3º → useState()
```

Se essa ordem mudar entre renderizações:
- Estados podem ser associados incorretamente
- Bugs difíceis de identificar podem surgir

---

## 🛑 Resumo rápido

| Situação | Permitido |
|----------|----------|
| Dentro de componente React | ✅ |
| Dentro de hook customizado | ✅ |
| Fora de componentes | ❌ |
| Dentro de `if` | ❌ |
| Dentro de loops | ❌ |
| Dentro de funções internas | ❌ |

---

## ✅ Boas práticas

- Declare Hooks sempre no topo do componente
- Coloque a lógica condicional dentro do Hook, não ao redor
- Utilize o `eslint-plugin-react-hooks` para evitar erros automaticamente

---

## 📌 Regra mental simples

**Hooks sempre no topo do componente, sempre na mesma ordem**
