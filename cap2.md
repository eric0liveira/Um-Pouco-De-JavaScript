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

O tipo `number` representa número. 

Os números podem ser reais (a parte fracionária é separada por `.` ao invés do padrão ABTN `,`); 

```js
29.35; 
.05;      //Exibe 0.05.
-.8;      //Exibe -0.8.
-0.090000 //Exibe -0.09.
```

Inteiros;

```js
42;
+42.00; //Exibe 42.
42e-0;  //Exibe 42.
-42;
42.;    //Exibe 42.
```

Ou expressos em notação científica, caso em que o expoente é indicado após `e` ou `E`. 

```js
27e2;     //O mesmo que 27 * (10 ^ 2). Exibe 2700.
-27E2;    //Exibe -2700.
```

Além de número inteiro, a mantissa pode ser um número real;

```js
0.27e4;  //Exibe 2700.
-0.27e4;  //Exibe -2700.
```

Já o expoente não;

```js
27e0.2;    //Exibe SyntaxError.
```

Contudo o expoente pode ser negativo.

```js
27e-2;    //O mesmo que 27 * (10 ^ -2). Exibe 0.27.
```

#### Precisão

O tipo `number` segue o padrão IEEE 754 que determina representações de números binários de ponto flutuante de precisão dupla (64 bits). No entanto mesmo os números inteiros são armazenados dessa forma.

**Nota:** Foge do escopo do livro explicar como funciona o padrão IEEE 754 e como valores `number` são [convertidos](http://www.h-schmidt.net/FloatConverter/IEEE754.html) e armazenados. 

É possível utilizar de forma segura valores inteiros entre `-9007199254740991` e `9007199254740991`;

```js
-9007199254740991;  //Number.MIN_SAFE_INTEGER
9007199254740991;   //Number.MAX_SAFE_INTEGER
```

Se esses valores forem ultrapassados, inconsistências podem ocorrer.

```js
(-9007199254740991 - 1) === (-9007199254740991 - 2); //Exibe true.
```

Em notação científica os valores máximos são `-1.7976931348623157e+308` e `1.7976931348623157e+308`;

```js
-1.7976931348623157e+308; //-Number.MAX_VALUE
1.7976931348623157e+308;  //Number.MAX_VALUE
```

E os mínimos `-5e-324` e `5e-324`.

```js
-5e-324; //-Number.MIN_VALUE
5e-324;  //Number.MIN_VALUE
```

Caso os valores máximos sejam ultrapassados, resultarão em `Infinity`;

```js
-1.7976931348623157e+308 * 1.1; //Exibe -Infinity.
```

E os mínimos em `0`.

```js
-5e-324 * 0.1; //Exibe -0. 
```

Caso precise trabalhar com números maiores, pesquise por bibliotecas como [BigInteger.js](https://github.com/peterolson/BigInteger.js) ou [bignumber.js](https://github.com/MikeMcl/bignumber.js).

#### Problemas em Números Fracionários

Como os valores do tipo `number` são armazenados de forma binária e não há como converter de forma exata muitos dos números decimais fracionários, podemos encontrar inconsistências em resultados de operações matemáticas.

```js
0.4 - 0.1 === 0.3; //Exibe false.

0.3.toFixed(20); //Exibe "0.29999999999999998890".
```

#### Sistemas Numéricos

Além do decimal, que é o padrão, há o hexadecimal, o octal e o binário. 

Hexadecimais são indicados com `0x` ou `0X` à sua frente. 

```js
0x1a; //Exibe 16.
-0xff; //Exibe -255.
```

As letras que representam números (`A` - `F`) podem ser maiúsculas e/ou minúsculas.

```js
0XaA; //Exibe 170.
```

Se colocada alguma letra inválida será lançado um `SyntaxError`.

```js
0xg; //Exibe SyntaxError.
```

Octais são identificados com `0o` ou `0O`.

```js
0o20;   //Exibe 16.
-0o20;  //Exibe -16.
```

Evite usar `0O` por ser difícil a distinção dos caracteres em determinadas fontes.

```js
-0O01; //Exibe -1.
```

Octais podem ser identificados com apenas `0` à sua frente, porém seu uso é desaconselhado já que essa sintaxe não é aceita no `strict mode` do ES6.

```js
-010; //Exibe SyntaxError.
```

E também porque `08` e `09` são identificados como decimais.

```js
-09; //Exibe 9.
```

Binários são identificados com `0B` ou `0b`. 

```js
0b10000; //Exibe 16.
-0B10000; //Exibe -16.
```

Qualquer valor diferente de `0` e `1` lançará um `SyntaxError`.

```js
-0b2; //Exibe SyntaxError.
```

Nenhum desses sistemas aceita números fracionários.

```js
-0b100.0; //Exibe SyntaxError.
0x1d.0;   //Exibe SyntaxError.
0o5.0;   //Exibe SyntaxError.
```

Nem notação científica exponencial.

```js
-0b1e0; //Exibe SyntaxError.
0x1de0;   //Exibe SyntaxError.
0o5e0;   //Exibe SyntaxError.
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

Os `()` internos precedem os externos.

```js
((13 + 3) / 4) % 3 // 13 + 3 == 16 então 16 / 4 == 4 então 4 % 3 == 1. Exibe 1 
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
