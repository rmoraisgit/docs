# 📄 Documentação — Componente TabButton e Comunicação com App

## 📌 Visão Geral

Este trecho do projeto demonstra conceitos fundamentais do React:

- Composição de componentes
- Passagem de funções como props
- Uso da prop `children`
- Comunicação entre componentes (pai → filho → pai)

O componente `TabButton` é responsável apenas pela **interface e disparo de eventos**, enquanto o componente `App` centraliza a **lógica de negócio**.

---

## 🧩 Componente `TabButton`

### Código

```jsx
export default function TabButton({ children, onSelected }) {
  return (
    <button onClick={onSelected}>
      {children}
    </button>
  );
}
````

### Responsabilidade

O componente `TabButton`:

* Renderiza um elemento `<button>`
* Exibe um conteúdo dinâmico via `children`
* Executa uma função quando o botão é clicado (`onSelected`)

O componente **não possui lógica própria**, não conhece estado e não sabe o que acontece após o clique.

---

## 🧠 Props do `TabButton`

### `children`

* Representa tudo que é passado entre a tag de abertura e fechamento do componente.

Exemplo:

```jsx
<TabButton>Components</TabButton>
```

No componente:

```js
children === "Components"
```

Renderização final:

```html
<button>Components</button>
```

---

### `onSelected`

* Função recebida do componente pai (`App`)
* Executada somente quando o botão é clicado

Uso no JSX:

```jsx
<button onClick={onSelected}>
```

O `TabButton` apenas **dispara o evento**, quem decide o que fazer é o componente pai.

---

## 🧩 Componente `App`

### Código relevante

```jsx
function App() {

  function handleClick(tabName) {
    console.log(`Tab: ${tabName}`);
  }

  return (
    <menu>
      <TabButton onSelected={() => handleClick('components')}>
        Components
      </TabButton>

      <TabButton onSelected={() => handleClick('props')}>
        Props
      </TabButton>

      <TabButton onSelected={() => handleClick('state')}>
        State
      </TabButton>
    </menu>
  );
}
```

---

## 🔁 Fluxo de execução (passo a passo)

### Exemplo analisado

```jsx
<TabButton onSelected={() => handleClick('components')}>
  Components
</TabButton>
```

---

### 1️⃣ Interpretação do JSX pelo React

O JSX é convertido internamente em algo equivalente a:

```js
TabButton({
  onSelected: () => handleClick('components'),
  children: 'Components'
});
```

* `children` recebe `"Components"`
* `onSelected` recebe uma função

---

### 2️⃣ Renderização do botão

Dentro do `TabButton`, o React renderiza:

```jsx
<button onClick={onSelected}>
  Components
</button>
```

Neste momento:

* Nenhuma função é executada
* O callback apenas é registrado

---

### 3️⃣ Clique do usuário

Quando o botão é clicado, o React executa:

```js
() => handleClick('components')
```

---

### 4️⃣ Execução da função no componente pai

A função `handleClick` é chamada com o argumento:

```js
handleClick('components');
```

Resultado no console:

```txt
Tab: components
```

---

## ⚠️ Por que usar uma arrow function?

### ❌ Forma incorreta

```jsx
<TabButton onSelected={handleClick('components')} />
```

Nesse caso, `handleClick` seria executada **durante a renderização**, o que não é desejado.

---

### ✅ Forma correta

```jsx
onSelected={() => handleClick('components')}
```

Essa abordagem:

* Cria uma função anônima
* Adia a execução até o clique
* Permite passar argumentos personalizados

---

## 🧠 Conceito-chave: Composição e controle pelo componente pai

Este padrão segue um dos pilares do React:

* O componente pai (`App`) controla o comportamento
* O componente filho (`TabButton`) controla apenas a interface
* A comunicação ocorre via props

Esse modelo favorece:

* Reutilização
* Clareza de responsabilidades
* Código mais previsível

---

## 🚀 Possíveis evoluções

Este padrão normalmente evolui para:

* Uso de `useState` para controlar a aba ativa
* Renderização condicional baseada na aba selecionada
* Estilização do botão ativo
* Criação de um componente de Tabs genérico

---

## ✅ Conclusão

O `TabButton` é um componente simples, reutilizável e desacoplado, que recebe comportamento via props e delega a lógica ao componente pai, seguindo as boas práticas do React moderno.

```

---
