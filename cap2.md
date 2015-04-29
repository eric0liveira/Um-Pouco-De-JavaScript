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

O tipo `number` representa um valor numérico. Valor esse que pode ser um número real, um número inteiro ou um número expresso em notação exponencial científica.

Os números que começam com `-` são negativos, e todos os outros positivos, começando com `+` ou não.

Números com notação exponencial têm o expoente indicado após `e` ou `E`. Esses expoentes podem ser positivos ou negativos.

```js
var inteiro = 42;
var inteiro2 = +42.00; //Exibe 42.
var inteiro3 = 42e-0; //Exibe 42.
var inteiroNeg = -42;

var real = 29.35; //É utilizado . ao invés de , para separar as casas decimais.
var outroReal = .05; //Exibe 0.05.
var realNeg = -.8; //Exibe -0.8.

var notacaoExp = 27e2; //O mesmo que 27 * (10 ^ 2). Resulta em 2700.
var notacaoExpPos = 27E+2; //Igual ao anterior.
var notacaoExpPos2 = 0.27E+4; //Igual ao anterior.
var notacaoExpNeg = 27e-2; //O mesmo que 27 * (10 ^ -2). Resulta em 0.27.
var NotacaoExpNeg2 = -27e-2 //Exibe -0.27.
```

#### Precisão

O tipo `number` segue o padrão IEEE 754 que determina representações de números binários de ponto flutuante de precisão dupla com 64 bits. No entanto mesmo os números inteiros são armazenados dessa forma.

Dos 64 bits: 1 bit para o sinal (positivo ou negativo), 11 bits para o expoente e 52 bits são utilizados para a mantissa.

**Nota:** Foge do escopo do livro explicar como funciona a conversão de números decimais para números binários normalizados pelo padrão IEEE 754. Contudo, esteja ciente que é um cálculo complexo e que pouco agrega ao conhecimento de uso de tipos `number`.

Simplificando a definição: podemos utilizar valores inteiros entre -9007199254740991 e 9007199254740991, intervalo de mais de 18 quadrilhões, ou simplificando ainda mais, podemos utilizar números inteiros de até 15 dígitos de forma segura. 

No capítulo sobre o objeto Number veremos que há quatro propriedades que definem os valores mínimos e máximos para o tipo `number` (`Number.MAX_SAFE_INTEGER`,`Number.MIN_SAFE_INTEGER`, `Number.MAX_VALUE`, `Number.MIN_VALUE`).

Caso precise trabalhar com números maiores, pesquise por bibliotecas como [BigInteger.js](https://github.com/peterolson/BigInteger.js) ou [bignumber.js](https://github.com/MikeMcl/bignumber.js).

#### Zero

Há `+0` ou simplmesmente `0` bem como há `-0`. 

O zero negativo não é maior nem menor que o zero *padrão*. 

```js
var zeroNeg = 0 / -3 ; //Exibe -0.

var eZero = 0 === -0; //Exibe true.
```

#### Infinity

`+Infinity` e `-Infinity` representam números que ultrapassam os limites de representação. 

Qualquer operação aritmética que contenha `Infinity` resultará em `Infinity`. Exceto elevado à pontencia de `0`, caso que resultará em 1.

```js
var infinito = -Infinity * -2 //Exibe Infinity
var infinito2 = 42 / 0; //Exibe Infinity
var infinito3 = Math.pow(Infinity, 0); //Exibe 1

var infinitoNeg = -42 / 0; //Exibe -Infinity
var infinitoNeg2 = 2 / -0; //Idem
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


#### Representação Decimal mas Nem Tanto

O sistema decimal foi desenvolvido por cima do sistema binário, que é natural à linguagem dos computadores.

```js

```


#### Operações Aritméticas

```js
var soma = 5 + 37; //Exibe 42.
var divisao = 45 / 3; //Exibe 15.
```
