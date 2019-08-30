# Guia (quase) completo de SCSS/SASS

Neste guia, **Sassy**, **Sass** e **Scss** se referirão aproximadamente à mesma coisa. Conceitualmente, não há muita diferença. Você aprenderá a diferença à medida que aprender mais, mas basicamente o **SCSS** é o que a maioria das pessoas utiliza agora. É apenas uma versão mais recente (e de acordo com alguns, superior) da sintaxe original do **Sass**.

`Nota: Todo o código Sass/SCSS é compilado de volta ao CSS padrão para que o navegador possa realmente entender e renderizar os resultados. Atualmente, os navegadores não têm suporte direto para Sass/SCSS ou qualquer outro pré-processamento CSS, nem a especificação CSS padrão fornece alternativas para recursos similares (ainda).`

 

## Let's begin!

Comecemos pelos princípios básicos do SCSS: **O que o Sass/SCSS pode fazer que o CSS Vanilla não pode?**

### 1. Regras aninhadas 

Aninhe suas propriedades CSS em vários conjuntos de colchetes. Isso torna seu código CSS um pouco mais limpo e intuitivo.

### 2. Variáveis

Css padrão tem, por definição, variáveis. Porém, você pode fazer muito mais com variáveis Sass: itere-as por um loop e gere valores de propriedade dinamicamente, Você pode incorporá-los aos próprios nomes de propriedades CSS. É útil para definições de "nome-propriedade-N {...}"

### 3. Melhores operadores

Você pode adicionar, subtrair, multiplicar e dividir valores CSS. Claro que o CSS padrão implementa isso via `calc()`, mas no Sass você não precisa usar o `calc()` e a implementação é um pouco mais intuitiva.

### 4. Funções

Sass permite criar definições de CSS como funções reutilizáveis. 

### 5. Trigonometria

Entre muitos dos seus recursos básicos, o SCSS permite que você escreva suas próprias funções, como seno e cosseno, inteiramente utilizando apenas a sintaxe Sass/SCSS, como faria em outras linguagens, como JavaScript, que nos ajudam a calcular o movimento de barras de progresso circulares ou criar efeitos de ondas animadas, por exemplo.

### 6. Instruções *for-loops*, *while-loops*, *if-else*

Você pode escrever CSS utilizando instruções familiares de controle e fluxo de código semelhantes a outras linguagens. O Sass controle apenas como a propriedade e os valores foram gerados. Não é uma linguagem em tempo real, apenas um pré-processador.

### 7. Mixins

Crie um conjunto de propriedades CSS uma vez e reutilize-as ou "misture" junto com quaisquer novas definições. Na prática, você pode usar mixins para criar temas separados para o mesmo layout, por exemplo. 



## Sass pré-processador

Sass não é dinâmico. Você não poderá gerar ou animar propriedades e valores de CSS em tempo real. Mas você pode gerá-los de uma maneira mais eficiente e deixar que as propriedades padrão (animação CSS, por exemplo) sejam recuperadas a partir daí.



## Nova sintaxe

O SCSS realmente não adiciona novos recursos à linguagem CSS. Apenas nova sintaxe que pode, em muitos casos, reduzir a quantidade de tempo gasto na criação de código CSS.

### Pré-requisitos

Os pré-processadores CSS adicionam novos recursos à sintaxe da linguagem CSS.

Existem 5 pré-processadores CSS: **Sass**, **SCSS**, **Less**, **Stylus** e **PostCSS**.

`Esse guia aborda principalmente o SCSS, que é semelhante as Sass. Mas você pode aprender mais sobre o Sass no site www.sass-lang.com.`

**SASS** - (**.sass**) **S**yntactically **A**wesome **S**tyle **S**heets.

**SCSS** - (**.scss**) **S**assy **C**ascading **S**tyle **S**heets.

As extensões **.sass** e **.scss** são semelhantes., mas não são as mesmas. Para entusiastas, é possível converter de **.sass** para **.scss** e vice-versa:

```bash
# Converter Sass para SCSS
sass-converter style.sass style.scss

# Converter SCSS para Sass
sass-converter style.scss style.sass
```

