---
layout: post
published: true
show-avatar: true
comments: true
title: Semântica na Web
date: '2018-08-13'
tags:
  - html5
  - html
  - web semantica
subtitle: 'Uma forma mais semântica de codar, utilizando HTML5'
---
A *semântica* é o estudo do entendimento das palavras em uma linguagem qualquer.
Na web, a semântica, auxilia tanto o desenvolvedor quanto o próprio browser a entender o contexto dos elementos, o que esses elementos **significam**.

Elementos como `div` e `span`, não nos dizem claramente o que temos em seu conteúdo. Por outro lado, elementos como `table`, `form`, `article`, `ul` - deixam mais claros o seu conteúdo.

Até o *HTML4*, classes e id's eram usados para indicar e estilizar elementos como cabeçalhos, rodapés e etc.
Isso dificultava bastante as engines de pesquisa para separar o que era conteúdo do que não era. 

O *HTML5* introduziu uma série nova de elementos que tem por objetividade indicar melhor o seu conteúdo e auxiliar no compartilhamento e reuso entre aplicações e etc.

Em muitos códigos-fontes anteriores *(ou não rsrs)* era possível perceber algumas partes assim: 
`<div id="nav">...</div>`,`<div id="header">...</div>`,`<div id="footer">...</div>`, que indicam o bloco da barra de navegação, bloco do cabeçalho, bloco do rodapé e etc.

Com *HTML5* os mesmos elementos descritos acima, podem ser escritos dessa maneira: 
`<nav>...</nav>`,`<header>...</header>`, `<footer>...</footer>`.

Já começou a ficar mais claro, não? Mas esses são só alguns dos novos elementos introduzidos.

Entre eles, também:

- `<article>`
- `<aside>`
- `<details>`
- `<figcaption>`
- `<figure>`
- `<footer>`
- `<header>`
- `<main>`
- `<mark>`
- `<nav>`
- `<section>`
- `<summary>`
- `<time>`

## Alguns exemplos e suas utilizações

### O elemento `<section>`

O elemento `<section>` define uma seção no documento, de acordo com a sua especificação pela W3C ele é: *"Uma seção com agrupamento temático, geralmente entitulado."*

Exemplo:
```html
<section>
  <h1>WWF</h1>
  <p>The World Wide Fund for Nature (WWF) is....</p>
</section>
```

### O elemento `<article>`

O elemento `<article>` especifica um conteudo independente e propriamente contido.
Um artigo tem que fazer sentido sozinho e ser possível de entender independente do conteúdo do resto do site.

Exemplo:
```html
<article>
  <h1>What Does WWF Do?</h1>
  <p>WWF's mission is to stop the degradation of our planet's natural environment,
  and build a future in which humans live in harmony with nature.</p>
</article>
```

Nesse momento pode começar a surgir uma dúvida: tem algum problema de ter `<section>` dentro de um `<article>`, e a resposta é **não**.

{: .alert.alert-info}
Naturalmente, páginas irão conter `<article>` dentro de `<section>` e vice-versa, como por exemplo, em um *jornal*, podemos ter: Um `<article>` de esporte, dentro da `<section>` de esporte, e cada artigo ter uma `<section>` com informações técnicas.

### Os elementos `<header>` e `<footer>`

Esses elementos especificam *cabeçalho* e *rodapé* do documento ou seção.

```html
<body>
  <header>
    <h1>John Doe</h1>
    <p>Um novo tipo de café</p>
  </header>
  
  ...
  
  <footer>
     <p>Desenvolvido por John Doe</p>
     <p>Me envie um email: <a href="mailto:johndoe@example.com">
     johndoe@example.com</a>.</p>
  </footer>
</body>
```

### O elemento `<nav>`

O elemento `<nav>` indica um conjunto de link's de navegação.

Exemplo:
```html
<nav>
  <a href="/html/">HTML</a> |
  <a href="/css/">CSS</a> |
  <a href="/js/">JavaScript</a> |
  <a href="/jquery/">jQuery</a>
</nav>
```

### O elemento `<aside>`

O elemento `<aside>` define um conteúdo que é colocado `paralelamente` ao conteúdo principal, como por exemplo, uma barra de navegação lateral.

E seu conteúdo deve ser relacionado ao conteúdo principal.

```html
<aside>
  <p> Algum conteudo relacionado à um <article> </p>
</aside>
```
### Os elementos `<figure>` e `<figcaption>`

O propósito do `<figcaption>` é adicionar uma legenda, uma explicação visual sobre a imagem.

No *HTML5*, uma imagem e sua legenda (`<figcaption>`) são colocadas dentro de um elemento `<figure>`.

```html
<figure>
  <img src="pic_trulli.jpg" alt="Trulli">
  <figcaption>Fig1. - Trulli, Puglia, Italy.</figcaption>
</figure>
```



Os elementos exemplificados aqui, são apenas alguns dos elementos semânticos inseridos no *HTML5*, para mais informações, vocês podem acessar a [W3Schools - HTML5 Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp).

Esse post é uma releitura da postagem original da [W3Schools](https://www.w3schools.com).

Abraços e hasta-luego.
