# CSS: Flexbox


## O que vamos aprender?

Olá, Tryber!

No dia de hoje você irá aprender a utilizar uma das ferramentas mais poderosas para a criação de layouts em CSS: o **flexbox**!

O *CSS Flexible Box Layout Module Level 1*, ou ***flexbox*** para os íntimos, é um módulo que foi implementado na edição 3 do CSS e cuja finalidade é tornar mais fácil e eficiente o desenvolvimento de interfaces web fluidas e responsivas.


### Você será capaz de:

Ao final do conteúdo de hoje, você será capaz de aplicar o *flexbox* nos seus sites e desenvolver os mais diversos layouts a partir dessa ferramenta, o que eliminará boa parte das dificuldades que você enfrentou até o momento quanto ao alinhamento e à centralização do conteúdo!


## Porque isso é importante?

Antes da implementação da versão 3 do CSS, as pessoas desenvolvedoras precisavam se virar nos 30 para deixar os seus sites com a aparência desejada usando a propriedade `display` com atributos que você já aprendeu: `float`, `inline-block`, `block`. Ou mesmo a propriedade `position`, em algumas situações bem específicas. 

Mas como você já sabe, criar um layout bem feito apenas com essas propriedades não é lá a coisa mais fácil do mundo. Existem tarefas que se tornam um pesadelo se apenas esses recursos estiverem disponíveis, dentre as quais:
-   Alinhar *verticalmente* um bloco de conteúdo *no centro* do bloco que o contém;
-   Fazer todos os elementos descendentes de um outro elemento ocuparem a mesma quantidade de espaço considerando a largura e altura disponíveis;
-   Fazer todas as colunas de um conteúdo possuírem a mesma altura mesmo tendo conteúdos de tamanhos diferentes.
-  Possibilitar com muito menos dor de cabeça a criação de layouts responsivos, o que você aprenderá mis adiante!

Com a chegada do CSS3, foi introduzido um modelo que acabou de vez com esse problema: o *Flexible Boxes*, ou **flexbox**. Com ele, tornou-se possível desenvolver layouts com muito mais facilidade e precisão: ele organiza os elementos de uma forma previsível e que pode ser facilmente adaptada para diferentes browsers e tamanhos de tela.

Vamos ver com mais detalhes todas as possibilidades maravilhosas trazidas pelo *flexbox*?
 
 
## Conteúdos

### Aplicando o *flexbox* a um elemento:

Para conseguir entender de verdade como funciona o *flexbox*,  primeiro vamos relembrar o comportamento padrão de uma página HTML, considerando o seguinte código:
```
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

Para exemplificar, vejamos como fica a página com o layout padrão (após algumas estilizações no css pra deixar com a cara da Trybe :wink:):

![Layout sem flexbox](https://i.ibb.co/fDqSwh4/no-flex-example.png)

Mas e se quisermos colocar os artigos um do lado do outro, como podemos fazer?
Agora temos duas opções!

Opção 1 - Penar por ~~algumas horas~~ alguns minutos com o `display: float;` e eventualmente conseguir montar um layout ~~mais ou menos~~ funcional na base de muita tentativa e erro;

Opção 2 - **Usar o flexbox**!

Para começar a usufruir das maravilhas do CSS Flexible Boxes, basta aplicar na `section`, que é o elemento pai dos artigos no HTML, a seguinte propriedade CSS:

```
section {
  display: flex;
}
```
Sim, é só isso! Pelo penos em um primeiro momento, para começar a utilizar o *flexbox*, basta aplicar o atributo `flex` à propriedade `display` do elemento que servirá como o que chamamos de ***flex container***. Claro que isso não é tudo, mas já faz uma grande diferença! Vamos ver o nosso layout como ficou:

![Layout com flexbox](https://i.ibb.co/RzTqCCr/flex-example.png)

Muito mais fácil, não é mesmo? Mas isso é só uma fração do poder do *flexbox*!

Pra extrair o melhor da ferramenta, você precisará conhecer o conceito de eixos e direções que norteiam o funcionamento do *flexbox*. Assim você poderá poder utilizar algumas propriedades bem interessantes para manipular o layout das suas páginas web de forma ainda mais flexível e estender as possibilidades *ao infinito e além* :rocket:!

### Eixos e direções no flexbox:

O *flex container* é o elemento que servirá como pai dos *flex items*, ou seja, é o elemento cujo conteúdo será posicionado na tela de acordo com as especificações do *flexbox*! Além disso, a partir da sua definição com o `display: flex;`, você poderá facilmente alterar a a direção, alinhamento e demais comportamentos de todos os seus *flex items* de forma flexível. Mas como isso funciona?

Todo *flex container*, uma vez definido, será transformado em um plano com duas dimensões: horizontal e vertical, que servirão para alinhar os itens contidos nele. Essas dimensões são conhecidas como flex axes, ou eixos flex:

![Flex Axes](https://i.ibb.co/rMhTn67/flex-axes.png)

Como se pode ver, os eixos flex são os seguintes:
 - **Main axis (eixo principal)** : É o eixo no qual os itens do flex-container serão distribuídos, por padrão. Você pode ver na imagem acima que os itens 1 e 2 estão dispostos lado a lado e da esquerda para a direita porque seu posicionamento segue o main axis do container.

 - **Cross axis (eixo cruzado)** :  É o eixo perpendicular ao main axis. Por padrão, o cross axis será utilizado para expandir a altura dos itens contidos para que todos possuam a mesma altura independentemente do conteúdo. Também serve para alinhar os itens no eixo cruzado.

Vamos praticar um pouco?
Copie e cole o código html abaixo no seu VS Code:

```
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
  </style>
</head>
<body>
  <div  class="flex-container">
    <div  class="flex-item"></div>
    <div  class="flex-item"></div>
    <div  class="flex-item"></div>
  </div>
</body>
```
Agora utilize o espaço indicado no comentário para transformar o seu container em um flex-container!

Feito isso, observe algumas coisas:

 1. Qual o comportamento dos flex-items ao transformar o container em um flex-container?
 2. Qual a direção e a ordem em que esses itens são dispostos automaticamente?
 3. Qual a altura dos flex-items antes e depois de você criar o flex-container?
 4. Quais os eixos responsáveis por cada um desses comportamentos?

Não se esqueça de modificar a largura dos flex-items e ver como eles se comportam, principalmente quando a soma das larguras ultrapassa a largura do container!

Como você pôde ver, a forma como os eixos estão dispostos inicialmente é bem simples de se compreender. Mas o flexbox não se limita a seguir sempre esse modelo apresentado: ele é apenas um padrão. Agora vamos aprender como modificar esse comportamento padrão!

### Manipulando os eixos flex:
 
## Exercícios

## Recursos Adicionais