**Sass** foi a primeira especificação para o **Sassy CSS** com a extensão de arquivo .sass. O desenvolvimento começou em 2006, porém, mais tarde, uma sintaxe alternativa foi desenvolvida com a extensão **.scss**, que alguns desenvolvedores acreditam ser a melhor. Atualmente, não há suporte imediato ao **Sassy CSS** em nenhum navegador, independentemente da sintaxe ou extensão do Sass que você usaria. 

### Superset

O Sassy CSS em qualquer uma de suas manifestações é um superconjunto da linguagem CSS. Isso significa que tudo o que funciona em CSS ainda funcionará em Sass ou SCSS.

### Variáveis

**Sass/SCSS** permite que você trabalhe com variáveis. Eles são diferentes das variáveis CSS que começam com traço duplo `--var-color` que você provavelmente já viu antes. Em vez disso, começaram com um `$`:

```scss
$number: 1;
$color: #FF0000;
$text: "Piece of string."
$text: "Another string." !default;
$nothing: null;
```

Você pode tentar sobreescrever um nome de variável. Se `!default` for anexado à redefinição de variável e a variável já existir, ela não será atribuída novamente. Em outras palavras, isso significa que o valor final da variável `$text` deste exemplo ainda será "Piece of string". A segunda atribuição "Another string" é ignorada, porque o valor padrão já existe.

```scss
#container {
    content: $text;
}
```



## Regras aninhadas

Com o CSS padrão, os elementos aninhados são acessados via caracteres de espaço:

```css
/* Standard CSS */
#A {
    color: red;
}
#A #B {
    color: green;
}
#A #B #C p {
    color: blue;
}
```

O código aceima pode ser expresso com as regras aninhadas da Sassy da seguinte maneira:

```scss
/* Nested Rules */
#A {
    color: red;
    #B {
        color: green;
        #C p {
            color: blue;
        }
    }
}
```

Como você pode ver, essa sintaxe parece mais limpa e menos repetitiva.

Isso é particularmente útil para gerenciar layouts complexos. Dessa forma, o alinhamento no qual as propriedades CSS aninhadas são gravadas no código corresponde à estrutura real do layout do aplicativo.

Por trás dos panos, o pré-processador ainda o compila no código CSS padrão (mostrado acima), para que possa ser renderizado no navegador. Simplesmente mudamos a maneira como o CSS é escrito.

### O caractere &

O Sassy CSS adiciona a diretiva de caractere `&`.

```scss
#P {
    color: black;
    a {
        font-weight: bold;
        &:hover{
            color: red;
        }
    }
}
```

O código SCSS acima, convertido em CSS fica:

```css
#P { color: black; }
#P a { font-weight: bold; }
#P a:hover { color: red; }
```

## Mixins

Um mixin é definido pela diretiva @mixin (ou também conhecida como regra do mixin). 

```scss
@mixin flexible() {
    display: flex;
    justify-content: center;
    align-items: center;
}
.centered-elements {
    @include flexible();
    border: 1px solid gray;
}
```

Agora, toda vez que você aplica a classe `.centered-elements` a um elemento HTML, ele se transforma em Flexbox. Um dos principais benefícios dos mixins é que você pode usá-los juntamente com outras propriedades CSS. Você pode até passar argumentos para um @mixin como se fosse uma função e depois atribuí-los a propriedades CSS. Vamos dar uma olhada nisso na próxima seção.

### Exemplo de configuração multi-browser

Alguns recursos experimentais (como o baseado em -webkit) ou o Firefox (baseado em -moz) funcionam apenas nos navegadores em que aparecem. Os mixins são úteis na definição de propriedades CSS independentes do navegador em uma classe. Por exemplo, se você precisar rotacionar um elemento em navegadores baseados no Webkit, bem como nos outros, poderá criar este mixin que usa o argumento `$degree`:

```scss
@mixin rotate ($degree) {
    -webkit-transform: rotate($degree); //webkit-based
    -moz-transform: rotate($degree); 	//Firefox
    -ms-transform: rotate($degree);		//Internet Explorer
    -o-transform: rotate($degree);		//Opera
    transform: rotate($degree);			//Standand CSS
}
```

Agora é possível utilizar esse mixin com @include nas definições de classe CSS:

```scss
.rotate-element {
    @include rotate(45deg);
}
```

## Operadores aritméticos

