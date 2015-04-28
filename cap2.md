# Um Pouco de JavaScript
# Capítulo 2: Tipos de Valores e Variáveis

## Tipos de Valores

Há 8 tipos: `string`, `number`, `boolean`, `object`, `array`, `symbol`, `undefined` e `null`.

```js
var numero = 42;
var palavra = "olá";
var condicao = true;
var objeto = {nome: 'Caio', idade: 26};
var vetor = [21, 'Hoje', false];
var simbolo = Symbol("identificador");
var indefinido;
var nulo = null;
```

Não se preocupe em decorar a sintaxe e os tipos agora. Conforme formos utilizando-os sua assimilação fluirá.

### Number

O tipo `number` representa um valor numérico. Valor esse que pode ser um número real, um número inteiro ou um número expresso em notação exponencial científica. Positivo ou negativo.

```js
var inteiro = 42;
var inteiroNeg = -8;
var precisaoDupla = 29.35; //É utilizado . ao invés de , para separar as casas decimais.
var outraPrecisaoDupla = .05; //Exibe 0.05
var precisaoDuplaNeg = -.8; //Exibe -0.8.
var notacaoExp = 27e2; //O mesmo que 27 * 10 ^ 2. Resulta em 2700.
var notacaoExp = 27e+2; //Igual ao anterior.
var notacaoExp3 = 27e-2; //O mesmo que 27 * 10 ^ -2. Resulta em 0.27.
```

#### Precisão

Os valores de tipo `number` têm sempre a capacidade de 64 bits, o que significa que independente do valor ser 1 ou 1000000000 a quantidade de memória alocada será sempre igual.

Dos 64 bits: 52 bits são utilizados para a mantissa, 11 bits para o expoente e 1 bit para o sinal (positivo ou negativo).

No capítulo sobre o objeto Number veremos que há quatro propriedades que definem os valores mínimos e máximos (`Number.MAX_SAFE_INTEGER`,`Number.MIN_SAFE_INTEGER`, `Number.MAX_VALUE`, `Number.MIN_VALUE`).  

#### Sistemas Numéricos

Além do decimal, podemos utilizar o hexadecimal, o octal e o binário. A letra b usada para identificar binários e a letra x para hexadecimais podem ser maiúsculas ou não, bem como as letras entre A e F dos valores hexa.

```js
var octal = 020; //Exibe 16.
var hexa = 0x1A; //Exibe 16.
var bin = `0b1100`; //Exibe 12.
```

#### Representação Decimal mas Nem Tanto

O sistema decimal foi desenvolvido por cima do sistema binário, que é natural à linguagem dos computadores.

```js

```


#### Operações Aritméticas

```js
var soma = 5 + 37; //Exibe 42.
var divisao = 45 / 3; //Exibe 15.
```
