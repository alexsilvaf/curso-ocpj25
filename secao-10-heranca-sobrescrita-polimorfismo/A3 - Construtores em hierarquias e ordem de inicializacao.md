# Construtores em hierarquias e ordem de inicialização

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Material 3 de 8</sub>

Um objeto de uma subclasse contém o estado definido por toda a hierarquia. Antes que a subclasse termine sua inicialização, a parte correspondente à superclasse precisa ser construída.

## Construtores não são herdados

```java
class Employee {
    Employee(String name) { }
}

class Manager extends Employee {
    Manager(String name) {
        super(name);
    }
}
```

`Manager` não herda `Employee(String)`. Ele declara seu próprio construtor e usa `super(name)` para invocar um construtor da superclasse direta.

## Chamada implícita a `super()`

Quando um construtor não escreve `this(...)` nem `super(...)`, o compilador insere uma chamada a `super()`:

```java
class Parent {
    Parent() {
        System.out.print("P");
    }
}

class Child extends Parent {
    Child() {
        // super(); inserido implicitamente
        System.out.print("C");
    }
}
```

`new Child()` imprime `PC`.

Se a superclasse não possui um construtor sem argumentos acessível, a subclasse precisa indicar outro construtor:

```java
class Parent {
    Parent(int value) { }
}

class Child extends Parent {
    Child() {
        super(10);
    }
}
```

Sem `super(10)`, o compilador tentaria inserir `super()`, que não existe.

## `this(...)` ou `super(...)`

Uma chamada `this(...)` escolhe outro construtor da mesma classe:

```java
class Manager extends Employee {
    Manager(String name) {
        this(name, 0.0);
    }

    Manager(String name, double bonus) {
        super(name);
    }
}
```

O primeiro construtor delega ao segundo; o segundo invoca a superclasse. Toda cadeia precisa terminar em um construtor que chame `super(...)`, explicitamente ou de modo implícito.

Um construtor não pode invocar diretamente `this(...)` e `super(...)` na mesma execução. Também não pode existir um ciclo entre construtores:

```java
class Example {
    Example() {
        this(1);
    }

    Example(int value) {
        // this(); // formaria um ciclo e não compilaria
    }
}
```

## Ordem de inicialização de instâncias

Considere:

```java
class Parent {
    int parentField = print("parent field");

    {
        print("parent block");
    }

    Parent() {
        print("parent constructor");
    }

    static int print(String text) {
        System.out.println(text);
        return 0;
    }
}

class Child extends Parent {
    int childField = print("child field");

    {
        print("child block");
    }

    Child() {
        print("child constructor");
    }
}
```

Ao executar `new Child()`, a ordem é:

1. inicializadores de campos e blocos de instância de `Parent`, na ordem textual;
2. corpo do construtor de `Parent`;
3. inicializadores de campos e blocos de instância de `Child`, na ordem textual;
4. corpo do construtor de `Child`.

A saída é:

```text
parent field
parent block
parent constructor
child field
child block
child constructor
```

Antes desses passos, a memória dos campos já recebeu seus valores padrão.

## Inicialização estática da hierarquia

Na primeira utilização que inicializa as classes, a superclasse é inicializada antes da subclasse:

```java
class Parent {
    static { System.out.print("PS "); }
}

class Child extends Parent {
    static { System.out.print("CS "); }
    Child() { System.out.print("C "); }
}
```

As duas criações:

```java
new Child();
new Child();
```

produzem `PS CS C C `. Blocos estáticos executam uma vez por inicialização da classe; o construtor executa para cada objeto.

## Corpos flexíveis de construtores no Java 25

Antes do Java 25, a invocação explícita `this(...)` ou `super(...)` precisava ser textualmente a primeira instrução. No Java 25, um prólogo restrito pode calcular e validar argumentos antes da chamada:

```java
class Employee {
    Employee(String name) { }
}

class Manager extends Employee {
    Manager(String name) {
        String normalized = name.strip();
        super(normalized);
    }
}
```

Esse código compila no Java 25. A variável local é calculada antes de iniciar a superclasse.

O objeto ainda está em construção durante o prólogo. Não se deve tentar observar ou expor essa instância incompleta. Parâmetros, variáveis locais e operações estáticas podem ser usados normalmente, mas campos da instância não podem ser lidos e métodos de instância não podem ser chamados antes de `super(...)` ou `this(...)`.

```java
class Manager extends Employee {
    private String department;

    Manager(String name) {
        // System.out.println(department); // leitura da instância antes de super
        // printDepartment();             // chamada de instância antes de super
        super(name);
    }

    void printDepartment() {
        System.out.println(department);
    }
}
```

Existe uma permissão importante: o prólogo pode atribuir campos declarados na própria classe por meio do operador de atribuição, mesmo antes de `super(...)`:

```java
class Parent {
    Parent() { }
}

class Child extends Parent {
    private final int code;

    Child(int code) {
        this.code = code; // atribuição permitida
        super();
    }
}
```

Essa permissão é para inicialização. Uma expressão como `System.out.println(this.code)` ainda tentaria ler o campo cedo demais e não compilaria. A regra permite preparar o estado sem deixar que uma instância parcialmente construída seja usada como se estivesse pronta.

## Exercícios de fixação

1. O que o compilador insere quando um construtor não escreve `this(...)` nem `super(...)`?
2. Por que uma subclasse pode deixar de compilar depois que a superclasse recebe apenas um construtor com parâmetros?
3. Ordene: inicializador de instância da subclasse, construtor da superclasse, bloco estático da subclasse e inicializador de instância da superclasse.
4. Quantas vezes os blocos estáticos executam ao criar três objetos consecutivos da mesma classe?
5. Escreva um construtor Java 25 que normalize um parâmetro localmente antes de passá-lo para `super(...)`.
6. Diferencie atribuir um campo próprio de ler esse campo no prólogo de um construtor.

---

<div align="center">

⬅️ [A2 · Membros herdados, acesso e palavra `super`](./A2%20-%20Membros%20herdados%20acesso%20e%20palavra%20super.md) &nbsp;·&nbsp; 📂 [Seção 10](./README.md) &nbsp;·&nbsp; [A4 · Sobrescrita de métodos](./A4%20-%20Sobrescrita%20de%20metodos.md) ➡️

</div>