Semelhante à sintaxe CSS padrão, você pode adicionar, subtrair, multiplicas e dividir valores, sem precisar usar a função `calc()` da sintaxe CSS clássica. Mas existem casos não óbvios que podem gerar erros.

### Adição

```scss
p {
    font-size: 10px + 2em; 	//*error: imcompatible units
    font-size: 10px + 6px; 	//16px
    font-size: 10px + 6;   	//16px
}
```

### Subtração

```scss
div {
    height: 12% - 2%;
    margin: 4rem - 1;
}
```

### Multiplicação

```scss
p {
    width: 10px * 10px;				//*error;
    width: 10px * 10;				//100px;
    width: 1px * 5 + 5px;			//10px;
    width: 5 * (5px + 5px);			//50px;
    width: 5px + (10px / 2) * 3;	//20px;
}
```

### Divisão

A divisão é um pouco complicada. Como no CSS padrão, o símbolo da divisão é reservado para uso em conjunto com outras propriedades de abreviação. Por exemplo, fonte: **24/32px** define uma fonte com tamanho de **25px** e altura de linha de **32px**. Mas o SCSS afirma ser compatível com o CSS padrão.

```css
p { font: 16px / 24px Arial, sans-serif; }
```

No CSS padrão, o símbolo de divisão aparecer na propriedade como abreviação, mas não é utilizado para realmente dividir valores. Então, como Sass lida com a divisão?

```scss
p {
    top: 16px / 24px;			//Saidas como CSS padrao
    top: (16px / 24px);			//Faz a divisao (quando parenteses sao adicionados)
    top: #{$var1} / #{$var2};	//Usa interpolacao, saida como CSS
    top: $var1 / $var2;			//Faz a divisao
    top: random(4) / 5;			//Faz a divisao (quando par com funcao)
    top: 2px / 4px + 3px		//Faz a divisao (quando parte da aritmetica)
}
```

Se você deseja dividir dois valores, basta adicionar parênteses ao redor da operação de divisão. Caso contrário, a divisão funcionará apenas em combinações com alguns dos outros operadores ou funções.

### Resto

O resto calcula o restante da operação de divisão. Neste exemplo, vamos ver como ele pode ser usado para criar um padrão de listras de zebra para um conjunto arbitrário de elementos HTML.

```scss
@mixin zebra() {
    @for $i from 1 through 7 {
        @if ($i % 2 == 1){
            .stripe-#{$i} {
                background-color: black;
                color: white;
            }
        }
    }
}
* { @include zebra (); }
```

Esse exemplo requer tais elementos HTML:

```html
<div class = "stripe-1">zebra</div>
<div class = "stripe-2">zebra</div>
<div class = "stripe-3">zebra</div>
<div class = "stripe-4">zebra</div>
<div class = "stripe-5">zebra</div>
<div class = "stripe-6">zebra</div>
<div class = "stripe-7">zebra</div>
```



## Operadores de comparação

| Operador | Exemplo | Descrição                                |
| -------- | ------- | ---------------------------------------- |
| ==       | x == y  | Retorna true se x e y forem iguais       |
| !=       | x  != y | Retorna true se x e y não forem iguais   |
| >        | x > y   | Retorna true se x for maior que y        |
| <        | x < y   | Retorna true se x for menos que y        |
| >=       | x >= y  | Retorna true se x for maior ou igual a y |
| <=       | x <= y  | Retorna true se x for menor ou igual a y |

Como utilizar os operadores de comparação na prática? Podem ser utilizados para escrever um @mixin que escolhe o tamanho do preenchimento se for maior que a margem:

 ```scss
@mixin spacing($padding, $margin) {
    @if ($padding > $margin) {
        padding: $padding;
    } @else {
        padding: $margin;
    }
}
.container {
    @include spacing(10px, 20px);
}
 ```

Após a compilação, o seguinte código CSS será gerado:

```css
.container { padding: 20px; }
```



## Operadores lógicos

| Operador | Exemplo | Descrição                         |
| -------- | ------- | --------------------------------- |
| and      | x and y | Retorna true se x e y forem true  |
| or       | x or y  | Returna true se x ou y forem true |
| not      | not x   | Retorna true se x não for true    |

```scss
@mixin button-color($height, $width) {
    @if(($height < $width) and ($width >= 35px)) {
        background-color: blue;
    } @else {
        background-color: green;
    }
}
.button {
    @include button-color(20px, 30px)
}
```

