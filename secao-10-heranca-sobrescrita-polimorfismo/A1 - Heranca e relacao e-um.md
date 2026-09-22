# Herança e relação “é um”

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Material 1 de 8</sub>

Herança permite criar uma classe a partir de outra quando existe uma relação conceitual de especialização. A nova classe reaproveita o estado e o comportamento disponíveis na classe mais geral e pode acrescentar características próprias.

## O problema da repetição

Considere duas classes inicialmente independentes:

```java
class Employee {
    private String name;
    private double baseSalary;

    // construtores e métodos
}

class Manager {
    private String name;
    private double baseSalary;
    private double bonus;

    // construtores e métodos
}
```

Um gerente também possui nome e salário-base. Repetir esses membros cria duas implementações que precisam permanecer consistentes.

## Superclasse e subclasse

`Manager` pode especializar `Employee`:

```java
class Employee {
    private String name;
    private double baseSalary;

    Employee(String name, double baseSalary) {
        this.name = name;
        this.baseSalary = baseSalary;
    }

    public String getName() {
        return name;
    }

    public double getBaseSalary() {
        return baseSalary;
    }
}
```

```java
class Manager extends Employee {
    private double bonus;

    Manager(String name, double baseSalary, double bonus) {
        super(name, baseSalary);
        this.bonus = bonus;
    }

    public double getBonus() {
        return bonus;
    }
}
```

Na declaração:

- `Employee` é a superclasse, classe-base ou classe-pai;
- `Manager` é a subclasse, classe derivada ou classe-filha;
- `extends` declara a relação de herança;
- todo objeto `Manager` também pode ser tratado como um `Employee`.

A chamada `super(...)` será aprofundada na Aula 3. Por enquanto, ela entrega à superclasse os dados necessários para construir a parte `Employee` do objeto.

## Relação “é um”

Antes de usar herança, complete mentalmente a frase:

> Um `Manager` é um `Employee`?

Se a frase representa corretamente o domínio, a herança pode fazer sentido. Compare:

- um gerente **é um** empregado: possível herança;
- um empregado **tem um** endereço: não é herança; é associação entre objetos;
- um carro **tem um** motor: `Car extends Engine` estaria conceitualmente errado.

Herança não deve ser usada apenas para copiar código.

## O objeto continua sendo único

```java
Manager manager = new Manager("Ana", 8_000.0, 2_000.0);
```

Existe um único objeto `Manager`. Ele contém o estado definido por sua superclasse e o estado acrescentado pela subclasse.

```text
Manager
+--------------------------------+
| parte Employee                 |
|   name = "Ana"                |
|   baseSalary = 8000.0          |
+--------------------------------+
| parte Manager                  |
|   bonus = 2000.0               |
+--------------------------------+
```

“Parte” é uma forma didática de acompanhar a construção; não significa que dois objetos foram criados.

## Herança é transitiva

Uma hierarquia pode ter mais níveis:

```java
class Person { }

class Employee extends Person { }

class Manager extends Employee { }
```

`Manager` é um `Employee` e também é um `Person`.

Cada classe pode estender diretamente apenas uma classe:

```java
// class Manager extends Employee, Person { } // não compila
```

Java não oferece herança múltipla de classes. A implementação de várias interfaces será estudada na Seção 11.

## `Object` no topo

Quando uma classe não declara `extends`, sua superclasse direta é `Object`:

```java
class Employee { }
```

É equivalente, quanto à relação de herança, a:

```java
class Employee extends Object { }
```

A classe `Object` e seus métodos serão aprofundados na Seção 11.

## O que não é herdado

Construtores não são herdados. `Manager` precisa declarar seus próprios construtores. Membros `private` da superclasse também não ficam diretamente acessíveis pelo código da subclasse; esse ponto será detalhado na próxima aula.

## Exercícios de fixação

1. Identifique superclasse e subclasse em `class SavingsAccount extends Account`.
2. Explique por que `House extends Address` não representa bem uma relação “é um”.
3. Em `Dog extends Animal`, um `Dog` também é um `Object`? Justifique.
4. Quantos objetos são criados por `new Manager(...)`?
5. Por que um construtor de `Employee` não passa automaticamente a existir em `Manager`?

---

<div align="center">

📂 [Seção 10](./README.md) &nbsp;·&nbsp; [A2 · Membros herdados, acesso e palavra `super`](./A2%20-%20Membros%20herdados%20acesso%20e%20palavra%20super.md) ➡️

</div>
