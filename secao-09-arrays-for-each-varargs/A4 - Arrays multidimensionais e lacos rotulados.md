# Arrays multidimensionais e laços rotulados

<sub>📚 [Documentação](../README.md) › [Seção 9 · Arrays, `for-each`, `var` e varargs](./README.md) › Material 4 de 8</sub>

Java não possui um tipo especial para matrizes. Uma matriz é representada por um array cujos elementos também são arrays. Essa estrutura explica por que cada linha pode ter tamanho próprio.

## Criando uma matriz regular

```java
int[][] matrix = new int[2][3];
```

A variável `matrix` aponta para um array de duas posições. Cada posição aponta para um array de três inteiros.

```text
matrix --> [ ref ][ ref ]
             |      |
             v      v
          [0,0,0] [0,0,0]
```

O primeiro par de colchetes seleciona a linha; o segundo, a coluna:

```java
matrix[0][1] = 7;
matrix[1][2] = 9;

System.out.println(matrix[0][1]); // 7
```

## Tamanhos

```java
System.out.println(matrix.length);    // 2 linhas
System.out.println(matrix[0].length); // 3 colunas na linha 0
```

`matrix.length` não informa o total de números. Ele informa quantas referências para linhas existem no array externo.

## Inicialização abreviada

```java
int[][] table = {
    {1, 2, 3},
    {4, 5, 6}
};
```

As quebras de linha facilitam a leitura, mas não alteram a sintaxe.

## Arrays irregulares

Como cada linha é um array independente, seus tamanhos podem ser diferentes:

```java
int[][] triangle = new int[3][];

triangle[0] = new int[1];
triangle[1] = new int[2];
triangle[2] = new int[3];
```

Também é possível inicializar diretamente:

```java
int[][] triangle = {
    {1},
    {2, 3},
    {4, 5, 6}
};
```

Não assuma que todas as linhas têm o tamanho de `triangle[0]`.

## Linhas inicialmente nulas

Esta criação produz somente o array externo:

```java
int[][] data = new int[3][];
```

As três posições guardam `null` até que cada linha seja criada. Portanto, `data[0].length` falha durante a execução enquanto `data[0]` for nulo.

## Percorrendo com dois índices

```java
for (int row = 0; row < triangle.length; row++) {
    for (int column = 0; column < triangle[row].length; column++) {
        System.out.print(triangle[row][column] + " ");
    }
    System.out.println();
}
```

O limite do laço interno depende da linha atual.

## Percorrendo com dois `for-each`

```java
for (int[] row : triangle) {
    for (int value : row) {
        System.out.print(value + " ");
    }
    System.out.println();
}
```

No laço externo, cada elemento é um `int[]`. No laço interno, cada elemento é um `int`.

Se alguma linha puder ser nula, verifique antes de percorrê-la:

```java
for (int[] row : data) {
    if (row == null) {
        continue;
    }

    for (int value : row) {
        System.out.println(value);
    }
}
```

## `break` em laços aninhados

Um `break` sem rótulo encerra somente o laço mais interno:

```java
for (int[] row : triangle) {
    for (int value : row) {
        if (value == 5) {
            break;
        }
        System.out.println(value);
    }
}
```

O laço externo continua com a próxima linha.

## Rótulos

Um rótulo é um identificador seguido de dois-pontos. Ele permite indicar qual laço deve receber o `break` ou o `continue`:

```java
search:
for (int row = 0; row < triangle.length; row++) {
    for (int column = 0; column < triangle[row].length; column++) {
        if (triangle[row][column] == 5) {
            System.out.println("Found at " + row + ", " + column);
            break search;
        }
    }
}
```

`break search` encerra o laço marcado como `search` e, consequentemente, também abandona o laço interno.

Com `continue`, a execução começa a próxima repetição do laço rotulado:

```java
rows:
for (int[] row : triangle) {
    for (int value : row) {
        if (value < 0) {
            continue rows;
        }
    }
    System.out.println("Row without negative values");
}
```

O rótulo não é um `goto`: `break` e `continue` continuam sujeitos às estruturas às quais podem se aplicar.

## Mais dimensões

A mesma regra pode ser repetida:

```java
int[][][] cube = new int[2][3][4];
System.out.println(cube.length);       // 2
System.out.println(cube[0].length);    // 3
System.out.println(cube[0][0].length); // 4
```

O número de pares de colchetes indica a quantidade de níveis de arrays.

## Exercícios de fixação

1. Crie uma matriz `2 x 2`, preencha seus quatro valores e calcule a soma.
2. Qual é a saída de `int[][] data = {{1, 2}, {3}}; System.out.println(data[1].length);`?
3. Explique por que `new int[3][]` compila, mas `new int[][3]` não compila.
4. Modifique a busca com rótulo para procurar um valor informado em `target`.
5. Diferencie `break` de `break search` quando ambos aparecem no laço interno.

---

<div align="center">

⬅️ [A3 · Percorrendo arrays com `for` e `for-each`](./A3%20-%20Percorrendo%20arrays%20com%20for%20e%20for-each.md) &nbsp;·&nbsp; 📂 [Seção 9](./README.md) &nbsp;·&nbsp; [A5 · Classe `Arrays`: ordenação, busca e cópia](./A5%20-%20Classe%20Arrays%20ordenacao%20busca%20e%20copia.md) ➡️

</div>
