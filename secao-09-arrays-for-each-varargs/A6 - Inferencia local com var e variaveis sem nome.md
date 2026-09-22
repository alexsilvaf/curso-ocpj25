# Inferência local com `var` e variáveis sem nome

<sub>📚 [Documentação](../README.md) › [Seção 9 · Arrays, `for-each`, `var` e varargs](./README.md) › Material 6 de 8</sub>

Java pode inferir o tipo de algumas variáveis locais a partir da expressão usada na inicialização. A palavra `var` reduz a repetição da escrita do tipo, mas não torna Java uma linguagem de tipagem dinâmica.

## Inferência não significa tipo variável

```java
var quantity = 10;                    // int
var price = 19.90;                    // double
var name = "Notebook";               // String
var values = new int[] {1, 2, 3};     // int[]
var product = new Product("TV", 900.0, 1); // Product
```

O compilador determina um tipo exato para cada variável. Depois disso, as regras são as mesmas de uma declaração explícita:

```java
var quantity = 10;
// quantity = "ten"; // não compila: quantity é int
```

`var` não significa “qualquer tipo” nem guarda a informação somente durante a execução.

## Onde `var` pode aparecer

`var` pode declarar uma variável local que possui inicializador:

```java
void calculate() {
    var total = 0;
}
```

Também pode aparecer na inicialização de um `for`:

```java
for (var index = 0; index < 3; index++) {
    System.out.println(index);
}
```

E como tipo da variável de um `for-each`:

```java
String[] names = {"Ana", "Bia"};

for (var name : names) {
    System.out.println(name);
}
```

Nesse caso, `name` é inferida como `String`.

## Onde `var` não pode aparecer

Não se usa `var` em campos, parâmetros comuns nem tipos de retorno:

```java
class Example {
    // private var value = 10; // campo: não compila

    // var calculate(var input) { // retorno e parâmetro: não compila
    //     return input;
    // }
}
```

O tipo também não pode ser inferido sem uma expressão apropriada:

```java
// var value;                    // sem inicializador
// var absent = null;            // null sozinho não fornece um tipo
// var numbers = {1, 2, 3};      // inicializador de array sem new
// var[] numbers = new int[3];   // var não recebe colchetes
```

A forma correta para o último caso é:

```java
var numbers = new int[] {1, 2, 3};
```

Uma declaração com `var` declara uma variável por vez:

```java
// var x = 1, y = 2; // não compila
```

## O tipo vem da expressão

O literal influencia o tipo inferido:

```java
var a = 10;   // int
var b = 10L;  // long
var c = 10.0; // double
```

A conversão explícita também influencia:

```java
var small = (byte) 10; // byte
```

Use `var` quando o tipo continuar claro para quem lê. Escrever o tipo explicitamente pode ser melhor quando a inferência esconder uma informação importante.

## Variáveis sem nome

Quando um valor precisa ser recebido por causa da sintaxe, mas não será utilizado, Java 25 permite declarar uma variável sem nome com `_`:

```java
int[] values = {4, 7, 9};

for (int _ : values) {
    System.out.println("One more element");
}
```

O laço executa uma vez por elemento, mas não precisa saber qual é o valor atual.

Uma variável sem nome também pode aparecer em uma declaração local com inicializador:

```java
int _ = calculate();
```

Nesse exemplo, `calculate()` é executado, mas seu resultado é descartado.

## Regras de `_`

`_` não cria um nome que possa ser lido posteriormente:

```java
int _ = 10;
// System.out.println(_); // não compila
```

Como não há um nome utilizável, mais de uma declaração sem nome pode existir no mesmo bloco:

```java
int _ = 10;
int _ = 20;
```

Isso é diferente de declarar duas variáveis comuns com o mesmo nome.

Uma variável sem nome deve possuir inicializador:

```java
// int _; // não compila
```

O mesmo marcador `_` voltará em lambdas e padrões quando essas estruturas forem ensinadas nas Seções 13 e 16.

## `var` e `_` não são sinônimos

- `var` pede que o compilador descubra o tipo de uma variável que será usada;
- `_` declara que o valor não será usado;
- `var _ = expression;` combina as duas ideias: o tipo é inferido e o resultado é descartado.

```java
var _ = calculate();
```

## Exercícios de fixação

1. Determine os tipos de `var x = 1`, `var y = 1L` e `var z = new double[2]`.
2. Explique por que `var value = null` não compila.
3. Corrija `var numbers = {1, 2, 3};`.
4. Escreva um `for-each` que use `_` apenas para contar quantos elementos existem, incrementando outra variável.
5. Diferencie inferência de tipo e tipagem dinâmica.

---

<div align="center">

⬅️ [A5 · Classe `Arrays`: ordenação, busca e cópia](./A5%20-%20Classe%20Arrays%20ordenacao%20busca%20e%20copia.md) &nbsp;·&nbsp; 📂 [Seção 9](./README.md) &nbsp;·&nbsp; [A7 · Varargs, `split`, `toCharArray` e prática integrada](./A7%20-%20Varargs%20split%20toCharArray%20e%20pratica%20integrada.md) ➡️

</div>
