---
layout: post
published: true
show-avatar: true
comments: true
title: 'Spark : descomplicando o Java para web'
image: /img/sparklogo2.png
---
Quando comecei a programar, sempre tive um apreço imenso pelo Java (um pouco masoquista). Criar aplicações desktop *cross-platform* parecia simples com auxílio do Netbeans e isso era suficiente para eu estar convicto de que era um programador de verdade.

Eu era um militante Java, até o dia em que comecei o tortuoso percurso de especialização na especificação de JavaEE (diga-se o *Java para web*). Depois de criar algumas aplicações, comecei a perceber que os *workarounds* eram grandes para features simples, se o caso fosse UX era [PrimeFaces](http://primefaces.org) neles!

Como minhas justificativas para os *workarounds* da plataforma eram sempre a UX, comecei a estudar técnicas de *Client-side Rendering* utilizando frameworks como **React**(tão masoquista quanto), **Angular**, por último e principalmente **Vue.JS**.

Pela facilidade que era *casar* esses frameworks frontend com outros frameworks como Express.js (Node.js), Bottle (Python), e a incorporação em serviços IOT-like, fui cada vez mais me distanciando do JavaEE.

## Começando no Spark

Depois dessa introdução de cair lágrimas, vamos ao que interessa, primeiro destacar algumas características do [Spark](http://sparkjava.com/documentation):

* Java 8 - lambdas expressions compatível
* Kotlin compatível
* API similar ao express
* Uma das melhores documentações que já vi. Simples,clara,objetiva...
* Tem suporte da comunidade para vários plugins de templates (pra quem gosta de *Server-side rendering*)
* Pode ser usado de maneira standalone ou em conjunto com servidores de aplicação

Para mostrar o quão prático é começar com Spark, utilizando maven, adicionamos a dependência no nosso `pom.xml`:
```xml
<dependency>
    <groupId>com.sparkjava</groupId>
    <artifactId>spark-core</artifactId>
    <version>2.7.2</version>
</dependency>
```

Agora na nossa classe principal, de forma similiar ao express, declaramos nossa primeira rota, aguardando o método GET:
```java
import static spark.Spark.*;

public class HelloWorld {
    public static void main(String[] args) {
        get("/hello", (req, res) -> "Hello World");
    }
}
```

Executando nossa classe, teremos o servidor rodando e aguardando a requisição.

> Acesse `http://localhost:4567/hello`

Nosso *Olá mundo* está de pé.

Podemos mudar nossa porta, utilizando o método `port` do Spark:
```java
port(8080);
```
Com facilidade podemos acessar os *Routes Parameters* e *Query Parameters*
```java
get("/hello/:name", (request, response) -> {
    return "Hello: " + request.params(":name") + request.queryParams("sobrenome");
});
```
> Acesse `http://localhost:4567/hello/Joao?sobrenome=Silva`

A manipulação da sessão e de comportamento da resposta também é absurdamente prática, exatamente por isso vou pular essa parte. Quero essencialmente mostrar o sistema de templates e de transformação de resposta, para mostrar que o framework agrada à gregos e troianos.

Antes de avançar, a pasta `src/main/resources` vai ser o nosso ponto de partida para os arquivos estáticos (estilos, páginas e scripts) e também para o diretório de templates.

### Server Side Rendering

Para renderizar as páginas do lado do servidor, é conveniente utilizar uma engine de templates para montar nossas views.
Neste exemplo, optei pelo [handlebars](https://handlebarsjs.com).

Adicionamos o wrapper do handlebars para Spark no nosso `pom.xml`

```xml
<dependency>
    <groupId>com.sparkjava</groupId>
    <artifactId>spark-template-handlebars</artifactId>
    <version>2.7.1</version>
</dependency>

```

Adicionamos nosso template à pasta `src/main/resources/templates`, com o nome de `index.hbs`: 
{% raw %}
```hbs
<html>
<head>
    <title>Exemplo</title>
    <meta charset="UTF-8">
</head>
<body>
    <h2>
        Olá {{nome}}
    </h2>
    Seus emails:
    <ul>
        {{#each emails}}
            <li>
                {{this}}
            </li>
        {{/each}}
    </ul>
</body>
</html>

```
{% endraw %}
E por fim adicionar um pouco de código: 
```java
get("/", (request, response) -> {
                    HashMap<String, Object> params = new HashMap();
                    params.put("nome", "Joazinho");
                    params.put("emails",
                    	new String[]{
                            "Email do trabalho", 
                            "Email da faculdade", 
                            "Email do Pedrinho"});
                    return new ModelAndView(params, "index.hbs");
                }, new HandlebarsTemplateEngine());
```

Agora quando acessamos nosso localhost denovo, temos a seguinte mensagem:

```html

<!DOCTYPE html>
<html>
<head>
    <title>Exemplo</title>
    <meta charset="UTF-8">
</head>
<body>
    <h2>
        Olá Joazinho
    </h2>
    Seus emails:
    <ul>
            <li>
                Email do trabalho
            </li>
            <li>
                Email da faculdade
            </li>
            <li>
                Email do Pedrinho
            </li>
    </ul>
</body>
</html>
```
Pronto! finalizamos a renderização de nossa View. Simples e facil, não?!

### API-like
