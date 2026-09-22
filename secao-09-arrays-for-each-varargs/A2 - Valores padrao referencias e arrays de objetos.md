# Valores padrão, referências e arrays de objetos

<sub>📚 [Documentação](../README.md) › [Seção 9 · Arrays, `for-each`, `var` e varargs](./README.md) › Material 2 de 8</sub>

Um array é criado no heap e recebe valores iniciais automaticamente. A variável usada pelo programa guarda uma referência para esse objeto, do mesmo modo que já acontecia com `Product` e `BankAccount`.

## Valores padrão dos elementos

Ao criar um array com `new`, cada posição recebe o valor padrão de seu tipo:

| Tipo do elemento | Valor padrão |
| --- | --- |
| `byte`, `short`, `int` e `long` | zero |
| `float` e `double` | zero positivo |
| `char` | caractere de código zero (`'\u0000'`) |
| `boolean` | `false` |
| qualquer tipo de referência | `null` |

```java
int[] numbers = new int[2];
boolean[] flags = new boolean[2];
String[] names = new String[2];

System.out.println(numbers[0]); // 0
System.out.println(flags[0]);   // false
System.out.println(names[0]);   // null
```

Esses valores são atribuídos aos elementos do array. Isso não muda a regra das variáveis locais comuns, que precisam ser inicializadas antes da leitura.

```java
int value;
// System.out.println(value); // não compila

int[] values = new int[1];
System.out.println(values[0]); // compila e imprime 0
```

## Arrays são objetos

Uma variável de array pode guardar `null`:

```java
int[] values = null;
```

Nesse caso, ainda não existe um array acessível pela variável. Tentar usar `values.length` ou `values[0]` causa `NullPointerException` durante a execução.

```java
int[] values = null;
// System.out.println(values.length); // falha em tempo de execução
```

Um array vazio é diferente de uma referência nula:

```java
int[] empty = new int[0];
int[] absent = null;

System.out.println(empty.length); // 0
// System.out.println(absent.length); // NullPointerException
```

## Duas variáveis, um mesmo array

A atribuição entre variáveis de array copia a referência, não os elementos:

```java
int[] first = {10, 20};
int[] second = first;

second[0] = 99;
System.out.println(first[0]); // 99
```

`first` e `second` apontam para o mesmo objeto. Esse compartilhamento de referência também é chamado de *aliasing*.

```text
first  ---+
          +--> [99, 20]
second ---+
```

A comparação com `==` verifica se as referências apontam para o mesmo array:

```java
int[] a = {1, 2};
int[] b = {1, 2};
int[] c = a;

System.out.println(a == b); // false
System.out.println(a == c); // true
```

A comparação dos conteúdos será feita com a classe `Arrays` na Aula 5.

## Arrays de objetos

Criar um array de `Product` não cria produtos:

```java
Product[] products = new Product[2];

System.out.println(products[0]); // null
System.out.println(products[1]); // null
```

O array possui duas posições capazes de guardar referências para objetos `Product`. Cada objeto precisa ser criado separadamente:

```java
products[0] = new Product("TV", 900.0, 1);
products[1] = new Product("Mouse", 50.0, 3);

System.out.println(products[0].getName());
```

O array e os produtos são objetos diferentes no heap.

```text
products --> [ referência | referência ]
                    |            |
                    v            v
               Product TV   Product Mouse
```

Uma posição pode continuar nula. Antes de usar seus métodos, o programa precisa saber se há um objeto nela:

```java
if (products[0] != null) {
    System.out.println(products[0].getName());
}
```

## Compatibilidade de tipos

O tipo do elemento controla o que pode ser armazenado:

```java
String[] names = new String[2];
names[0] = "Ana";
// names[1] = 10; // não compila
```

Arrays de tipos primitivos diferentes também não são compatíveis:

```java
int[] integers = {1, 2};
// long[] longs = integers; // não compila
```

Mesmo que um valor `int` isolado possa ser convertido para `long`, `int[]` não é `long[]`.

## Coleta de lixo

Se nenhuma referência alcança um array, ele se torna elegível à coleta de lixo:

```java
int[] values = {1, 2, 3};
values = new int[] {4, 5};
```

Depois da segunda instrução, o primeiro array fica elegível à coleta, desde que nenhuma outra variável ainda aponte para ele. Não é possível determinar exatamente quando o coletor o removerá.

## Exercícios de fixação

1. Quais são os valores iniciais de `new double[3]`, `new boolean[2]` e `new String[1]`?
2. Explique a diferença entre `new String[0]` e uma variável `String[]` com valor `null`.
3. Preveja a saída:

```java
int[] a = {1, 2};
int[] b = a;
b[1] = 7;
System.out.println(a[1]);
System.out.println(a == b);
```

4. Quantos objetos são criados por `Product[] data = new Product[3];`?
5. Por que `long[] values = new int[2];` não compila?

---

<div align="center">

⬅️ [A1 · Introdução aos arrays](./A1%20-%20Introducao%20aos%20arrays.md) &nbsp;·&nbsp; 📂 [Seção 9](./README.md) &nbsp;·&nbsp; [A3 · Percorrendo arrays com `for` e `for-each`](./A3%20-%20Percorrendo%20arrays%20com%20for%20e%20for-each.md) ➡️

</div>
