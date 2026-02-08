# Funcionamento do `className` no componente `TabButton`

## Visão geral

O componente `TabButton` utiliza o atributo `className` de forma **condicional** para aplicar estilos diferentes dependendo do estado da aplicação.

Esse comportamento é essencial para indicar visualmente qual aba (tab) está selecionada no momento.

---

## Código do componente `TabButton`

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

---

## O papel do `className`

No React, o atributo `className` é usado no lugar de `class`, pois `class` é uma palavra reservada do JavaScript.

Neste componente, o `className` é definido da seguinte forma:

```jsx
className={isSelected ? 'active' : undefined}
```

### O que isso significa?

* Se `isSelected` for `true` → a classe CSS **`active`** será aplicada ao botão
* Se `isSelected` for `false` → **nenhuma classe** será aplicada

Isso permite alternar estilos dinamicamente sem manipular o DOM manualmente.

---

## De onde vem o `isSelected`?

O valor de `isSelected` é controlado pelo componente `App`, usando estado (`useState`).

### Estado no `App`

```jsx
const [selectedTab, setSelectedTab] = useState();
```

Esse estado guarda o nome da aba atualmente selecionada.

---

## Como o `isSelected` é calculado

Cada `TabButton` recebe uma comparação booleana:

```jsx
<TabButton
  isSelected={selectedTab === 'components'}
  onSelected={() => handleClick('components')}
>
  Components
</TabButton>
```

### O que acontece aqui?

* `selectedTab === 'components'` retorna:

  * `true` → se a aba ativa for `"components"`
  * `false` → caso contrário
* Esse valor é passado como `isSelected` para o `TabButton`

---

## Fluxo completo de funcionamento

1. O usuário clica em um `TabButton`
2. A função `handleClick` é chamada
3. O estado `selectedTab` é atualizado
4. O React re-renderiza o componente `App`
5. Cada `TabButton` recalcula o valor de `isSelected`
6. Apenas o botão ativo recebe `className="active"`

---

## Relação com o CSS

No arquivo `TabButton.css`, normalmente existe algo como:

```css
button.active {
  background-color: #5c5cff;
  color: white;
}
```

Ou seja:

* **Sem `active`** → botão normal
* **Com `active`** → botão destacado visualmente

---

## Por que usar `undefined` no `className`?

```jsx
className={isSelected ? 'active' : undefined}
```

Quando o valor é `undefined`, o React **não renderiza o atributo `class` no HTML**, deixando o botão limpo, sem classes extras.

Isso evita:

* Classes vazias (`class=""`)
* Condições mais verbosas

---

## Benefícios dessa abordagem

* Código simples e legível
* Estilo controlado apenas por estado
* Sem manipulação direta do DOM
* Totalmente alinhado ao modelo declarativo do React

---

## Resumo

* `className` é aplicado de forma condicional
* A condição depende do estado `selectedTab`
* Apenas o botão ativo recebe a classe `active`
* O visual reflete diretamente o estado da aplicação

Esse padrão é muito comum para:

* Tabs
* Menus
* Botões de navegação
* Filtros ativos
