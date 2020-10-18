# BEM - Padrão de convenção de nomenclatura CSS

**BEM** (que significa **Block-Element-Modifier**) é um padrão de convenção de nomenclatura para nomes de classes CSS. Sua adoção é bastante ampla e é imensamente útil na criação de CSS mais fácil de ler, entender e dimensionar.

## Porque BEM

A nomeação do BEM fornece três benefícios específicos:

- Comunica propósito ou função;
- Comunica a estrutura do componente;
- Ele define um baixo nível consistente de especificidade para os seletores de estilo.

## Como funciona

Um nome de classe BEM inclui até três partes.

- Bloco: o elemento pai mais externo do componente é definido como o bloco.
- Elemento: dentro do componente pode haver um ou mais filhos chamados elementos.
- Modificador: Um bloco ou elemento pode ter uma variação significada por um modificador.

Se todos os três forem usados em um nome, seria algo como isto:

```css
[block]__[element]--[modifier]
```

Após essa breve introdução, vamos ver alguns exemplos específicos.

## Exemplos

### Componente sem elementos ou modificadores

Componentes simples podem empregar apenas um único elemento e, portanto, uma única classe que seria o bloco.

```html
<button class="”btn”"></button>

<style>
  .btn {
  }
</style>
```

### Componente com um modificador

Um componente pode ter uma variação. A variação deve ser implementada com uma classe modificadora.

```html
<!-- DO THIS -->
<button class="btn btn--secondary"></button>

<style>
  .btn {
    display: inline-block;
    color: blue;
  }
  .btn--secondary {
    color: green;
  }
</style>
```

Não use a classe modificadora sozinha. A classe modificadora visa aumentar, não substituir, a classe base.

```html
<!-- DON'T DO THIS -->
<button class="btn--secondary"></button>

<style>
  .btn--secondary {
    display: inline-block;
    color: green;
  }
</style>
```

### Componentes com elementos

Componentes mais complexos terão elementos filhos. Cada elemento filho que precisa de estilo deve incluir uma classe nomeada.

Um dos propósitos por trás do BEM é manter a especificidade baixa e consistente. Não omita os nomes das classes dos elementos filhos no seu HTML. Isso forçará você a usar um seletor com especificidade aumentada para estilizar esses elementos nus dentro do componente (consulte os elementos `img` e `figcaption` abaixo). Deixar essas classes de fora pode ser mais sucinto, mas você aumentará os riscos de problemas em cascata no futuro. Um objetivo do BEM é que a maioria dos seletores use apenas um nome de classe.

```html
<!-- DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg" />
  <figcaption class="photo__caption">Look at me!</figcaption>
</figure>

<style>
  .photo {
  } /* Specificity of 10 */
  .photo__img {
  } /* Specificity of 10 */
  .photo__caption {
  } /* Specificity of 10 */
</style>

<!-- DON'T DO THIS -->
<figure class="photo">
  <img src="me.jpg" />
  <figcaption>Look at me!</figcaption>
</figure>

<style>
  .photo {
  } /* Specificity of 10 */
  .photo img {
  } /* Specificity of 11 */
  .photo figcaption {
  } /* Specificity of 11 */
</style>
```

Se o seu componente tiver elementos filhos com vários níveis de profundidade, não tente representar cada nível no nome da classe. O BEM não se destina a comunicar profundidade estrutural. Um nome de classe BEM representando um elemento filho no componente deve incluir apenas o nome da base/bloco e o nome do elemento. Nos exemplos abaixo, observe que `photo__caption__quote` é um uso incorreto do BEM, enquanto `photo__quote` é mais apropriado.

```html
<!-- DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg" />
  <figcaption class="photo__caption">
    <blockquote class="photo__quote">Look at me!</blockquote>
  </figcaption>
</figure>

<style>
  .photo {
  }
  .photo__img {
  }
  .photo__caption {
  }
  .photo__quote {
  }
</style>

<!-- DON'T DO THIS -->
<figure class="photo">
  <img class="photo__img" src="me.jpg" />
  <figcaption class="photo__caption">
    <blockquote class="photo__caption__quote">
      <!-- never include more than one child element in a class name -->
      Look at me!
    </blockquote>
  </figcaption>
</figure>

<style>
  .photo {
  }
  .photo__img {
  }
  .photo__caption {
  }
  .photo__caption__quote {
  }
</style>
```

### Elemento com modificador

Em alguns casos, convém variar um único elemento em um componente. Nesses casos, adicione um modificador ao elemento em vez do componente. Descobri que modificar elementos é muito menos comum e menos útil do que modificar componentes inteiros.

```html
<figure class="photo">
  <img class="photo__img photo__img--framed" src="me.jpg" />
  <figcaption class="photo__caption photo__caption--large">
    Look at me!
  </figcaption>
</figure>

<style>
  .photo__img--framed {
    /* incremental style changes */
  }
  .photo__caption--large {
    /* incremental style changes */
  }
</style>
```

### Elementos de estilo baseado no modificador do componente

Se você estiver consistentemente modificando elementos do mesmo componente juntos da mesma maneira, considere adicionar o modificador à base do componente e ajustar estilos para cada elemento filho com base nesse modificador. Isso aumentará a especificidade, mas simplificará muito a modificação do seu componente.

```html
<!-- DO THIS -->
<figure class="photo photo--highlighted">
  <img class="photo__img" src="me.jpg" />
  <figcaption class="photo__caption">Look at me!</figcaption>
</figure>

<style>
  .photo--highlighted .photo__img {
  }
  .photo--highlighted .photo__caption {
  }
</style>

<!-- DON'T DO THIS -->
<figure class="photo">
  <img class="photo__img photo__img--highlighted" src="me.jpg" />
  <figcaption class="photo__caption photo__caption--highlighted">
    Look at me!
  </figcaption>
</figure>

<style>
  .photo__img--highlighted {
  }
  .photo__caption--highlighted {
  }
</style>
```

### Nomes com múltiplas palavras

Os nomes BEM intencionalmente usam sublinhados duplos e hífens duplos em vez de simples para separar o modificador de elemento de bloco. O motivo é que os hífens únicos podem ser usados como separadores de palavras. Os nomes das classes devem ser muito legíveis, portanto, a abreviação nem sempre é desejável, a menos que as abreviações sejam universalmente reconhecíveis.

```html
<!-- DO THIS -->
<div class="some-thesis some-thesis--fast-read">
  <div class="some-thesis__some-element"></div>
</div>

<style>
  .some-thesis {
  }
  .some-thesis--fast-read {
  }
  .some-thesis__some-element {
  }
</style>

<!-- DON'T DO THIS -->
// These class names are harder to read
<div class="somethesis somethesis--fastread">
  <div class="somethesis__someelement"></div>
</div>

<style>
  .somethesis {
  }
  .somethesis--fastread {
  }
  .somethesis__someelement {
  }
</style>
```

## Conclusão

A utilização do BEM é sempre recomendável, pois mesmo podendo ser diferente do que está acostumado, verá rapidamente os benefícios que ela oferece em projetos grandes e pequenos. E para isso, esses exemplos o auxiliarão a evitar alguns dos erros comuns cometidos pela maioria de nós ao mergulhar nesta convenção de nomes peculiares.
