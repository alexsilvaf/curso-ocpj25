# Introdução aos arrays

<sub>📚 [Documentação](../README.md) › [Seção 9 · Arrays, `for-each`, `var` e varargs](./README.md) › Material 1 de 8</sub>

Até aqui, cada variável guardava um valor ou uma referência. Quando um programa precisa armazenar várias notas, criar `nota1`, `nota2`, `nota3` e assim por diante torna o código repetitivo. Um array reúne vários elementos do mesmo tipo em uma única estrutura.

## O que é um array

Um array é um objeto:

- de tamanho definido durante sua criação;
- cujas posições guardam elementos de um único tipo;
- acessado por índices inteiros;
- cujo primeiro índice é sempre zero.

```java
int[] notes = new int[3];
```

Essa instrução declara a variável `notes`, cria um array com três posições e guarda na variável a referência para esse objeto.

```text
índice       0     1     2
          +-----+-----+-----+
notes --> |  0  |  0  |  0  |
          +-----+-----+-----+
```

Os zeros iniciais são valores padrão. Eles serão estudados com mais cuidado na próxima aula.

## Declaração e criação

As duas declarações abaixo são válidas:

```java
int[] first;
int second[];
```

A primeira forma é preferida porque deixa claro que o tipo da variável é `int[]`.

Declarar a variável não cria o array:

```java
int[] notes;
notes = new int[3];
```

O tamanho precisa ser informado na criação. Ele pode vir de uma expressão calculada em tempo de execução:

```java
int amount = 4;
double[] prices = new double[amount];
```

Depois de criado, o tamanho do array não muda. A variável pode receber a referência de outro array, mas o objeto original não cresce nem diminui.

## Acessando posições

Cada elemento pode ser lido ou alterado pelo seu índice:

```java
int[] notes = new int[3];

notes[0] = 8;
notes[1] = 6;
notes[2] = 10;

System.out.println(notes[0]); // 8
System.out.println(notes[2]); // 10
```

Para um array com três elementos, os índices válidos são `0`, `1` e `2`. O maior índice é sempre `length - 1`.

```java
System.out.println(notes.length);     // 3
System.out.println(notes.length - 1); // 2
```

Em arrays, `length` é um campo e não recebe parênteses. Compare:

```java
notes.length       // tamanho do array
"Java".length()   // tamanho da String
```

## Índice inválido

O compilador aceita uma expressão inteira como índice, mesmo quando o valor só será conhecido durante a execução:

```java
int index = 3;
System.out.println(notes[index]);
```

O código compila, mas a execução falha porque não existe a posição `3`. O nome do erro é `ArrayIndexOutOfBoundsException`. Por enquanto, basta reconhecer a causa; o tratamento de exceções será ensinado na Seção 12.

Índices negativos também são inválidos.

## Inicialização com valores

Quando os valores já são conhecidos, declaração, criação e preenchimento podem aparecer juntos:

```java
int[] primes = {2, 3, 5, 7};
String[] weekdays = {"Mon", "Tue", "Wed"};
```

O compilador deduz o tamanho pela quantidade de elementos.

Também é possível escrever o tipo explicitamente:

```java
int[] primes = new int[] {2, 3, 5, 7};
```

Depois que a variável já foi declarada, as chaves isoladas não podem ser usadas:

```java
int[] values;
// values = {1, 2, 3};          // não compila
values = new int[] {1, 2, 3};  // compila
```

Não se informa o tamanho quando os elementos aparecem entre chaves:

```java
// int[] values = new int[3] {1, 2, 3}; // não compila
```

## Array vazio

Um array pode ter tamanho zero:

```java
int[] empty = new int[0];
System.out.println(empty.length); // 0
```

Ele é um objeto válido, mas não possui posição que possa ser acessada.

## Exercícios de fixação

1. Declare um array capaz de guardar cinco temperaturas do tipo `double`.
2. Preencha a primeira e a última posição com `18.5` e `27.0`.
3. Para `int[] data = {4, 8, 12}`, indique o valor de `data.length`, o primeiro índice e o último índice.
4. Explique por que `data[data.length]` compila, mas falha durante a execução.
5. Corrija: `String[] names; names = {"Ana", "Bia"};`.

---

<div align="center">

📂 [Seção 9](./README.md) &nbsp;·&nbsp; [A2 · Valores padrão, referências e arrays de objetos](./A2%20-%20Valores%20padrao%20referencias%20e%20arrays%20de%20objetos.md) ➡️

</div>
