# Classe `Arrays`: ordenação, busca e cópia

<sub>📚 [Documentação](../README.md) › [Seção 9 · Arrays, `for-each`, `var` e varargs](./README.md) › Material 5 de 8</sub>

A classe `java.util.Arrays` reúne métodos estáticos para operações comuns. Ela não substitui os fundamentos de índices e laços, mas evita reimplementar algoritmos já oferecidos pela plataforma.

## Importação

```java
import java.util.Arrays;
```

Depois da importação, os métodos são chamados pelo nome da classe, pois são estáticos.

## Exibindo o conteúdo

Imprimir diretamente um array não mostra seus elementos de maneira conveniente:

```java
int[] values = {4, 1, 3};
System.out.println(values);
```

Use `Arrays.toString` para um array unidimensional:

```java
System.out.println(Arrays.toString(values)); // [4, 1, 3]
```

Para estruturas aninhadas, use `deepToString`:

```java
int[][] matrix = {{1, 2}, {3, 4}};
System.out.println(Arrays.deepToString(matrix)); // [[1, 2], [3, 4]]
```

## Ordenação

`sort` altera o próprio array:

```java
int[] values = {4, 1, 3};
Arrays.sort(values);
System.out.println(Arrays.toString(values)); // [1, 3, 4]
```

Textos são ordenados de acordo com a ordem natural definida por `String`, que considera os valores dos caracteres e diferencia letras maiúsculas de minúsculas:

```java
String[] names = {"bia", "Ana", "caio"};
Arrays.sort(names);
System.out.println(Arrays.toString(names)); // [Ana, bia, caio]
```

A ordenação personalizada de objetos dependerá de `Comparable` e `Comparator`, estudados na Seção 15.

## Busca binária

`binarySearch` procura um valor e devolve seu índice:

```java
int[] values = {1, 3, 4, 8};

System.out.println(Arrays.binarySearch(values, 4)); // 2
```

O array precisa estar ordenado segundo a mesma ordem usada pela busca. Em um array não ordenado, o resultado não possui significado confiável.

Quando o valor não existe, o resultado é negativo. A fórmula é:

```text
-(ponto de inserção) - 1
```

O ponto de inserção é o índice em que o valor poderia entrar sem quebrar a ordem.

```java
int[] values = {2, 4, 8};

System.out.println(Arrays.binarySearch(values, 1)); // -1
System.out.println(Arrays.binarySearch(values, 3)); // -2
System.out.println(Arrays.binarySearch(values, 9)); // -4
```

## Preenchimento

`fill` atribui o mesmo valor a todas as posições:

```java
int[] values = new int[4];
Arrays.fill(values, 7);

System.out.println(Arrays.toString(values)); // [7, 7, 7, 7]
```

Também existe uma forma que preenche o intervalo iniciado em um índice inclusivo e terminado em um índice exclusivo:

```java
int[] values = {0, 0, 0, 0, 0};
Arrays.fill(values, 1, 4, 9);

System.out.println(Arrays.toString(values)); // [0, 9, 9, 9, 0]
```

## Comparando conteúdos

`equals` compara tamanho e elementos na mesma ordem:

```java
int[] first = {1, 2};
int[] second = {1, 2};

System.out.println(first == second);            // false
System.out.println(Arrays.equals(first, second)); // true
```

Para arrays aninhados, use `deepEquals`:

```java
int[][] a = {{1}, {2}};
int[][] b = {{1}, {2}};

System.out.println(Arrays.deepEquals(a, b)); // true
```

`compare` faz uma comparação lexicográfica. Ele observa os elementos da esquerda para a direita e devolve um número negativo, zero ou positivo:

```java
System.out.println(Arrays.compare(new int[] {1, 2}, new int[] {1, 3})); // negativo
System.out.println(Arrays.compare(new int[] {1, 2}, new int[] {1, 2})); // 0
```

`mismatch` devolve o primeiro índice diferente ou `-1` quando não há diferença:

```java
System.out.println(Arrays.mismatch(
        new int[] {1, 5, 3},
        new int[] {1, 8, 3})); // 1
```

## Copiando

`copyOf` cria outro array:

```java
int[] original = {1, 2, 3};
int[] copy = Arrays.copyOf(original, original.length);

copy[0] = 99;
System.out.println(original[0]); // 1
```

O novo tamanho pode ser diferente. Posições adicionais recebem valores padrão; um tamanho menor descarta elementos do final:

```java
int[] larger = Arrays.copyOf(original, 5); // [1, 2, 3, 0, 0]
int[] smaller = Arrays.copyOf(original, 2); // [1, 2]
```

`copyOfRange` usa início inclusivo e fim exclusivo:

```java
int[] part = Arrays.copyOfRange(original, 1, 3); // [2, 3]
```

`clone` também produz um novo array unidimensional do mesmo tipo e tamanho:

```java
int[] copy = original.clone();
```

Em arrays de referências, essas operações copiam as referências, não os objetos apontados. Portanto, a cópia é superficial.

## Exercícios de fixação

1. Ordene `{9, 2, 7, 1}` e procure o valor `7`.
2. Calcule o resultado de `binarySearch` ao procurar `5` em `{2, 4, 8}`.
3. Diferencie `==` de `Arrays.equals`.
4. Qual é o resultado de copiar `{1, 2}` para um array de tamanho quatro?
5. Por que alterar um objeto alcançado por um array copiado pode ser percebido pelo array original?

---

<div align="center">

⬅️ [A4 · Arrays multidimensionais e laços rotulados](./A4%20-%20Arrays%20multidimensionais%20e%20lacos%20rotulados.md) &nbsp;·&nbsp; 📂 [Seção 9](./README.md) &nbsp;·&nbsp; [A6 · Inferência local com `var` e variáveis sem nome](./A6%20-%20Inferencia%20local%20com%20var%20e%20variaveis%20sem%20nome.md) ➡️

</div>
