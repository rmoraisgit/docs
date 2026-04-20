# 📄 Documentação — Controle de Tabs com useState no React

## 📌 Visão Geral

Esta implementação introduz o uso do **Hook `useState`** para controlar qual aba está selecionada na aplicação.

O objetivo é:
- Armazenar o estado da aba ativa
- Atualizar esse estado a partir de interações do usuário
- Refletir automaticamente a mudança na interface

Esse padrão representa o **jeito idiomático do React** de lidar com interações e UI dinâmica.

---

## 🧠 O que é `useState`

`useState` é um Hook do React que permite:

- Criar estado em componentes funcionais
- Fazer o React re-renderizar o componente quando o estado muda
- Manter valores entre renderizações

Importação:

```js
import { useState } from 'react';
```

---

## 🧩 Criação do estado

```js
const [selectedTab, setSelectedTab] = useState('Please, select a tab');
```

Essa linha cria três coisas importantes:

| Elemento                 | Descrição                            |
| ------------------------ | ------------------------------------ |
| `selectedTab`            | Valor atual do estado                |
| `setSelectedTab`         | Função usada para atualizar o estado |
| `'Please, select a tab'` | Valor inicial do estado              |

Na **primeira renderização**, `selectedTab` possui esse valor inicial.

---

## ⚠️ Regra fundamental do estado

> ❗ O estado **nunca deve ser alterado diretamente**

❌ Errado:

```js
selectedTab = 'components';
```

✅ Correto:

```js
setSelectedTab('components');
```

Somente a função `setSelectedTab` informa ao React que o estado mudou.

---

## 🧩 Função `handleClick`

```js
function handleClick(tabName) {
  setSelectedTab(tabName);
  console.log(`Tab: ${tabName}`);
}
```

Responsabilidades da função:

1. Atualizar o estado da aba selecionada
2. Registrar a ação no console (debug/log)

A chamada de `setSelectedTab` dispara um **novo ciclo de renderização** do componente.

---

## 🧩 Componente `TabButton`

```jsx
export default function TabButton({ children, onSelected }) {
  return (
    <button onClick={onSelected}>
      {children}
    </button>
  );
}
```

Responsabilidades do `TabButton`:

* Renderizar um botão
* Exibir conteúdo via `children`
* Executar a função recebida via `onSelected`

O componente:

* Não possui estado
* Não conhece a aba ativa
* Apenas dispara eventos

---

## 🔁 Fluxo completo de execução

### Exemplo analisado

```jsx
<TabButton onSelected={() => handleClick('components')}>
  Components
</TabButton>
```

---

### 1️⃣ Renderização inicial

* `useState` define o valor inicial
* `selectedTab === 'Please, select a tab'`

Renderização no JSX:

```jsx
{selectedTab}
```

Resultado na tela:

```txt
Please, select a tab
```

---

### 2️⃣ Clique do usuário

O usuário clica no botão **Components**.

O React executa:

```js
() => handleClick('components')
```

---

### 3️⃣ Atualização do estado

Dentro do `handleClick`:

```js
setSelectedTab('components');
```

O React:

* Atualiza o estado interno
* Agenda a re-renderização do componente `App`

---

### 4️⃣ Re-renderização do componente

Durante a nova renderização:

```js
selectedTab === 'components'
```

O JSX agora renderiza:

```txt
components
```

Sem manipulação manual do DOM.

---

## 🧠 O que significa “re-renderizar”?

* O React executa novamente a função `App`
* Recalcula o JSX com o novo estado
* Atualiza apenas o que mudou no DOM real

Importante:

* O estado é preservado entre renderizações
* Apenas o valor atualizado é utilizado

---

## 🔄 Fluxo de dados no React

Este exemplo segue o fluxo padrão do React:

```
Estado (App)
   ↓
Props (TabButton)
   ↓
Evento (onClick)
   ↓
Atualização de estado
   ↓
Nova renderização
```

Esse fluxo é **unidirecional**, previsível e fácil de debugar.

---

## 🧠 Conceitos aplicados

* State como *single source of truth*
* UI como função do estado
* Componentes controlados pelo pai
* Separação de responsabilidades
* Composição de componentes

---

## ✅ Conclusão

Com o uso do `useState`, a aplicação passa a:

* Reagir a interações do usuário
* Manter contexto entre renderizações
* Centralizar o controle da UI no estado

Esse exemplo representa um dos **padrões mais importantes do React moderno**.