Exemplo de alteração de cor de um botão baseado no tamanho.

## Strings

Em alguns casos, é possível adicionar strings a valores CSS, desde que a string seja adicionada à direita:

```scss
p {
    font: 50px Ari + "al";	//Compila como 50px Arial
}
```

O exemplo a seguir, seguindo a mesma ideia do anterior mas escrito de outra maneira, ao compilar gera erro:

```scss
p {
    font: "50px " + Arial;	//Error
}
```

Você pode adicionar cadeias de caracteres sem aspas duplas, desde que a string não contenha espaços. Por exemplo, o exemplo a seguir não será compilado:

```scss
p:after {
    content: "Quoted string with " + added tail.;
}
```

Possível solução?

```scss
p:after {
    content: "Quoted string with " + "added tail.";
}
```

Também é possível adicionar números e strings:

```scss
p:after {
    content: "Long " + 12345678 + " Added";
}
```

Observe que a propriedade `content` funciona apenas com pseudo-seletores: `before` e `after`. É recomendável evitar o uso da propriedade `content` nas suas definições CSS e sempre especificar o conteúdo entre as tags HTML. Aqui, é explicado apenas no contexto de trabalho com cadeias de caracteres no Sass/SCSS.

## Instruções de controle de fluxo

O SCSS possui **funções()** e **@diretivas** (também conhecidas como regras). Já criamos um tipo de função quando analisamos os mixins para os quais você pode passar argumentos. Uma função geralmente tem um parêntese anexado ao final do nome da função. Uma diretiva / regra começa com um caractere @. Assim como no JavaScript ou em outras linguagens, o SCSS permite trabalhar com o conjunto padrão de instruções de controle de fluxo.

### if()

**if()** é uma função e seu uso é bastante primitivo. A instrução retornará um dos dois valores especificados, com base em uma condição:

```scss
/* Usando a funcao if() */
if (true, 1px, 2px) => 1px;
if (false, 1px, 2px) => 2px;
```

### @if

**@if** é uma diretiva usado para ramificar com base em uma condição.

```scss
/* Usando a diretiva @if */
p {
    @if 1 + 1 == 2 { border: 1px solid; }
    @if 7 < 5	   { border: 2px dotted; }
    @if null	   { border: 3px double; }
}
```

Essa instrução compila como:

```css
p { border: 1px solid; }
```

Um outro exemplo utilizando instruções if:

```scss
/* Criando a variavel $type */
$type: river;

/* Printa divs azuis se variavel for setada para river */
div {
    @if $type == river {
        color: blue;
    }
}

/* Colorizacao condicional no paragrafo */
p {
    @if $type == tree { color: green; }
    @else if $type == river { color: blue; }
    @else if $type == dirt { color: brown; }
}
```

### Checando existência de if pai


O símbolo AND & selecionará o elemento pai, se existir, ou retorne **null** caso contrário. Portanto, ele pode ser usado em combinação com uma diretiva **@if**.

Nos exemplos a seguir, vamos ver como podemos criar estilos CSS condicionais com base na existência ou não do elemento pai.

```scss
/* Checando existencia de if pai */
@mixin does-parent-exist {
    @if & {
        &:hover { color: blue; }
    } @else {
        a { color: blue; }
    }
}
p {
    @include does-parent-exist();
}
```

Se no pai não existir **&** avaliado como **null**, será usado um estilo alternativo.

### @for

A regra **@for** é utilizada para repetir definições de CSS várias vezes seguidas.

```scss
@for $i from 1 through 5 {
    .definition-#{$i} { width: 10px * $i; }
}
```

Que após compilação:

```css
.definition-1 { width: 10px; }
.definition-2 { width: 20px; }
.definition-3 { width: 30px; }
.definition-4 { width: 40px; }
.definition-5 { width: 50px; }
```

### @each

A regra **@each** pode ser utilizada para iterar sobre uma lista de valores.

```scss
@each $animal in platypus, lion, sheep, dove {
    .#{$animal}-icon {
        background-image: url("/images/#{$animal}.png");
	}
}
```

Esse código, após compilação:

