# Um Pouco de JavaScript
# Capítulo 2: Tipos de Valores e Variáveis

## Tipos de Valores

Há 7 tipos: `number`, `string`, `boolean`, `object`, `symbol`, `undefined` e `null`.

```js
var numero = 42;
var palavra = "olá";
var condicao = true;
var objeto = {nome: 'Caio', idade: 26};
var simbolo = Symbol("identificador");
var indefinido;
var nulo = null;
```

Não se preocupe em decorar a sintaxe e os tipos agora. Conforme formos utilizando-os sua assimilação fluirá.

### Number

O tipo `number` representa um número. Esse número pode ser real, inteiro ou expresso em notação exponencial científica.

Os números que começam com `-` são negativos, e todos os outros positivos, começando com `+` ou não.

Números com notação exponencial têm o expoente indicado após `e` ou `E`. Esses expoentes podem ser positivos ou negativos.

Os números reais tem sua parte fracionária dividia por `.` ao invés do padrão ABTN `,`.

```js
var inteiro1 = 42;
var inteiro2 = +42.00; //Exibe 42
var inteiro3 = 42e-0; //Exibe 42
var inteiro4 = -42;
var inteiro5 = 42.; //Exibe 42

var real1 = 29.35; 
var real2 = .05; //Exibe 0.05
var real3 = -.8; //Exibe -0.8

var notacaoExp1 = 27e2; //O mesmo que 27 * (10 ^ 2). Exibe 2700
var notacaoExp2 = 27E+2; //Idem.
var notacaoExp3 = 0.27E+4; //Idem.
var notacaoExp4 = 27e-2; //O mesmo que 27 * (10 ^ -2). Exibe 0.27
var NotacaoExp5 = -27e-2 //Exibe -0.27
```

#### Precisão

O tipo `number` segue o padrão IEEE 754 que determina representações de números binários de ponto flutuante de precisão dupla (64 bits). No entanto mesmo os números inteiros são armazenados dessa forma.

Dos 64 bits: 1 bit para o sinal (positivo ou negativo), 11 bits para o expoente e 52 bits são utilizados para a mantissa.

**Nota:** Foge do escopo do livro explicar como funciona o padrão IEEE 754 e como valores `number` são [convertidos](http://www.h-schmidt.net/FloatConverter/IEEE754.html) e armazenados. Contudo, esteja ciente que é um cálculo complexo e que não prejudica o aprendizado de JS.

Simplificando: podemos utilizar valores inteiros entre -9007199254740991 e 9007199254740991 (mais de 9 quadrilhões) o que nós dá a segurança de utilizar inteiros de até 15 dígitos. 

No capítulo sobre o objeto Number você verá que há quatro propriedades que definem os valores mínimos e máximos para o tipo `number` (`Number.MAX_SAFE_INTEGER`,`Number.MIN_SAFE_INTEGER`, `Number.MAX_VALUE`, `Number.MIN_VALUE`).

Caso precise trabalhar com números maiores, pesquise por bibliotecas como [BigInteger.js](https://github.com/peterolson/BigInteger.js) ou [bignumber.js](https://github.com/MikeMcl/bignumber.js).

#### Zero

Há `+0` ou simplmesmente `0` bem como há `-0`. 

O zero negativo não é maior nem menor que o zero *positivo*. 

```js
var zero = 0 / -3 ; //Exibe -0.

var eZero = 0 === -0; //Exibe true.
```

#### Infinity

`+Infinity` e `-Infinity` representam números que ultrapassam os limites de representação. 

Qualquer operação aritmética que contenha `Infinity` resultará em `Infinity`. Exceto quando elevado à pontencia de `0`, caso em que resultará em 1.

```js
var infinito1 = -Infinity * -2; //Exibe Infinity
var infinito2 = 42 / 0; //Exibe Infinity
var infinito3 = Math.pow(Infinity, 0); //Infinity elevado a 0. Exibe 1

var infinito4 = -42 / 0; //Exibe -Infinity
var infinito5 = 2 / -0; //Idem
```

### NaN

`NaN` (Not a Number) é um número que representa que não é um número. 

Usualmente é resultado de uma operação aritmética em que ao menos um dos operandos não é um número.

```js
var naoNum1 = 21 * "dois"; //Exibe NaN.
var naoNum2 = "quarenta" / "três"; //Exibe NaN.
var naoNum3 = 58 - "sete"; //Exibe NaN.
var naoNum4 = "cinco" + 50; //Exibe cinco50?!? Concatenação de string. Explicarei na próxima seção!
```
Uma característica um tanto estranha de `NaN` é que ele é o único valor que nunca é igual a si.

```js
var eNaoNum = NaN === NaN //Exibe false.
```

#### Sistemas Numéricos

Além do decimal, que é o padrão, podemos utilizar o hexadecimal, o octal e o binário. 

Identificamos um número hexadecimal colocando `0x` ou `0X` à sua frente, no octal com `0o` ou `0O` e no binário `0b` ou `0B`. As letras entre `A` e `F`, no hexadecimal, podem ser maiúsculas ou não.

Para não ocasionar erros de leitura, evite utilizar `0O` para octais pois dependendo da fonte utilizada fica  difícil distinguir entre a letra e o número.

Podemos também identificar um octal colocando apenas um `0` à sua frente, porém essa sintaxe não será mais aceita no `strict mode` do ES6.

```js
var octal = 0o20; //Exibe 16.
var hexa = 0x1A; //Exibe 16.
var bin = 0b10000; //Exibe 16.

var octalNeg = -0O20; //Exibe -16.
var hexaNeg = -0X1a; //Exibe -16.
var binNeg = -0B10000; //Exibe -16.
```

Nenhum desses sistemas aceita `.` como separador da parte fracionária nem notação científica exponencial.


#### Problemas em Números Fracionários

Como os valores do tipo `number` são armazenados de forma binária e não há como converter de forma exata números fracionários, podemos encontrar inconsistências em resultados de operações matemáticas.

```js
var diferente = 0.4 - 0.1 === 0.3; //Exibe false.

var tresDecimos = 0.3.toFixed(20); //Método para exibir determinado número de casas decimais em string. Exibe "0.29999999999999998890".
```


#### Operações Aritméticas

```js
var soma = 5 + 37; //Exibe 42.
var divisao = 45 / 3; //Exibe 15.
```
