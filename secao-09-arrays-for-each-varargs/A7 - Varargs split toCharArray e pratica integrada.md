# Varargs, `split`, `toCharArray` e prática integrada

<sub>📚 [Documentação](../README.md) › [Seção 9 · Arrays, `for-each`, `var` e varargs](./README.md) › Material 7 de 8</sub>

Um método com varargs aceita uma quantidade variável de argumentos. A sintaxe é conveniente para quem chama o método, mas, dentro dele, o parâmetro continua sendo um array.

## Declarando um varargs

Os três pontos aparecem entre o tipo e o nome do parâmetro:

```java
static int sum(int... values) {
    int total = 0;

    for (int value : values) {
        total += value;
    }

    return total;
}
```

As chamadas podem fornecer zero, um ou vários argumentos:

```java
System.out.println(sum());          // 0
System.out.println(sum(5));         // 5
System.out.println(sum(1, 2, 3));   // 6
```

Também é possível passar um array já existente:

```java
int[] numbers = {4, 5};
System.out.println(sum(numbers)); // 9
```

## O parâmetro é um array

Dentro de `sum`, `values` possui o tipo `int[]`. Por isso, ele oferece `length`, índices e `for-each`.

Para uma chamada como `sum(1, 2, 3)`, o compilador prepara um array correspondente para a invocação.

## Regras de declaração

Um método pode declarar no máximo um varargs, e ele precisa ser o último parâmetro:

```java
static void print(String title, int... values) {
    System.out.println(title);
}
```

Estas declarações não compilam:

```java
// static void wrong(int... values, String title) { }
// static void wrong(int... first, int... second) { }
```

Os tipos `int...` e `int[]` produzem a mesma assinatura de método. Portanto, não podem formar duas sobrecargas:

```java
static void show(int... values) { }
// static void show(int[] values) { } // assinatura repetida
```

## Varargs e sobrecarga

Uma chamada de aridade fixa é escolhida antes de uma alternativa varargs quando ambas são aplicáveis:

```java
static void show(int value) {
    System.out.println("one");
}

static void show(int... values) {
    System.out.println("many");
}

show(10);       // one
show(10, 20);   // many
```

Regras mais complexas envolvendo boxing serão estudadas depois das classes wrapper, na Seção 14.

## Passando `null`

Como o parâmetro é um array, é possível passar uma referência nula explicitamente:

```java
int[] absent = null;
sum(absent);
```

O método compila, mas o `for-each` falha durante a execução porque não existe um array para percorrer. A chamada `sum()` é diferente: ela fornece um array vazio, não `null`.

## Transformando texto em array com `split`

O método `split` divide uma `String` e devolve `String[]`:

```java
String line = "Ana,8.5,9.0";
String[] parts = line.split(",");

System.out.println(parts[0]); // Ana
System.out.println(parts[1]); // 8.5
System.out.println(parts[2]); // 9.0
```

O separador é uma expressão regular. Alguns caracteres, como o ponto, possuem significado especial. Para separar pelo ponto literal, ele precisa ser escapado:

```java
String[] parts = "a.b.c".split("\\.");
```

O estudo detalhado de expressões regulares não é necessário nesta etapa; basta reconhecer que nem todo separador é interpretado literalmente.

## Transformando texto em caracteres

`toCharArray` cria um `char[]`:

```java
char[] letters = "Java".toCharArray();

for (char letter : letters) {
    System.out.println(letter);
}
```

Alterar esse array não modifica a `String` original, pois `String` é imutável:

```java
String word = "Java";
char[] letters = word.toCharArray();
letters[0] = 'L';

System.out.println(word);        // Java
System.out.println(letters);     // Lava
```

## Prática integrada: boletim

O programa a seguir separa nome e sobrenome com `split`, lê duas notas com `Scanner` e usa um método varargs para calcular a média.

```java
import java.util.Scanner;

public class Program {
    public static double average(double... values) {
        if (values.length == 0) {
            return 0.0;
        }

        double sum = 0.0;
        for (double value : values) {
            sum += value;
        }
        return sum / values.length;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter first and last name separated by comma: ");
        String[] nameParts = sc.nextLine().split(",");
        String name = nameParts[0].strip() + " " + nameParts[1].strip();

        System.out.print("Enter two grades: ");
        double first = sc.nextDouble();
        double second = sc.nextDouble();

        System.out.printf("%s: %.2f%n", name, average(first, second));

        sc.close();
    }
}
```

---

<div align="center">

⬅️ [A6 · Inferência local com `var` e variáveis sem nome](./A6%20-%20Inferencia%20local%20com%20var%20e%20variaveis%20sem%20nome.md) &nbsp;·&nbsp; 📂 [Seção 9](./README.md) &nbsp;·&nbsp; [A8 · A certificação OCP Java SE 25 e esta seção](./A8%20-%20A%20certificacao%20OCP%20Java%20SE%2025.md) ➡️

</div>
