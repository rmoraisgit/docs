````md
# Composição de Componentes em React com `children` e Slots

Este documento explica os principais conceitos de React aplicados nos componentes `Section`, `Tabs` e `TabButton`, com foco em **composição**, **children**, **repasse de props** e **componentes baseados em slots**.

---

## Exemplo de Uso

```jsx
return (
  <Section title="Examples" id="examples">
    <Tabs
      buttons={
        <>
          <TabButton
            isSelected={selectedTab === 'components'}
            onSelected={() => handleClick('components')}
          >
            Components
          </TabButton>

          <TabButton
            isSelected={selectedTab === 'props'}
            onSelected={() => handleClick('props')}
          >
            Props
          </TabButton>

          <TabButton
            isSelected={selectedTab === 'state'}
            onSelected={() => handleClick('state')}
          >
            State
          </TabButton>
        </>
      }
    >
      {tabContent}
    </Tabs>
  </Section>
);
````

Este exemplo demonstra como componentes React podem ser compostos de forma declarativa utilizando JSX e `children`.

---

## Componente `Section`

### Implementação

```jsx
export default function Section({ title, children, ...props }) {
  return (
    <section {...props}>
      <h2>{title}</h2>
      {children}
    </section>
  );
}
```

### Conceitos Aplicados

#### 1. `children`

* Tudo que é colocado entre `<Section>...</Section>` é recebido pela prop `children`.
* O componente não precisa saber qual conteúdo está sendo renderizado.
* Permite criar componentes de layout altamente reutilizáveis.

#### 2. Repasse de Props (`...props`)

* Props adicionais (`id`, `className`, `aria-*`, etc.) são repassadas diretamente para o elemento `<section>`.
* Faz o componente se comportar como um elemento HTML nativo.

#### 3. Componente de Layout

* `Section` é um componente focado apenas em estrutura.
* Não possui estado nem lógica de negócio.
* Responsável por organizar o layout e a semântica da página.

---

## Componente `Tabs`

### Implementação

```jsx
export default function Tabs({ children, buttons }) {
  return (
    <>
      <menu>
        {buttons}
      </menu>
      {children}
    </>
  );
}
```

### Conceitos Aplicados

#### 1. JSX como Valor

* JSX não é HTML, mas sim um objeto JavaScript.
* Pode ser passado como prop da mesma forma que qualquer outro valor.
* A prop `buttons` recebe um elemento React.

#### 2. Composição Baseada em Slots

* O React não possui slots nativos.
* É possível simular slots usando props.

Neste componente:

* `buttons` funciona como um **slot nomeado** para os botões
* `children` funciona como o **slot padrão** para o conteúdo

```jsx
<Tabs buttons={...}>
  {conteudo}
</Tabs>
```

#### 3. Separação de Responsabilidades

* O componente `Tabs` não:

  * cria botões
  * controla estado
  * define qual aba está ativa
* Ele apenas define **onde** os elementos serão renderizados.

Isso reduz o acoplamento e melhora a reutilização.

---

## Uso de Fragments

```jsx
<>
  <TabButton />
  <TabButton />
  <TabButton />
</>
```

* Fragments permitem agrupar múltiplos elementos
* Não adicionam nós extras ao DOM
* Mantêm a marcação limpa e semântica

---

## Benefícios Arquiteturais

* Separação clara entre layout e lógica
* Componentes altamente reutilizáveis
* APIs previsíveis e explícitas
* Código mais fácil de testar e manter
* Estado elevado para o componente pai (lifting state up)

---

## Modelo Mental

* **Section**: define uma área semântica da página
* **Tabs**: define slots para botões e conteúdo
* **TabButton**: representa uma ação específica
* **Estado**: fica no componente pai, não nos componentes de layout

> Princípio importante do React:
> **Componentes que controlam estado não devem ser responsáveis pelo layout.**

---

## Resumo dos Conceitos Utilizados

* JSX como valor
* `children`
* Repasse de props (`...props`)
* React Fragments
* Composição em vez de configuração
* Componentes baseados em slots
* Baixo acoplamento e alta reutilização

---

## Conclusão

Esse padrão representa um nível intermediário a avançado de design de componentes em React e escala muito bem para aplicações maiores, favorecendo clareza, composição e manutenção a longo prazo.

```

---

Se quiser, posso:
- adaptar essa doc para **TypeScript**
- criar uma versão **mais curta (cheat sheet)**
- ou padronizar o estilo das tuas documentações React 📚
```
