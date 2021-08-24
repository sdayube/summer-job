# CSS: Flexbox


## O que vamos aprender?

Olá, XP Inker!

No dia de hoje você irá aprender a utilizar uma das ferramentas mais poderosas para a criação de layouts em CSS: o **flexbox**!

O [*CSS Flexible Box Layout Module Level 1*](https://www.w3.org/TR/css-flexbox-1/), ou ***flexbox*** para os íntimos, é um módulo que foi implementado na edição 3 do CSS e cuja finalidade é tornar mais fácil e eficiente o desenvolvimento de interfaces web fluidas e responsivas.


## Porque isso é importante?

Antes da implementação da versão 3 do CSS, as pessoas desenvolvedoras precisavam se virar nos 30 para deixar os seus sites com a aparência desejada usando propriedades que não foram exatamente pensadas para esse fim: a propriedade  `display` com os valores `float`, `inline-block`, `block`, etc. e a propriedade `position` com os valores `fixed`, `absolute`, `relative`, etc. 

Por não terem sido inicialmente concebidas para tanto, a criação de um layout bem feito apenas com essas propriedades CSS acaba não sendo a coisa mais fácil do mundo. Existem tarefas que se tornam um pesadelo se apenas esses recursos estiverem disponíveis, como pro exemplo:
-   Alinhar *verticalmente* um bloco de conteúdo *no centro* do bloco que o contém;
-   Fazer todos os elementos descendentes de um outro elemento ocuparem a mesma quantidade de espaço considerando a largura e altura disponíveis;
-   Fazer todas as colunas de um conteúdo possuírem a mesma altura mesmo tendo conteúdos de tamanhos diferentes.
-   A criação de layouts responsivos.

Com a chegada do CSS3, foi introduzido um módulo que acabou de vez com esse problema: o *CSS Flexible Boxes*, amplamente conhecido como **flexbox**. Com ele, tornou-se possível desenvolver layouts com muito mais facilidade e precisão: ele organiza os elementos de uma forma previsível, relativamente fácil de se controlar e que pode ser facilmente adaptada para diferentes browsers e tamanhos de tela.

Vamos ver com mais detalhes todas as possibilidades maravilhosas trazidas pelo *flexbox*?
 
 
## Conteúdos

### Aplicando o *flexbox* a um elemento:

Para conseguir entender de verdade como funciona o *flexbox*,  primeiro vamos relembrar o comportamento padrão de uma página HTML, considerando o seguinte código:
```html
<body>
  <header>
    <h1>Título da página</h1>
  </header>
  <section>
    <article>
      <h2>Primeiro artigo</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing
      elit. Morbi nunc leo, feugiat quis velit ut, porta
      pharetra arcu.</p>
    </article>
    <article>
      <h2>Segundo Artigo</h2>
	    <p>Lorem ipsum dolor sit amet, consectetur adipiscing
	    elit. Cras vulputate urna in massa tincidunt, sed
        efficitur magna faucibus.</p>
    </article>
    <article>
	  <h2>Terceiro Artigo</h2>
	  <p>Proin at sodales ante. Suspendisse venenatis massa id
	  justo placerat vestibulum. Maecenas tincidunt orci id mi
	  rhoncus, eu mattis ligula viverra.</p>
    </article>
  </section>
</body>
```

Ao rodar esse código no browser utilizando o layout padrão do HTML, a `section` ficará abaixo do `header`, todos os `article` ficarão abaixo um do outro e os `p` ficarão abaixo dos `h2`. Isso acontece por conta do display padrão desses elementos ser o `display: block;`.

Para exemplificar, vejamos como fica uma página com esse layout padrão após algumas pequenas estilizações para que fique mais apresentável:

![Layout sem flexbox](https://i.ibb.co/fDqSwh4/no-flex-example.png)

Mas e se quisermos colocar os artigos um do lado do outro, como podemos fazer?
Temos duas opções:

- Opção 1 - Penar por ~~horas~~ algum tempo com o `display: float;` e eventualmente conseguir montar um layout ~~mais ou menos~~ funcional na base de muita tentativa e erro;

- Opção 2 - **Usar o flexbox**!

Para começar a usufruir das maravilhas do *CSS Flexible Boxes*, basta aplicar na `section`, que é o elemento pai dos artigos no HTML, a seguinte propriedade CSS:

```CSS
section {
  display: flex;
}
```
Sim, é só isso que você precisa fazer --- pelo menos em um primeiro momento! Para começar a utilizar o *flexbox*, basta aplicar o valor `flex` à propriedade `display` do elemento que servirá como o que chamamos de ***flex container*** e que é o elemento anterior aos que você quer organizar.

Claro que isso não é tudo, mas já faz uma grande diferença! Vamos ver o nosso layout como ficou:

![Layout com flexbox](https://i.ibb.co/RzTqCCr/flex-example.png)

Muito mais fácil, não é mesmo? Mas isso é só uma fração do poder do *flexbox*!

Pra extrair o melhor da ferramenta, você precisará conhecer o conceito de **eixos e direções**, que norteia o funcionamento do *flexbox*. Uma vez sabendo esse conceito, você poderá poder utilizar algumas propriedades bem interessantes para manipular o layout das suas páginas web de forma ainda mais flexível e estender as possibilidades *ao infinito e além* :rocket:!

### Eixos e direções no flexbox:

O *flex container* é o elemento que servirá como pai dos *flex items*, ou seja, é o elemento cujo conteúdo será posicionado na tela de acordo com as especificações do *flexbox*! Além disso, a partir da sua definição com o `display: flex;`, você poderá facilmente alterar a a direção, alinhamento e demais comportamentos de todos os seus *flex items* de forma flexível. Mas como isso funciona?

Todo *flex container*, uma vez definido, será transformado em um plano com duas dimensões: horizontal e vertical, que servirão para alinhar os itens contidos nele. Essas dimensões são conhecidas como *flex axes*, ou eixos flex:

![Flex Axes](https://i.ibb.co/rMhTn67/flex-axes.png)

Como se pode ver, os eixos flex são os seguintes:
 - **Main axis (eixo principal)** : É o eixo no qual os itens do flex-container serão distribuídos, por padrão. Você pode ver na imagem acima que os itens 1 e 2 estão dispostos lado a lado porque seu posicionamento segue o main axis do container.

 - **Cross axis (eixo cruzado)** :  É o eixo perpendicular ao main axis. Por padrão, o cross axis será utilizado para expandir a altura dos itens contidos para que todos possuam a mesma altura independentemente do conteúdo. Também serve para alinhar os itens no eixo cruzado.

Também podemos ver a partir dessa imagem que ambos os eixos possuem uma direção padrão: da esquerda para a direita no main axis e de cima pra baixo no cross axis. À junção do eixo principal com a direção padrão damos o nome de ***flex direction***. Não esqueça desse termo, pois será muito importante nas próximas etapas!

Vamos praticar um pouco?
Copie e cole o código html abaixo no seu VS Code:

```html
<head>
  <style>
    .flex-container {
      background-color: #e4e8ec;
      box-sizing: border-box;
      padding: 10px;
      /* Utilize o espaço abaixo para transformar a div em um flex-container */
      
    }

    .flex-item {
      padding: 10px;
      margin: 10px;
      background: white;
      border: 1px  solid  rgba(0,0,0,.125);
      border-radius: .25rem;
      /* Experimente mudar a propriedade width para ver o que acontece com os itens! */
      width: 10%;
      text-align: center;
    }

    .f1 {
      font-size: 60px;
    }

    .f2 {
      font-size: 45px;
    }

    .f1 {
      font-size: 30px
    }
  </style>
</head>
<body>
  <div class="flex-container">
    <div class="flex-item f1"></div>
    <div class="flex-item f2"></div>
    <div class="flex-item f3"></div>
  </div>
</body>
```
Agora utilize o espaço indicado no primeiro comentário para transformar o seu container em um flex-container!

Feito isso, observe algumas coisas:

 1. Qual o comportamento dos *flex-items* quando você aplica ao *container* a propriedade que o transforma em um *flex-container*?
 2. Qual a *direção* e a *ordem* em que esses itens são dispostos automaticamente?
 3. Qual a *altura* dos flex-items antes e depois de você criar o flex-container?
 4. Quais os eixos responsáveis por cada um desses comportamentos?

Como você pôde ver, a forma como os eixos estão dispostos inicialmente é bem simples de se compreender. Mas o flexbox não se limita a seguir sempre esse modelo apresentado: ele é apenas um padrão. Agora vamos aprender como modificar esse comportamento padrão!

> **NOTA:** Não se esqueça de modificar a largura dos flex-items e ver como eles se comportam de maneira flexível, principalmente quando a soma das larguras ultrapassar a largura do container!

### Manipulando os eixos flex:
 
Agora que você já sabe o que são o *main axis* e o *cross axis* do flex-container, vamos ver como podemos modificar essa estrutura pra dar ainda mais flexibilidade à forma como queremos dispor os nossos layouts.

Antes de prosseguir, como já explicamos, o conjunto do *main axis* com a sua *direção* é o que chamamos de *flex direction*. Só que a melhor parte é que nós podemos modificar a flex direction usando o CSS! Para isso, basta aplicar a propriedade `flex-direction` no flex-container:

```css
.flex-container {
	display: flex;
	flex-direction: row;
}
```

A propriedade flex-direction tem quatro valores que servem para alterar o eixo principal e sua a direção. **Clique em cada um para saber mais**! 

<details>
  <summary><code>flex-direction: row;</code></summary>
  <p>Alinha o flex-container na horizontal, da esquerda para a direita:</p>
  <img src="https://i.ibb.co/rMhTn67/flex-axes.png" alt="representação do flex-direction row">
  <p>O <code>flex-direction: row;</code> é o atributo padrão dos flex-containers.</p>
  <br>
</details>

<details>
  <summary><code>flex-direction: row-reverse;</code></summary>
  <p>Alinha o flex-container na horizontal, da direita para a esquerda:</p>
  <img src="https://i.ibb.co/WxFvjL3/flex-row-reverse.png" alt="representação do flex-direction row-reverse">
  <p>Neste caso, apenas invertemos a direção do eixo principal, que permanece na horizontal.</p>
  <br>
</details>

<details>
  <summary><code>flex-direction: column;</code></summary>
  <p>Alinha o flex-container na vertical, de cima para baixo:</p>
  <img src="https://i.ibb.co/92jv8wg/flex-column.png" alt="representação do flex-direction column">
  <p>Ao usar o valor <code>column</code> nós trocamos o <em>main axis</em> e o <em>cross axis</em> de lugar. Isso possibilita posicionarmos elementos de forma parecida com o <code>display: block;</code>, mas mantendo toda a flexibilidade do <em>flexbox</em>!</p>
  <br>
</details>

<details>
  <summary><code>flex-direction: column-reverse;</code></summary>
  <p>Alinha o flex-container na vertical, de baixo para cima:</p>
  <img src="https://i.ibb.co/ZXNZr1d/flex-column-reverse.png" alt="representação do flex-direction column-reverse">
  <p>Ao usar o valor <code>column</code> nós trocamos o <em>main axis</em> e o <em>cross axis</em> de lugar. Isso possibilita posicionarmos elementos de forma parecida com o <code>display: block;</code>, mas mantendo toda a flexibilidade do <em>flexbox</em>!</p>
  <br>
</details>
<br>

### Vamos praticar?
Agora que você já sabe como modificar a flex-direction para exibir o conteúdo em qualquer direção, vamos fazer isso na prática! Primeiro, copie o código abaixo e cole no seu VS Code:

```html
<head>
  <style>
    .flex-container {
      background-color: #e4e8ec;
      box-sizing: border-box;
      padding: 10px;
      display: flex;
      /* Utilize o espaço abaixo para manipular a direção do conteúdo */
      
    }

    .flex-item {
      padding: 10px;
      margin: 10px;
      background: white;
      border: 1px  solid  rgba(0,0,0,.125);
      border-radius: .25rem;
      min-width: 10%;
      text-align: center;
      font-size: 60px;
    }
  </style>
</head>
<body>
  <div class="flex-container">
    <div class="flex-item"></div>
    <div class="flex-item"></div>
    <div class="flex-item"></div>
  </div>
</body>
```

Agora faça o seguinte:

 1. Faça com que o conteúdo flua da direita para a esquerda;
 2. Faça com que o conteúdo flua de cima para baixo;
 3. Faça com que o conteúdo flua de baixo para cima;
 4. Faça com que o conteúdo flua da esquerda para a direita (comportamento padrão) .

Agora que você já sabe como manipular os eixos do flexbox para que o conteúdo flua em qualquer direção, vamos entender melhor como alinhar os flex-items de acordo com o eixo em que estão colocados! 


### Justificando o conteúdo:

Por vezes, os flex-items não são capazes de preencher, com a sua própria largura, toda a dimensão do flex-container. Isso ocorre principalmente quando o eixo principal está na horizontal, pois nesses casos a largura do flex container, se não for modificada, costuma acompanhar o tamanho da tela.

Você pôde ver isso no bloco de código que utilizamos no exercício anterior:

![Comportamento padrão - justify-content: flex-start;](https://i.ibb.co/PWB9LmS/Flex-justify-example1.png)

Todavia, o flexbox nos permite alinhar o conteúdo dentro do eixo principal sem necessáriamente alterar a direção do eixo. Pra isso, podemos usar a propriedade `justify-content`, que alinha o conteúdo do flex-container dentro do eixo usando vários atributos.

O atributo mais utilizado é o `justify-content: center;`, que alinha o conteúdo dos flex-items no centro do eixo principal, independente de qual direção ele siga. Outras opções de atributos para a propriedade `justify-content` são as seguintes:

-   `flex-start`: alinha os flex-items no início do flex-container, considerando o flex-direction do eixo principal.  Trata-se da forma de padrão de se justificar o conteúdo de um flex-container, ou seja, esse é o comportamento padrão dos itens se a propriedade `justify-content` não for utilizada.

-   `flex-end`: alinha os flex-items no final do flex-container. É diferente de usar o flex-direction para inverter a direção porque a ordem em que os itens são postos permanece a mesma do eixo, eles só são "empurrados" para o final do container.
 
-   `space-between`: alinha os itens no centro do eixo principal e põe automaticamente um espaço entre os itens. Com esse espaço automático, o primeiro dos itens sempre ficará grudado no início do eixo e o último sempre ficará grudado ao final. A distância entre os itens vai depender da quantidade de itens colocados no eixo.

-   `space-around`: funciona de forma parecida com o `space-between`, só que metade do espaço é colocada entre o primeiro e último itens e o começo e o final do eixo.

-   `space-evenly`: é muito parecido com a última propriedade, mas ao invés de meio espaço ela coloca um espaço inteiro entre o primeiro e último itens e o começo e o final do eixo.

Certamente as definições ainda estão um pouco confusas, mas agora vamos entender como todos esses atributos funcionam da melhor maneira: na prática! Primeiro, copie o código abaixo e cole em seu VS Code:

```html
<head>
  <style>
    .flex-container {
      background-color: #e4e8ec;
      box-sizing: border-box;
      padding: 10px;
      display: flex;
      margin: 0  0  20px;
    }

    .flex-item {
      padding: 10px;
      margin: 10px;
      background: white;
      border: 1px  solid  rgba(0,0,0,.125);
      border-radius: .25rem;
      min-width: 10%;
      text-align: center;
      font-size: 60px;
    }

    .flex-start {
      justify-content: flex-start;
    }

    .center {
      
    }

    .flex-end {
      
    }

    .space-between {
      
    }

    .space-around {
      
    }

    .space-evenly {
      
    }

  </style>
</head>
<body>
  <div class="flex-container flex-start">
    <div class="flex-item"></div>
    <div class="flex-item"></div>
    <div class="flex-item"></div>
  </div>

  <div class="flex-container center">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
    <div class="flex-item">3</div>
  </div>

  <div class="flex-container flex-end">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
    <div class="flex-item">3</div>
  </div>

  <div class="flex-container space-between">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
    <div class="flex-item">3</div>
  </div>

  <div class="flex-container space-around">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
    <div class="flex-item">3</div>
  </div>

  <div class="flex-container space-evenly">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
    <div class="flex-item">3</div>
  </div>
  
</body>
```
Agora preencha todas as classes com a propriedade justify-content e o valor correto. A cada propriedade que você aplicar, salve o código e veja a diferença no Live Server!

Agora mais um desafio: mude a `flex-direction` da classe `.flex-container` para que o eixo principal tenha como direção de cima para baixo. Em seguida, aplique a esta mesma classe uma altura de 500px. Agora compare o alinhamento do *flex-items* de cada container para que você veja como eles se comportam quando o *main axis* é alterado.

Viu só como o flexbox é extremamente poderoso? Só com o que você já sabe, é possível fazer os layouts bem construídos e flexíveis com muito mais facilidade! Mas ainda faltam algumas outras ferramentas de controle mais fino do alinhamento e tamanho dos itens para fecharmos o conteúdo!


### Alinhamento, alinhamento e mais alinhamento!

Além de ser possível alinhar os itens dentro do *main axis* utilizando a propriedade `justify-content`. também podemos alinhar os itens de acordo com o *cross axis*!

Para isso, temos uma propriedade específica: **align-items**! 

Até o momento você não provavelmente não pensou nisso, mas o atributo padrão do `align-items`, que é chamado de `stretch`, é o responsável pelo alinhamento da altura de todos os seus flex-items independentemente do conteúdo e cada um deles!

E a melhor parte é que como o `align-items: stretch;` é uma propriedade padrão do flexbox, você sequer precisa aplicá-la, a não ser que queira deixar bem específico em seu código esse comportamento por algum motivo.

Além do stretch, você pode aplicar à propriedade `align-items` os atributos   `flex-start`, `center` e `flex-end` do mesmo jeito que foi feito na propriedade justify-content: a única diferença é que o eixo no qual o conteúdo será alinhado é o *cross axis*, não o *main axis*.

Por fim, podemos também aplicar ao align-items o atributo `baseline`, que alinha o conteúdo de acordo com a "linha de base" do texto. Essa linha funciona mais ou menos como uma linha de caderno invisível, em cima da qual todas as letras são colocadas. [Para saber mais sobre o conceito de baseline, acesse aqui](https://material.io/design/typography/understanding-typography.html#type-properties).

Agora vamos experimentar o alinhamento do conteúdo no cross axis usando align-items! Copie o código abaixo e cole no seu VS Code:

```html 
<head>
  <style>
    .flex-container {
      background-color: #e4e8ec;
      box-sizing: border-box;
      padding: 10px;
      display: flex;
      margin: 0 0 20px;
    }

    .flex-item {
      padding: 10px;
      margin: 10px;
      background: white;
      border: 1px solid rgba(0,0,0,.125);
      border-radius: .25rem;
      width: 100%;
      text-align: center;
    }

    .flex-item:nth-child(1) {
      font-size: 60px;
    }

    .flex-item:nth-child(2) {
      font-size: 40px;
    }

    .flex-item:nth-child(3) {
      font-size: 30px;
    }

    /* Preencha as classes abaixo com a propriedade align-items e o com o valor indicado */
    .stretch {
      align-items: stretch;
    }

    .baseline {
      
    }

    .flex-start {
      
    }

    .center {
      
    }

    .flex-end {
      
    }
    
  </style>
</head>
<body>
  <div class="flex-container stretch">
    <div class="flex-item">A</div>
    <div class="flex-item">B</div>
    <div class="flex-item">C</div>
    <div class="flex-item">D</div>
  </div>

  <div class="flex-container baseline">
    <div class="flex-item">A</div>
    <div class="flex-item">B</div>
    <div class="flex-item">C</div>
    <div class="flex-item">D</div>
  </div>

  <div class="flex-container flex-start">
    <div class="flex-item">A</div>
    <div class="flex-item">B</div>
    <div class="flex-item">C</div>
    <div class="flex-item">D</div>
  </div>

  <div class="flex-container center">
    <div class="flex-item">A</div>
    <div class="flex-item">B</div>
    <div class="flex-item">C</div>
    <div class="flex-item">D</div>
  </div>

  <div class="flex-container flex-end">
    <div class="flex-item">A</div>
    <div class="flex-item">B</div>
    <div class="flex-item">C</div>
    <div class="flex-item">D</div>
  </div>
</body>
```

Agora utilize a propriedade que você acabou de aprender para alinhar os itens no *cross axis*, sem se esquecer de olhar a a diferença de alinhamento de cada um dos containers no *live server* do VS Code!


#### Align Self 

E se você quiser alinhar um item específico de maneira diferente dos demais, como pode fazer isso? É muito simples: basta utilizar a propriedade **align-self** no item que você quer alinhar de forma específica!

O `align-self` lhe permite ajustar o alinhamento de forma individual, sobrescrevendo qualquer alinhamento definido com o `align-items`. Os valores que `align-self`  aceitam são exatamente os mesmos do `align-items`, sendo a única diferença o escopo da ua aplicação.

*Volte ao exercício anterior e aplique a qualquer flex-item do primeiro container, de forma individual, um alinhamento diferente do que foi definido no exercício! Repita esse processo para cada flex-container.*


#### Order

A última opção de alinhamento que vamos ver não trata tanto do local no qual os flex-itens serão postos dentro do container, *mas sim da ordem no qual eles serão postos*!

Às vezes o seu layout pode requerer que a ordem seja trocada por algum motivo. Nesses casos, será possível reordenar os flex-items aplicando a eles a propriedade `order`!

Essa propriedade se aplica por padrão a todos os itens flex com o valor 0 e aceita qualquer número inteiro positivo ou negativo como valor. 

Todos os itens de mesmo valor serão ordenados de acordo com a sua posição no código. 

Entretanto, se a propriedade for aplicada com qualquer valor numérico a algum item, ele será posicionado de forma prioritária e de acordo com o valor estabelecido para ele e para os demais (que por padrão é zero).

Veja o exemplo:

![Como order funciona](https://i.ibb.co/8jB6sVB/order-property.png)

É claro que em condições normais, a melhor opção sempre será colocar os itens no HTML seguindo exatamente a mesma ordem em que eles aparecem na tela, por uma questão de semântica e de acessibilidade.

### Controlando tamanhos e quebra de linha:

Por fim, vamos aprender as propriedades CSS que controlam o tamanho dos itens flex e os manipulam diretamente por meio do flexbox. 

Isso é importante porque, por mais que você possa utilizar o `width` para ajustar o comportamento dos flex-items, é sempre bom ter mais ferramentas no nosso arsenal! Além disso, as propriedades que você vai ver agora funcionam de uma maneira um pouco diferente e em muitos contextos usá-las pode ser a melhor opção.

**flex-wrap:**

O flexbox, por padrão, irá fazer com que todos os itens sejam dispostos sobre o eixo principal em uma única linha, ou seja, o conteúdo nunca será quebrado. Quando não sobra espaço para todos os itens, o flex-container simplesmente os diminui para que caibam naquele espaço.

Isso é conveniente na maioria dos layouts, mas não em todos eles. Para nossa alegria, o flexbox possui uma propriedade chamada `flex-wrap`, que nos permite definir que o conteúdo, *ao invés de diminuir, será quebrado em múltiplas linhas*.

Para usar essa propriedade, basta aplicá-la da seguinte forma:

```css
.flex-container {
  flex-wrap: wrap;
}
```

Uma vez feito isso, o ponto de quebra será definido com base no tamanho do flex-container e dos itens, sendo que ela ocorrerá de forma dinâmica caso o tamanho do container seja alterado.

A propriedade flex-wrap tem como valor padrão o `nowrap`, que define que os itens não serão quebrados. 

É possível também aplicar à propriedade o valor `wrap-reverse`, que inverte a ordem na qual os itens quebrados serão dispostos na tela (as linhas decorrentes da quebra serão colocadas acima da original no flex-container padrão, por exemplo).

Para ver como o flex-wrap funciona, copie o seguinte código e cole no VS Code:

```html
<head>
  <style>
    .flex-container {
      background-color: #e4e8ec;
      box-sizing: border-box;
      padding: 10px;
      display: flex;
      margin: 0 0 20px;
      /* aplique o flex-wrap abaixo */

    }

    .flex-item {
      box-sizing: border-box;
      padding: 10px;
      margin: 10px;
      background: white;
      border: 1px solid rgba(0,0,0,.125);
      border-radius: .25rem;
      width: 25%;
      text-align: center;
    }
    
  </style>
</head>
<body>
  <div class="flex-container">
    <div class="flex-item">A</div>
    <div class="flex-item">B</div>
    <div class="flex-item">C</div>
    <div class="flex-item">D</div>
    <div class="flex-item">E</div>
    <div class="flex-item">F</div>
    <div class="flex-item">G</div>
    <div class="flex-item">H</div>
    <div class="flex-item">I</div>
    <div class="flex-item">J</div>
  </div>
</body>
``` 

Como você pode ver, a largura dos itens está definida como 25%, mas todos cabem na mesma linha. Agora aplique a propriedade `flex-wrap` no container e veja a mágica acontecer! Compare o que acontece quando você usa os valores `wrap` e `wrap-reverse`!

> **NOTA.:** Mesmo a largura sendo 25%, apenas três itens ficaram dispostos em cada linha. Tente descobrir porquê manipulando outras propriedades dos *flex-items*!

**Encolhendo e aumentando:**

Pra terminar o conteúdo de hoje, vamos dar uma olhada nas propriedades que controlam o tamanho dos itens flex!

Você já sabe que quando o tamanho do flex-container não é grande o suficiente para acomodar os flex-items, eles tem como comportamento padrão diminuir o próprio tamanho pra caber de forma ordenada dentro do seu container. Por outro lado, normalmente eles não crescem para além do seu tamanho máximo -- mas podemos mudar isso se quisermos!

A tão comentada flexibilidade do flexbox está justamente na possibilidade de ajuste automático das caixas que ficam dentro do container: elas podem aumentar ou diminuir de forma automática para melhor se adaptar ao container. Para isso, temos a propriedade `flex`, que possui como valor padrão o seguinte:

```css
.flex-item {
  flex:  0  1 auto;
}
```

Cada um dos valores da propriedade `flex` representa um propriedade que pode ser aplicada individualmente, sendo `flex` uma [propriedade shorthand](https://developer.mozilla.org/pt-BR/docs/Web/CSS/Shorthand_properties) das três propriedades seguintes:

```css
.flex-item {
  flex-grow:  0;
  flex-shrink:  1;
  flex-basis: auto;
}
```

Vamos agora explicar o que cada uma faz.

Primeiro, temos as propriedades `flex-grow` e `flex-shrink`, que são conhecidas como ***fatores flex*** porque controlam o quanto os itens flex irão aumentar ou diminuir para se adaptar ao container.

O **fator de crescimento (*flex-grow*)** é, por padrão, 0, ou seja, os itens flex não aumentam para preencher espaços vazios dentro do container.

Quando se dá ao flex-grow um valor maior que zero, esse valor é traduzido como uma requisição de uma parte do espaço livre disponível, sendo que 1 significa “100% do espaço livre”. Nesse caso, se apenas tivermos um elemento e atribuirmos a ele um `flex-grow: 1;`; ele preencherá sempre todo o espaço livre do container.

> **NOTA.:** Isso também significa que se você utilizar números decimais poderá ajustar de forma mais fina o quanto cada item crescerá, podendo inclusive ser que menos de 100% do espaço seja ocupado caso a soma dos flex-grow de cada item seja menor que 1!

Mas e se tivermos a soma dos flex-grow for maior que 1, o que vai acontecer? Será que vai rolar um overflow do conteúdo? Ou o flexbox vai dar um jeito de recalcular? Vamos conferir:

```html
<head>
  <style>
    .flex-container {
      background-color: #e4e8ec;
      box-sizing: border-box;
      padding: 10px;
      display: flex;
      margin: 0  0  20px;
      }

    .flex-item {
      box-sizing: border-box;
      padding: 10px;
      margin: 10px;
      background: white;
      border: 1px  solid  rgba(0,0,0,.125);
      border-radius: .25rem;
      width: 25%;
      text-align: center;
    }

    .a {
      
    }

    .b {
      
    }

  </style>
</head>
<body>
  <div class="flex-container">
    <div class="flex-item a">A</div>
    <div class="flex-item b">B</div>
  </div>
</body>
``` 
Copie o código acima e siga os passo a seguir, sempre salvado a cada passo e observando no live server como os elementos se comportam:

 1. Dê ao item A um flex-grow com valor 1;
 2. Dê ao item B um flex-grow com valor 1;
 3. Dê ao item A um flex-grow com valor 2;
 4. Dê ao item B um flex-grow com valor 3;
 5. Dê ao item A um flex-grow com valor 0.3;
 6. Dê ao item B um flex-grow com valor 0.4;

Viu só como os elementos flex se adaptam aos valores colocados?

O que acontece é que sempre que a soma dos flex-grow de todos os itens for ***maior*** que um, *a requisição dos 100% do espaço passará a ser igual ao valor da soma*, sendo que ***cada item utilizará uma parte desses 100% do espaço de forma proporcional ao próprio valor***!

De maneira oposta, como já vimos, caso a soma dos flex-grow seja ***menor*** que um, o valor que equivale a 100% do espaço permanece sendo 1, e nem todo o espaço será preenchido!

<hr>

O **fator de diminuição (*flex-shrink*)** , diferente do `flex-grow`, está ativo na configuração padrão, ou seja, os itens flex diminuem sempre que o espaço do container for menor que a soma das larguras dos flex-items.

O `flex-shrink` considera duas variáveis na hora de realizar a diminuição dos itens:

 - A quantidade de *espaço livre negativo*, ou seja, a diferença entre a soma dos tamanhos dos itens flex e  o tamanho do container.
 
 - O tamanho base de cada item flex.

Assim, se tivermos dois itens de tamanhos diferentes, eles serão reduzidos de maneira proporcional ao seu tamanho. Para ver como isso acontece, copie o código abaixo e cole no VS Code:

```html
<head>
  <style>
    .flex-container {
      background-color: #e4e8ec;
      box-sizing: border-box;
      padding: 10px;
      display: flex;
      margin: 0  0  20px;
      width: 50vw;
    }

    .flex-item {
      box-sizing: border-box;
      padding: 10px;
      margin: 10px;
      background: white;
      border: 1px  solid  rgba(0,0,0,.125);
      border-radius: .25rem;
      width: 25%;
      text-align: center;
    }

    .a {
      flex-shrink: 0;
      width: 50%;
    }

    .b {
      flex-shrink: 0;
      width: 100%;
    }

  </style>
</head>
<body>
  <div class="flex-container">
    <div class="flex-item a">A</div>
    <div class="flex-item b">B</div>
  </div>
</body>
``` 

Agora siga os passos seguintes, mais uma vez salvando e observando a cada passo:

 1. Dê ao item A um flex-shrink com valor 1;
 2. Dê ao item A um flex-shrink com valor 0 e ao B um flex-shrink com valor 1;
 3. Dê ao item A um flex-shrink com valor 1;
 4. Dê ao item B um flex-shrink com valor 3;

O importante nesse exercício é notar que, como as larguras dos dois itens são diferentes, se ambos tiverem o mesmo valor de `flex-shrink` (e esse valor for diferente de zero) eles sempre serão reduzidos na proporção da sua largura.

Para alterar essa proporção, você pode alterar o fator de diminuição (`flex-shrink`) de um dos itens, ou pode alterar o tamanho dos itens. No entanto, a forma mais apropriada de fazer isso não é com a já conhecida `width`, mas usando a última propriedade que veremos hoje: `flex-basis`! 

<hr>

A propriedade ***flex-basis*** serve para especificar o tamanho inicial do flex-item em um flex-container, podendo substituir `width` ou `height` a depender da direção do *main axis*. Esse será o tamanho considerando antes de se aplicar os fatores de aumento e diminuição que vimos acima.

Na prática, não existe muita diferença entre usar o `flex-basis` e usar o `width` ou `height`: o browser renderizará o conteúdo da mesmíssima forma. Só que existem alguns pontos que nos levam a considerar o uso do `flex-basis` no contexto de um container flex:

-  `flex-basis`  apenas funciona quando aplicado a itens flex.

-   `flex-basis`  funciona automaticamente de acordo com o main axis definido, ou seja, irá ajustar o width caso o eixo seja horizontal ou o height caso seja vertical.
    
-  E por último, se utilizarmos a propriedade shorthand `flex` que vimos no início dessa parte, esse valor pode ser definido de forma mais organizada que se for declarado em uma propriedade solta. Veja os exemplo a seguir, que fazem a mesma coisa:

```css
.flex-item {
  flex-grow: 2;
  flex-shrink: .5;
  width: 100px;
}
```
```css
.flex-item {
  flex: 2 .5 100px;
}
```

Vale ressaltar que a [documentação oficial do flexbox](https://www.w3.org/TR/css-flexbox-1/#flex-components) recomenda que ao invés de usar as propriedades `flex-grow`, `flex-shrink` e `flex-basis` separadas os desenvolvedores utilizem o shorthand `flex`, pois isso evita erros no CSS!

Agora que você já conheceu todo o potencial magnífico do flexbox, tá na hora de botar a mão na massa e praticar esse conhecimento!

### Agora a prática!

Todos os exercícios terão como base os seguintes códigos:

HTML:
```html
<!DOCTYPE  html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Exercício 1 - Flexbox</title>
  <!-- Faça um link para o seu arquivo css abaixo -->
  
</head>
<body>
  <div class="flex-container">
    <div class="flex-item"></div>
    <div class="flex-item"></div>
    <div class="flex-item"></div>
    <div class="flex-item"></div>
    <div class="flex-item"></div>
  </div>
</body>
</html>

```
CSS:
```css
.flex-container {
  background-color: rgba(0, 0, 0, .05);
  box-sizing: border-box;
  padding: 10px;
  /* modifique o container dessa linha pra baixo */

}

.flex-item {
  background: rgba(0, 0, 255, 0.333);
  border-radius: .25rem;
  border: 1px  solid  rgba(0,0,0,.225);
  box-sizing: border-box;
  margin: 5px;
  padding: 50px;
  /* modifique os itens dessa linha pra baixo */

}
```
Para cada exercício, você irá utilizar-se dos códigos acima, salvando-os na pasta desse bloco em seu repositório de exercícios (crie um se não tiver).

Agora você irá construir alguns layouts flexíveis usando tudo aquilo que aprendeu até o momento!

## Exercícios

### Exercício 1:
Copie os códigos base acima para o VS Code e salve-os em arquivos com os nomes `exercise-1.html` e `exercise-1.css`, respectivamente. Não esqueça de linkar o CSS e o HTML na área indicada e colocar um título apropriado!

Agora elabore um layout em que todos os itens se alinhem ao centro da barra, mantendo as mesmas dimensões. Faça isso usando apenas as propriedades que você aprendeu nesse conteúdo!

Deverá ficar mais ou menos assim:

![Layout - Exercício 1](https://i.ibb.co/mzb89Jr/exercise-1.png)

### Exercício 2:
Repita o processo do exercício 1 e crie os arquivos  `exercise-2.html` e `exercise-2.css`.


Agora elabore um layout em que todos os itens se *alinhem lateralmente* e *preencham 100% do espaço do container* usando apenas as propriedades que você aprendeu nesse conteúdo!

Deverá ficar mais ou menos assim:

![Layout - Exercício 2](https://i.ibb.co/Sm6f1F3/exercise-2.png)

### Exercício 3:
Repita o processo do exercício 1 e crie os arquivos  `exercise-3.html` e `exercise-3.css`.

Agora elabore um layout em que apenas o item do meio se expanda para preencher o espaço vazio e os outros quatro permaneçam com o mesmo tamanho.

> **DICA:** crie uma nova classe para alterar apenas o item do meio!

Deverá ficar mais ou menos assim:
![Layout - Exercício 3](https://i.ibb.co/yk1DqQz/exercise-3.png)

### Exercício 4:
Repita o processo do exercício 1 e crie os arquivos  `exercise-4.html` e `exercise-4.css`.

Agora elabore um layout de grid alternado de três linhas de forma que:

 1. A primeira linha tenha dois itens ocupando metade do espaço livre;
 2. A segunda linha deverá ter um único item ocupando todo o espaço da linha;
 3. A terceira linha deverá ser igual à primeira

Mais uma vez, fique à vontade para criar classes, mas você deve inserir nelas apenas as propriedades que aprendeu nesse conteúdo! 

Seu layout deve ficar mais ou menos assim:

![Layout - Exercício 4](https://i.ibb.co/rsGpg16/exercise-4.png)

### Exercício 5:
Repita o processo do exercício 1 e crie os arquivos  `exercise-5.html` e `exercise-5.css`.

Primeiramente, aplique ao container uma altura de 100vh. Isso fará com que ele ocupe todo o espaço em branco da tela.

Agora elabore um layout em que todos os itens estejam centralizados exatamente no meio da página, tanto verticalmente quanto horizontalmente!

Seu layout deverá ficar parecido com esse:

![Layout - Exercício 5](https://i.ibb.co/FJg9FYv/exercise-5.png)

### Exercício Bônus *(opcional)*:

Você já é capaz de criar layouts com muito mais facilidade do que antes, mas agora, como bônus, vamos tentar algo mais difícil!

Primeiro, defina a altura do container como 300px e a largura como 800px.

Agora utilize o mesmo código base dos exercícios anteriores para criar um layout que se pareça com um gráfico de barras como esse:

![Layout - Exercício Bônus](https://i.ibb.co/yQLNqnJ/exercise-bonus.png)

Você pode utilizar a propriedade `height` nos flex-items para completar esse exercício, mas se quiser levar suas habilidades de flexbox ao limite tente replicar esse layout apenas com o que você aprendeu nesse conteúdo!

> **DICAS:** tente utilizar o flex-wrap para fazer com que as barras quebrem, e utilize valores que não permitam às barras se acumularem na mesma linha. Lembre-se: esse layout não é sobre criar um gráfico de verdade, mas a *ilusão* de um gráfico!

## Recursos Adicionais

 1. [Documentação Oficial do Flexbox](https://www.w3.org/TR/css-flexbox-1/)
 2. [Flexbox Playground - Um guia visual para o Flexbox](https://demos.scotch.io/visual-guide-to-css3-flexbox-flexbox-playground/demos/)
 3. [Tutorial do MDN sobre o Flexbox](https://developer.mozilla.org/pt-BR/docs/Learn/CSS/CSS_layout/Flexbox)
 4. [Flexbox Froggy](https://flexboxfroggy.com/)