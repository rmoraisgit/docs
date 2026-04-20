# TabButton – Abordagens de Design de Componente em React

Este documento explica duas abordagens diferentes para implementar o componente `TabButton` em React, destacando suas diferenças conceituais, vantagens, desvantagens e quando utilizar cada uma.

---

## Contexto

O componente `TabButton` representa um botão usado para selecionar abas (tabs).  
Apesar de ambas as implementações produzirem o mesmo comportamento visual e funcional, elas seguem **filosofias diferentes de design de componentes**.

---

## Abordagem 1 — Componente genérico e flexível

### Implementação

```jsx
import './TabButton.css';

export default function TabButton({ children, isSelected, ...props }) {
  return (
    <button
      className={isSelected ? 'active' : undefined}
      {...props}
    >
      {children}
    </button>
  );
}
```

### Uso

```jsx
<TabButton
  isSelected={selectedTab === 'components'}
  onClick={() => handleClick('components')}
>
  Components
</TabButton>
```

### Características

* Usa o **rest operator (`...props`)** para capturar todas as props adicionais.
* Repassa essas props diretamente para o elemento `<button>`.
* Não define explicitamente eventos como `onClick`.

### Consequências

* O componente aceita qualquer atributo válido de um botão HTML:

  * `onClick`
  * `disabled`
  * `type`
  * `aria-*`
  * `data-*`

### Vantagens

* ✅ Alta reutilização
* ✅ Mais flexível
* ✅ Próximo da API nativa do HTML
* ✅ Ideal para componentes base ou de Design System

### Desvantagens

* ⚠️ Menos explícito
* ⚠️ A API do componente não fica clara só olhando sua assinatura
* ⚠️ Maior chance de uso incorreto se não houver documentação

---

## Abordagem 2 — Componente explícito e semântico

### Implementação

```jsx
import './TabButton.css';

export default function TabButton({ children, onSelected, isSelected }) {
  return (
    <button
      className={isSelected ? 'active' : undefined}
      onClick={onSelected}
    >
      {children}
    </button>
  );
}
```

### Uso

```jsx
<TabButton
  isSelected={selectedTab === 'components'}
  onSelected={() => handleClick('components')}
>
  Components
</TabButton>
```

### Características

* Define explicitamente a prop `onSelected`.
* O consumidor do componente **não lida diretamente com `onClick`**.
* O nome da prop comunica o propósito do componente.

### Consequências

* A API do componente é **controlada e previsível**.
* O componente deixa claro que representa uma **ação de seleção**, não um botão genérico.

### Vantagens

* ✅ Melhor semântica
* ✅ Mais fácil de entender ao ler o JSX
* ✅ Menor risco de uso indevido
* ✅ Ideal para componentes de domínio específico

### Desvantagens

* ⚠️ Menos flexível
* ⚠️ Para aceitar novas funcionalidades (ex: `disabled`), o componente precisa ser alterado
* ⚠️ Menos reutilizável fora do contexto de tabs

---

## Comparação direta

| Aspecto                     | Abordagem 1 | Abordagem 2 |
| --------------------------- | ----------- | ----------- |
| Flexibilidade               | Alta        | Baixa       |
| Clareza semântica           | Média       | Alta        |
| Reutilização                | Excelente   | Limitada    |
| Controle da API             | Baixo       | Alto        |
| Ideal para Design System    | ✅           | ❌           |
| Ideal para regra de negócio | ❌           | ✅           |

---

## Quando usar cada abordagem

### Use a Abordagem 1 quando:

* O componente for genérico
* A intenção for reutilização em múltiplos contextos
* O componente fizer parte de um UI Kit ou Design System

Exemplos:

* `Button`
* `IconButton`
* `BaseButton`

---

### Use a Abordagem 2 quando:

* O componente tiver uma responsabilidade específica
* A semântica for mais importante que a flexibilidade
* O comportamento fizer parte da regra de negócio

Exemplos:

* `TabButton`
* `PaginationButton`
* `ModalCloseButton`

---

## Abordagem híbrida (recomendada em muitos casos)

É possível combinar flexibilidade com identidade semântica:

```jsx
export default function TabButton({ children, isSelected, ...props }) {
  return (
    <button
      className={`tab-button ${isSelected ? 'active' : ''}`}
      {...props}
    >
      {children}
    </button>
  );
}
```

### Benefícios da abordagem híbrida

* Mantém a flexibilidade do `...props`
* Preserva a identidade visual e funcional do componente
* Reduz acoplamento sem perder reutilização

---

## Conclusão

A escolha entre as abordagens não é sobre certo ou errado, mas sobre **intenção**:

* **Componentes genéricos → flexibilidade**
* **Componentes de domínio → semântica e clareza**

Projetar bem a API de um componente React é tão importante quanto sua implementação visual.
