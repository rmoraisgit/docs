# Renderização dinâmica de componentes com `map`

Este projeto utiliza uma abordagem dinâmica para renderizar componentes React a partir de uma lista de dados, seguindo boas práticas recomendadas pelo React.

---

## 📌 Contexto

Anteriormente, os componentes `CoreConcepts` eram renderizados manualmente, acessando posições específicas do array `CORE_CONCEPTS`:

```jsx
<CoreConcepts {...CORE_CONCEPTS[1]} />
<CoreConcepts {...CORE_CONCEPTS[2]} />
<CoreConcepts {...CORE_CONCEPTS[3]} />
```

Apesar de funcional, essa abordagem não é escalável e dificulta a manutenção do código.

---

## ✅ Nova abordagem

A renderização foi refatorada para usar o método `map`, tornando o código mais flexível e limpo:

```jsx
{CORE_CONCEPTS.map((conceptItem) => (
  <CoreConcepts
    key={conceptItem.title}
    {...conceptItem}
  />
))}
```

---

## 🔍 O que esse código faz

* Percorre o array `CORE_CONCEPTS` usando o método `map`
* Para cada item do array, renderiza um componente `CoreConcepts`
* As propriedades do objeto são repassadas automaticamente para o componente através do **spread operator** (`...conceptItem`)

Com isso, a interface se adapta automaticamente à quantidade de itens existentes no array.

---

## 🚀 Vantagens dessa abordagem

### Escalabilidade

Novos itens podem ser adicionados ou removidos do array `CORE_CONCEPTS` sem necessidade de alterar o JSX.

### Código mais limpo

Evita repetição de código e deixa mais claro que os componentes são gerados a partir de uma fonte de dados.

### Manutenção facilitada

Reduz o risco de erros ao acessar índices inexistentes do array.

### Boas práticas do React

O uso de `map` para renderizar listas é o padrão recomendado pela documentação oficial do React.

---

## 🗝️ A propriedade `key`

```jsx
key={conceptItem.title}
```

A propriedade `key` é usada pelo React para identificar de forma única cada elemento de uma lista.

### Por que a `key` é importante?

* Ajuda o React a identificar quais itens foram adicionados, removidos ou alterados
* Melhora a performance do processo de renderização
* Evita comportamentos inesperados na interface

### Boas práticas

* A `key` deve ser **única**
* Deve ser **estável** entre renderizações
* Evitar usar o índice do array como `key`, sempre que possível

Neste projeto, `conceptItem.title` é utilizado como `key`, assumindo que os títulos sejam únicos.

---

## 🧠 Resumo

* A renderização passou de manual para dinâmica
* O método `map` cria automaticamente um componente para cada item do array
* O código ficou mais limpo, escalável e fácil de manter
* A propriedade `key` permite que o React gerencie listas de forma eficiente
