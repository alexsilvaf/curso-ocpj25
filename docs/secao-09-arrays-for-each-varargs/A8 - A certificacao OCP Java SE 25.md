# A certificação OCP Java SE 25 e esta seção

<sub>📚 [Documentação](../README.md) › [Seção 9 · Arrays, `for-each`, `var` e varargs](./README.md) › Material 8 de 8</sub>

Arrays aparecem na OCP Java SE 25 tanto como assunto direto quanto como base para varargs, métodos, controle de fluxo e APIs. As questões costumam explorar diferenças pequenas entre sintaxes parecidas e entre erro de compilação e falha durante a execução.

## Pontos que precisam estar consolidados

- um array possui tamanho fixo definido na criação;
- índices válidos vão de zero até `length - 1`;
- `length` é um campo do array, sem parênteses;
- elementos recebem valores padrão, mas variáveis locais comuns não;
- criar um array de referências não cria os objetos de cada posição;
- atribuir uma variável de array a outra compartilha a referência;
- `==` compara referências; `Arrays.equals` compara conteúdos unidimensionais;
- o `for-each` não fornece índice e reatribuir sua variável não substitui o elemento;
- cada linha de um array multidimensional é outro array e pode ter tamanho diferente ou ser nula;
- `binarySearch` pressupõe uma ordenação compatível;
- `var` só pode inferir variáveis locais com inicializador adequado;
- `_` representa uma variável sem nome e não pode ser lido;
- dentro do método, um parâmetro varargs é um array;
- só pode existir um varargs, sempre na última posição dos parâmetros.

## Questões de leitura de código

### 1. Limites

```java
int[] values = new int[3];
System.out.println(values[values.length - 1]);
```

Compila e imprime `0`. O último índice é `2`, e o elemento possui valor padrão.

### 2. `length`

```java
String[] names = {"Ana", "Bia"};
System.out.println(names.length);
System.out.println(names[0].length());
```

Imprime `2` e `3`. O array usa o campo `length`; a `String` usa o método `length()`.

### 3. Inicializador isolado

```java
int[] values;
// values = {1, 2};
```

A atribuição comentada não compila. Depois da declaração, é necessário escrever `new int[] {1, 2}`.

### 4. Compartilhamento

```java
int[] first = {1, 2};
int[] second = first;
second[0]++;
System.out.println(first[0]);
```

Imprime `2`, pois as duas variáveis apontam para o mesmo array.

### 5. Objetos não criados

```java
Product[] products = new Product[1];
System.out.println(products[0]);
```

Imprime `null`. O array foi criado, mas nenhum `Product` foi colocado nele.

### 6. `for-each`

```java
int[] values = {1, 2, 3};
for (int value : values) {
    value++;
}
System.out.println(values[0]);
```

Imprime `1`: a variável `value` recebe uma cópia de cada número.

### 7. Array irregular

```java
int[][] data = {{1, 2}, null, {3}};
System.out.println(data.length);
System.out.println(data[2].length);
```

Imprime `3` e `1`. Tentar ler `data[1].length` causaria `NullPointerException`.

### 8. Rótulo

```java
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer;
        }
        System.out.print(i + "" + j + " ");
    }
}
```

A saída é `00 01 02 10 `. O `break outer` encerra os dois laços quando os índices chegam a `1` e `1`.

### 9. Busca binária

```java
int[] values = {2, 4, 8};
System.out.println(java.util.Arrays.binarySearch(values, 5));
```

Imprime `-3`. O valor entraria no índice `2`; aplica-se `-2 - 1`.

### 10. Cópia

```java
int[] original = {1, 2};
int[] copy = java.util.Arrays.copyOf(original, 3);
copy[0] = 9;
System.out.println(original[0] + " " + copy[2]);
```

Imprime `1 0`. É outro array, e a posição adicional recebeu o valor padrão.

### 11. Inferência

```java
var values = new int[] {1, 2};
// values = new long[] {1, 2};
```

`values` foi inferida como `int[]`; a segunda atribuição não compila.

### 12. Sem nome

```java
int count = 0;
for (int _ : new int[3]) {
    count++;
}
System.out.println(count);
```

Compila no Java 25 e imprime `3`. O elemento atual é deliberadamente ignorado.

### 13. Varargs vazio

```java
static void show(int... values) {
    System.out.println(values.length);
}

show();
```

Imprime `0`. Uma chamada sem argumentos fornece um array vazio.

### 14. Assinatura repetida

```java
static void run(int... values) { }
// static void run(int[] values) { }
```

A segunda declaração não compila porque as duas formas representam a mesma assinatura.

### 15. `split`

```java
String[] parts = "a,b,c".split(",");
System.out.println(parts[1]);
```

Imprime `b`.

## Armadilhas frequentes

- usar `<= array.length` em um percurso crescente;
- escrever `array.length()` como se fosse um método;
- confundir array vazio com referência nula;
- acreditar que `new Product[3]` cria três produtos;
- usar `==` para comparar conteúdo;
- esperar que a variável do `for-each` substitua o elemento;
- usar o tamanho da primeira linha como limite de todas as linhas;
- executar `binarySearch` antes de ordenar;
- tratar `var` como um tipo que muda durante a execução;
- tentar ler `_`;
- declarar um parâmetro depois do varargs.

## O que continua planejado

Esta seção não apresenta collections nem generics. Ainda serão estudados:

- arrays em hierarquias e arrays polimórficos, na Seção 10;
- collections e arrays de objetos ordenados com `Comparable` e `Comparator`, na Seção 15;
- lambdas, incluindo parâmetros sem nome, na Seção 16;
- streams sobre arrays, na Seção 17;
- regras de boxing e unboxing na resolução de sobrecargas, na Seção 14.

## Referências

- [JLS 25 — Arrays](https://docs.oracle.com/javase/specs/jls/se25/html/jls-10.html).
- [JLS 25 — Local Variable Type Inference](https://docs.oracle.com/javase/specs/jls/se25/html/jls-14.html#jls-14.4).
- [JLS 25 — Unnamed Variables](https://docs.oracle.com/javase/specs/jls/se25/html/jls-14.html#jls-14.4.2).
- [Java SE 25 API — `Arrays`](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/Arrays.html).

---

<div align="center">

⬅️ [A7 · Varargs, `split`, `toCharArray` e prática integrada](./A7%20-%20Varargs%20split%20toCharArray%20e%20pratica%20integrada.md) &nbsp;·&nbsp; 📂 [Seção 9](./README.md) &nbsp;·&nbsp; [Seção 10 · Herança, sobrescrita e polimorfismo](../secao-10-heranca-sobrescrita-polimorfismo/README.md) ➡️

</div>
