# CSS: Flexbox

## O que vamos aprender?
Olá, Tryber!

No dia de hoje nós iremos aprender a utilizar uma das ferramentas mais poderosas para a criação de layouts em CSS: o **flexbox**!

## Você será capaz de?
Ao final do conteúdo de hoje, você será capaz de aplicar o *flexbox* nos seus sites e desenvolver os mais diversos layouts a partir dessa ferramenta, o que eliminará boa parte das dificuldades que você enfrentou até o momento quanto ao alinhamento e à centralização do conteúdo!

## Porque isso é importante?
Antes da implementação da versão 3 do CSS, as pessoas desenvolvedoras precisavam se virar nos 30 para deixar os seus sites com a aparência desejada usando a propriedade `display` com atributos que você já aprendeu: `float`, `inline-block`, `block`. Ou mesmo a propriedade `position`, em algumas situações bem específicas. 

Mas como você já sabe, criar um layout bem feito apenas com essas propriedades não é lá a coisa mais fácil do mundo. Existem tarefas que se tornam um pesadelo se apenas esses recursos estiverem disponíveis, dentre as quais:
-   Alinhar *verticalmente* um bloco de conteúdo *no centro* do bloco que o contém;
-   Fazer todos os elementos descendentes de um outro elemento ocuparem a mesma quantidade de espaço considerando a largura e altura disponíveis;
-   Fazer todas as colunas de um conteúdo possuírem a mesma altura mesmo tendo conteúdos de tamanhos diferentes.
Com a chegada do CSS3, foi introduzido um modelo que acabou de vez com esse problema: o *Flexible Boxes*, ou **flexbox**. Com ele, tornou-se possível desenvolver layouts com muito mais facilidade e precisão: ele organiza os elementos de uma forma previsível e que pode ser facilmente adaptada para diferentes browsers e tamanhos de tela.

Vamos ver com mais detalhes todas as possibilidades maravilhosas trazidas pelo *flexbox*?
 
## Conteúdos

Para conseguir entender de verdade como funciona o *flexbox*,  primeiro vamos relembrar o comportamento padrão de uma página HTML:

https://codepen.io/Coderesting/pen/yLyaJMz

<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
