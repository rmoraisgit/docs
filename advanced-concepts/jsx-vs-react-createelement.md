### 🎯 You Don't Need JSX (But It's Convenient)

Esta documentação explica que **JSX não é obrigatório no React**. Internamente, o React utiliza `React.createElement`, e o JSX existe apenas como uma abstração sintática para facilitar a escrita do código.
 
### 🧩 Elemento Raiz e Fragments

Exploração das formas de retornar múltiplos elementos (`div`, `Fragment`, `<> </>`) e quando usar cada uma. [Veja detalhes](../basic-concepts/root-fragments.md)

---

## 🧩 Comparação das abordagens

Ambas as formas abaixo geram exatamente a mesma interface:

```html
<div id="content">
  <p>Hello World!</p>
</div>
```

---

## ✨ Usando JSX

```jsx
<div id="content">
  <p>Hello World!</p>
</div>
```

### Características

* Sintaxe parecida com HTML
* Mais legível e expressiva
* Requer etapa de build (Babel, Vite, Webpack)
* Código transformado automaticamente em `React.createElement`

---

## ⚙️ Usando `React.createElement` (sem JSX)

```js
React.createElement(
  'div',
  { id: 'content' },
  React.createElement(
    'p',
    null,
    'Hello World'
  )
);
```

### Características

* JavaScript puro
* Funciona sem transpilers
* Código mais verboso
* Total controle sobre a criação dos elementos

---

## 🔍 Parâmetros do `React.createElement`

| Parâmetro      | Descrição                                                     |
| -------------- | ------------------------------------------------------------- |
| Component Type | Define o tipo do elemento (`div`, `p` ou um componente React) |
| Props Object   | Define propriedades e atributos                               |
| Child Content  | Conteúdo interno (texto ou outros elementos)                  |

---

## ✅ Vantagens de **não** usar JSX

Embora menos comum, evitar JSX pode ser vantajoso em alguns cenários específicos:

### 1. Elimina a necessidade de build step

* Não exige Babel, Vite ou Webpack
* Pode ser executado diretamente no browser
* Ideal para projetos simples ou educacionais

---

### 2. Melhor entendimento do funcionamento interno do React

* Ajuda a compreender como o React cria elementos
* Facilita o aprendizado da API fundamental (`React.createElement`)
* Excelente para estudos e debugging

---

### 3. Útil em ambientes restritos

* Ambientes onde não é possível configurar build tools
* Integrações em sistemas legados
* Uso direto via `<script>` CDN

---

### 4. Menos dependências no projeto

* Reduz complexidade de setup
* Menor superfície de erros relacionados a transpilers
* Stack mais enxuta

---

### 5. Código 100% JavaScript

* Nenhuma sintaxe "especial"
* Ferramentas JS padrão funcionam sem configuração extra
* Sem confusão entre HTML e JavaScript para iniciantes mais técnicos

---

## ⚠️ Quando **não** usar JSX

Apesar das vantagens, evitar JSX **não é recomendado** para projetos grandes:

* Código fica difícil de ler e manter
* Estruturas complexas ficam muito verbosas
* Comunidade e ecossistema usam JSX como padrão

---