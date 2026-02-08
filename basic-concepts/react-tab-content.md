# Documentação – Funcionamento do Tab Content no React

## Visão geral

Este trecho do código é responsável por **exibir dinamicamente o conteúdo da aba selecionada** (tab) com base no estado da aplicação. Ele utiliza um objeto de dados (`EXAMPLES`) como fonte de informação e o estado `selectedTab` como chave para decidir **qual conteúdo renderizar**.

```jsx
<div id="tab-content">
  <h3>{EXAMPLES[selectedTab]?.title}</h3>
  <p>{EXAMPLES[selectedTab]?.description}</p>
  <pre>
    <code>
      {EXAMPLES[selectedTab]?.code}
    </code>
  </pre>
</div>
```

---

## Estrutura de dados envolvida (`EXAMPLES`)

O objeto `EXAMPLES`, definido no arquivo `data.js`, funciona como um **dicionário de conteúdo**.

Cada chave representa uma aba (`components`, `jsx`, `props`, `state`) e aponta para um objeto com três propriedades:

* `title`: título exibido na interface
* `description`: texto explicativo
* `code`: exemplo de código a ser mostrado

### Exemplo completo da chave `components`

```js
components: {
  title: 'Components',
  description:
    'Components are the building blocks of React applications. A component is a self-contained module (HTML + optional CSS + JS) that renders some output.',
  code: `
function Welcome() {
  return <h1>Hello, World!</h1>;
}`,
}
```

Esse objeto é consumido diretamente pelo componente através da chave dinâmica `selectedTab`.

---

## Estrutura do objeto `EXAMPLES`

```js
EXAMPLES = {
components: {
title: 'Components',
description: '...',
code: '...'
}
}
```

---

## Papel do estado `selectedTab`

O estado `selectedTab` guarda **qual aba está atualmente selecionada**. Ele recebe valores como:

- `'components'`
- `'props'`
- `'state'`

Esse valor é atualizado quando o usuário clica em um botão (`TabButton`), através da função `handleClick`.

```jsx
<TabButton onSelected={() => handleClick('components')}>Components</TabButton>
```

Quando o estado muda, o React **re-renderiza o componente**, atualizando automaticamente o conteúdo exibido.

---

## Como o conteúdo é renderizado dinamicamente

### 1. Acesso dinâmico ao objeto

```jsx
EXAMPLES[selectedTab]
```

Aqui, o valor de `selectedTab` é usado como **chave** para acessar o objeto correto dentro de `EXAMPLES`.

Exemplo prático:

```js
selectedTab = 'props'

EXAMPLES[selectedTab] === EXAMPLES.props
```

---

### 2. Optional Chaining (`?.`)

```jsx
EXAMPLES[selectedTab]?.title
```

O operador `?.` evita erros quando `selectedTab` ainda não foi definido.

Sem ele, o código quebraria se `selectedTab` fosse `null` ou `undefined`.

Com `?.`, o React simplesmente renderiza **nada**, mantendo a aplicação estável.

---

## Renderização de cada parte

### Título

```jsx
<h3>{EXAMPLES[selectedTab]?.title}</h3>
```

Exibe o título correspondente à aba selecionada.

---

### Descrição

```jsx
<p>{EXAMPLES[selectedTab]?.description}</p>
```

Mostra o texto explicativo relacionado ao conceito atual.

---

### Bloco de código

```jsx
<pre>
  <code>
    {EXAMPLES[selectedTab]?.code}
  </code>
</pre>
```

Esse trecho:

* Preserva quebras de linha e espaçamento (`<pre>`)
* Exibe código de forma legível (`<code>`)
* Renderiza o exemplo armazenado como **string** no objeto `EXAMPLES`

Esse padrão é muito comum em documentações e páginas educacionais.

---

## Fluxo completo de funcionamento

1. O usuário clica em um `TabButton`
2. A função `handleClick` atualiza o estado `selectedTab`
3. O React re-renderiza o componente
4. O valor de `selectedTab` muda
5. O conteúdo dentro de `#tab-content` é atualizado automaticamente

---

## Benefícios dessa abordagem

* Separação clara entre **dados** e **interface**
* Código escalável (adicionar nova aba exige apenas um novo item em `EXAMPLES`)
* Evita condicionais complexos (`if` / `switch`)
* Código mais declarativo e legível

---

## Conclusão

O `div#tab-content` atua como um **renderizador dinâmico de conteúdo**, controlado por estado e alimentado por um objeto de configuração. Esse padrão é simples, poderoso e muito utilizado em aplicações React que trabalham com abas, painéis ou seções dinâmicas.
