# Percorrendo arrays com `for` e `for-each`

<sub>📚 [Documentação](../README.md) › [Seção 9 · Arrays, `for-each`, `var` e varargs](./README.md) › Material 3 de 8</sub>

Percorrer um array significa visitar suas posições. Como os índices formam uma sequência de `0` até `length - 1`, o `for` tradicional se encaixa naturalmente nessa tarefa.

## Percurso com índice

```java
int[] notes = {8, 6, 10};

for (int i = 0; i < notes.length; i++) {
    System.out.println("Position " + i + ": " + notes[i]);
}
```

A condição usa `<`, e não `<=`. Quando `i` chega a `notes.length`, já não existe uma posição correspondente.

Um percurso de trás para frente também usa os limites do array:

```java
for (int i = notes.length - 1; i >= 0; i--) {
    System.out.println(notes[i]);
}
```

## Soma e média

```java
double[] prices = {10.0, 20.0, 15.0};
double sum = 0.0;

for (int i = 0; i < prices.length; i++) {
    sum += prices[i];
}

double average = sum / prices.length;
System.out.println(average); // 15.0
```

Antes de dividir pelo tamanho, um programa que aceita arrays vazios deve verificar `prices.length > 0`.

## Busca sequencial

O índice é útil quando o resultado da busca deve indicar uma posição:

```java
String[] names = {"Ana", "Bia", "Caio"};
String target = "Bia";
int foundAt = -1;

for (int i = 0; i < names.length; i++) {
    if (names[i].equals(target)) {
        foundAt = i;
        break;
    }
}

System.out.println(foundAt); // 1
```

O valor `-1` representa “não encontrado”, pois índices válidos nunca são negativos.

## O laço `for-each`

Quando o índice não é necessário, o `for-each` oferece diretamente cada elemento:

```java
int[] notes = {8, 6, 10};

for (int note : notes) {
    System.out.println(note);
}
```

Leia a declaração como “para cada `note` do tipo `int` em `notes`”. O tipo da variável deve ser compatível com o tipo dos elementos.

O cálculo da soma fica mais direto:

```java
int total = 0;

for (int note : notes) {
    total += note;
}
```

## A variável recebe uma cópia do elemento

Em um array de primitivos, a variável do `for-each` recebe uma cópia do valor. Reatribuí-la não altera o array:

```java
int[] values = {1, 2, 3};

for (int value : values) {
    value *= 10;
}

System.out.println(values[0]); // 1
```

Para substituir os elementos, use os índices:

```java
for (int i = 0; i < values.length; i++) {
    values[i] *= 10;
}
```

## `for-each` com referências

Em um array de objetos, cada iteração copia uma referência. É possível alterar o objeto alcançado por ela:

```java
Product[] products = {
    new Product("TV", 900.0, 1),
    new Product("Mouse", 50.0, 3)
};

for (Product product : products) {
    product.setPrice(product.getPrice() * 1.10);
}
```

Entretanto, reatribuir a variável local não troca a posição do array:

```java
for (Product product : products) {
    product = null;
}

System.out.println(products[0] == null); // false
```

## Quando usar cada forma

Use o `for` tradicional quando precisar:

- conhecer ou exibir o índice;
- substituir elementos;
- percorrer apenas parte do array;
- andar em ordem diferente da esquerda para a direita;
- comparar posições vizinhas.

Use `for-each` quando precisar apenas processar cada elemento, do primeiro ao último.

## `break` e `continue`

As instruções já conhecidas continuam válidas:

```java
for (int value : values) {
    if (value < 0) {
        continue;
    }
    if (value == 100) {
        break;
    }
    System.out.println(value);
}
```

`continue` passa para o próximo elemento; `break` encerra o laço.

## Exercícios de fixação

1. Percorra `int[] values = {5, 8, 2, 9}` e encontre o maior valor.
2. Exiba somente os elementos que estão em índices pares.
3. Reescreva com `for-each` um laço que apenas soma todos os elementos.
4. Explique por que `for (int value : values) value = 0;` não zera o array.
5. Para qual tarefa o índice é indispensável: exibir todos os nomes ou trocar o primeiro nome pelo último?

---

<div align="center">

⬅️ [A2 · Valores padrão, referências e arrays de objetos](./A2%20-%20Valores%20padrao%20referencias%20e%20arrays%20de%20objetos.md) &nbsp;·&nbsp; 📂 [Seção 9](./README.md) &nbsp;·&nbsp; [A4 · Arrays multidimensionais e laços rotulados](./A4%20-%20Arrays%20multidimensionais%20e%20lacos%20rotulados.md) ➡️

</div>