```css
.platypus-icon {
    background-image: url("/images/platypus.png");
}
.lion-icon {
    background-image: url("/images/lion.png");
}
.sheep-icon {
    background-image: url("/images/sheep.png");
}
.dove-icon {
    background-image: url("/images/dove.png");
}
```

### @while

```scss
$index: 5;
@while $index >0 {
    .element-#{$index} { width: 10px * $index; }
    $index: $index - 1;
}
```

Após compilação:

```css
.element-5 { width: 50px; }
.element-4 { width: 40px; }
.element-3 { width: 30px; }
.element-2 { width: 20px; }
.element-1 { width: 10px; }
```

## Funções Sass

Utilizando Sass/SCSS, você pode definir funções como em qualquer outra linguagem. Vamos criar uma função de trezentos px que retorne um valor de **300px**.

```scss
@function three-hundred-px() {
    @return 300px;
}
.name {
    width: three-hundred-px();
    border: 1px solid gray;
    display: block;
    position: absolute;
}
```

Obvamente, as funções Sass podem retornar qualquer valor CSS válido e ser atribuídas a qualquer propriedade CSS que você possa imaginar. Eles podem até ser calculados, com base em um argumento passado:

```scss
@function double($width) {
    return $width * 2;
}
```

### Trigonometria Sass

As funções de trigonometria **sin** e **cos** são frequentemente encontradas como parte de classes internas em muitas linguagens, como JavaScript, por exemplo.

Acho que vale a pena aprender como eles funcionam, se você deseja reduzir o tempo necessário para criar animações da interface do usuário (digamos, por exemplo, uma barra de progresso giratória).

Aqui, demonstrarei alguns exemplos que reduzem o código ao mínimo para criar efeitos interessantes de animação usando a função **sin()**. Os mesmos princípios podem ser expandidos para serem usados para criar elementos interativos da interface do usuário (movimento ao redor de um círculo, desenhos ondulados etc.)

Usar trigonometria junto com CSS é uma ótima maneira de reduzir a largura de banda. Em vez de usar animações **.gif** (cada uma pode levar uma solicitação HTTP extra para carregar, pois as animações .gif não podem ser colocadas em uma única imagem).

Você pode escrever suas próprias funções trigonométricas no Sass.

### Escrevendo suas próprias funções em Sass

Vamos considerar a função **rad()**. Para sua definição, é necessário **pi()**.

```scss
@function pi() { @return 3.1459265359; }
```

Escrever funções no Sass/SCSS é muito parecido com JavaScript, por exemplo.

#### pow()

```scss
@function pow($number, $exp) {
    $value: 1;
    @if $exp > 0 {
        @for $i from 1 through $exp {
            $value: $value * $number;
        }
    }
    @else if $exp < 0 {
        @for $i from 1 through -$exp {
            $value: $value / $number;
        }
    }
    @return $value;
}
```

#### rad()

```scss
@function rad($angle) {
    $unit: unit($angle);
    $unitless: $angle / ($angle * 0 + 1);
    //Se o angulo for em 'deg', converte para radianos
    @if $unit == deg {
        $unitless: $unitless / 180 * pi();
    }
    @return $unitless;
}
```

#### sin()

```scss
@function sin($angle) {
    $sin: 0;
    $angle: rad($angle);
    // Iteracao de 10
    @for $i from 0 through 10 {
        $fact = fact(2 * $i + 1);
        $pow = pow($angle, (2 * $i + 1)) / $fact;
        $sin = $sin + pow(-1, $i) * ;
    }
    @return $sin;
}
```

#### Animação de oscilação

```scss
@import "compass/css3";

.atom {
    text-align: center;
    border-radius: 20px;
    height: 40px;
    width: 40px;
    margin: 1px;
    display: inline-block;
    border: 10px #1893e7 solid;
    /*Aplicando animacao de oscilacao*/
    animation: oscillate 3s ease-in-out infinite;
    /*Criando 15 classes para cada uma das 15 caixas*/
    @for $i from 1 through 15 {
        &:nth-child(#{$i}) {
            animation-delay: ( #{sin(.4) * ($i)}s );
        }
    }
}
@keyframes oscillate {
    0% { transform: translateY(0px); }
    50% { transform: translateY(200px); }
}
```

```html
<!-- Repete esse elemento 15x -->
<div class = "atom"></div>
```

