# Um Pouco de JavaScript
# Capítulo 2: Tipos de Valores

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
var inteiro6 = 42

var real1 = 29.35; 
var real2 = .05; //Exibe 0.05
var real3 = -.8; //Exibe -0.8
var real4 = -0.090000 //Exibe -0.09

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

No capítulo sobre o objeto `Number` você verá que há quatro propriedades que definem os valores mínimos e máximos para o tipo `number` (`Number.MAX_SAFE_INTEGER`,`Number.MIN_SAFE_INTEGER`, `Number.MAX_VALUE`, `Number.MIN_VALUE`).

Caso precise trabalhar com números maiores, pesquise por bibliotecas como [BigInteger.js](https://github.com/peterolson/BigInteger.js) ou [bignumber.js](https://github.com/MikeMcl/bignumber.js).

#### Sistemas Numéricos

Além do decimal, que é o padrão, pode-se utilizar o hexadecimal, o octal e o binário. 

Identifica-se um número hexadecimal colocando `0x` à sua frente, no octal `0o` e no binário `0b`. Essas letras podem ser maiúsculas, bem como as letras utilizadas nos valores hexadecimais.

Evite utilizar `0O` para octais pois dependendo da fonte utilizada no código-fonte torna-se difícil distinguir entre a letra `O` maiúscula e o número `0`.

É possível também identificar um octal colocando apenas um `0` à sua frente, porém seu uso é desaconselhado já que essa sintaxe não será mais aceita no `strict mode` do ES6.

```js
var octal = 0o20; //Exibe 16.
var hexa = 0x1A; //Exibe 16.
var bin = 0b10000; //Exibe 16.

var octalNeg = -0O20; //Exibe -16.
var hexaNeg = -0X1a; //Exibe -16.
var binNeg = -0B10000; //Exibe -16.
```

Nenhum desses sistemas aceita números fracionários ou notação científica exponencial.

#### Problemas em Números Fracionários

Como os valores do tipo `number` são armazenados de forma binária e não há como converter de forma exata muitos dos números decimais fracionários, podemos encontrar inconsistências em resultados de operações matemáticas.

```js
var diferente = 0.4 - 0.1 === 0.3; //Exibe false.

var tresDecimos = 0.3.toFixed(20); //Exibe "0.29999999999999998890".
```

#### Operações Aritméticas Básicas

É possível utilizar adição `+`, subtração `-`, divisão `/`, multiplicação `*` e resto de divisão `%`.

```js
5 + 37;   //Exibe 42.
50 - 42;  //Exibe 8.
60 / 4;   //Exibe 15.
12 * 3;   //Exibe 36.
5 % 2;    //Exibe 1.
```

Operações aritméticas mais complexas serão cobertas no capítulo sobre o objeto `Math`.

#### Precedência dos Operadores Aritméticos

As expressões são avaliadas da esquerda para a direita levando em conta a precedência dos operadores para realizar as associações entre os operandos e assim efetuar os cálculos.

Precedência dos operadores:
* `*`, `/` e `%`
* `+` e `-`

Operações com operadores de mesmo nível de precedência ocorrem pela ordem de surgimento. 

```js
10 / 2 % 3;   //10 / 2 == 5 então 5 % 3 == 2. Exibe 2 
```

A precedência dos operadores pode ser contornada com o uso de `()`.

```js
10 / (2 % 3);   //2 % 3 == 2 então 10 / 2 == 5. Exibe 5.
```

#### Zero Negativo

Há `-0` em JS.

```js
0 / -3 ;  //Exibe -0.
```

Tem o mesmo valor que o `+0`, diferindo apenas em sua polaridade.

```js
0 === -0;   //Exibe true.
```

#### Infinity

`Infinity` (ou `+Infinity`)  é um número que representa o infinito positivo, assim como `-Infinity` representa o infinito negativo.

```js
typeof Infinity;  //Exibe "number".
```

Números divididos por `0` resultam em `Infinity` ou `-Infinity`, dependendo dos sinais dos operandos.

```js
-42 / -0;   //Exibe Infinity
42 / -0;    //Exibe -Infinity
```

Números maiores que 1.797693134862315E+308 ou menores que -1.797693134862315E+308 são convertidos em `Infinity` e `-Infinity` respectivamente.

```js
-1.797693134862315E+308 * 1.1;   //Exibe -Infinity
```

Operações aritméticas que contenham `Infinity` resultarão em `Infinity`. 

```js
-Infinity / -2;   //Exibe Infinity.
1 - Infinity;     //Exibe -Infinity.
```

Exceto quando elevado à pontência de `0`, caso em que resultará 1.

```js
Math.pow(-Infinity, 0); //-Infinity elevado a 0. Exibe 1
```

Ou quando divide `0`.

```js
0 / -Infinity;  //Exibe -0.
```

Ou quando multiplicado por `0`.

```js
Infinity * 0;  //Exibe NaN.
```

Ou quando houver um `NaN`.

```js
NaN + -Infinity; //Exibe NaN.
```

Ou ainda quando um `Infinity` for dividido por outro `Infinity`.

```js
Infinity / -Infinity; //Exibe NaN
```

### NaN

`NaN` (Not a Number) é uma representação de um número inválido. 

Ainda assim é um número.

```js
typeof NaN;   //Exibe "number"
```

Usualmente é resultado de uma operação aritmética em que um dos operandos não pode ser transformado em um número.

```js
21 * "dois";        //Exibe NaN.
"quarenta" / true;  //Exibe NaN.
"cinco" + 50;       //Exibe cinco50?!? Concatenação de string!
```

Ou quando `0` é dividido por `0`.

```js
0 / -0;  //Exibe NaN.
```

Operações aritméticas que contenham `NaN` sempre resultarão em `NaN`.

```js
4 + NaN * 2;  //Exibe NaN.
```

E é o único valor em JS que nunca é igual a si.

```js
NaN === NaN;   //Exibe false.
```
