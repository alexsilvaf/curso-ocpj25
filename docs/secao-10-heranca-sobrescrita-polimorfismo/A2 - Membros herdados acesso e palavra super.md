# Membros herdados, acesso e palavra `super`

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Material 2 de 8</sub>

Uma subclasse recebe membros de sua superclasse, mas herança e acesso não são exatamente a mesma coisa. Os modificadores apresentados na Seção 8 determinam quais membros o código da subclasse pode mencionar diretamente.

## Campos privados e métodos públicos

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

Uma subclasse não acessa diretamente os campos privados:

```java
class Manager extends Employee {
    Manager(String name, double baseSalary) {
        super(name, baseSalary);
    }

    void printData() {
        // System.out.println(name); // não compila
        System.out.println(getName());
    }
}
```

O estado definido por `Employee` existe no objeto, mas continua encapsulado. A subclasse usa as operações que a superclasse disponibiliza.

## Visão geral do acesso

| Modificador | Mesma classe | Mesmo pacote | Subclasse em outro pacote | Código sem relação em outro pacote |
| --- | :---: | :---: | :---: | :---: |
| `public` | sim | sim | sim | sim |
| `protected` | sim | sim | sim, com regra própria | não |
| sem modificador | sim | sim | não | não |
| `private` | sim | não | não | não |

O acesso de pacote depende do pacote, e não da herança.

## Uso simples de `protected`

```java
class Employee {
    protected double baseSalary;
}

class Manager extends Employee {
    double annualBaseSalary() {
        return baseSalary * 12;
    }
}
```

O código de `Manager` pode acessar o membro protegido herdado. Mesmo assim, campos privados com métodos protegidos ou públicos costumam preservar melhor as regras da classe.

## `protected` entre pacotes

Em outro pacote, uma subclasse acessa o membro protegido por meio da herança, usando a instância atual ou uma referência cujo tipo permita essa relação:

```java
package company;

public class Employee {
    protected double baseSalary = 1_000.0;
}
```

```java
package management;

import company.Employee;

public class Manager extends Employee {
    void compare(Manager other, Employee employee) {
        System.out.println(baseSalary);       // compila
        System.out.println(this.baseSalary);  // compila
        System.out.println(other.baseSalary); // compila
        // System.out.println(employee.baseSalary); // não compila
    }
}
```

Fora do pacote de `Employee`, `protected` não equivale a `public`. Acesso por uma referência geral `Employee` não é permitido nesse código da subclasse.

## A palavra `super`

`this` representa a instância atual vista a partir da classe atual. `super` permite referir-se à parte herdada da instância.

Considere campos com o mesmo nome:

```java
class Parent {
    protected String label = "parent";
}

class Child extends Parent {
    private String label = "child";

    void show() {
        System.out.println(label);       // child
        System.out.println(this.label);  // child
        System.out.println(super.label); // parent
    }
}
```

A subclasse declarou outro campo; ela não substituiu o campo da superclasse. Essa ocultação será retomada na Aula 5.

## Chamando uma implementação da superclasse

Uma subclasse também pode invocar um método acessível da superclasse:

```java
class Employee {
    public String description() {
        return "Employee";
    }
}

class Manager extends Employee {
    public String completeDescription() {
        return super.description() + " - Manager";
    }
}
```

`super.description()` seleciona a implementação definida na superclasse. A especialização do próprio método `description` será estudada como sobrescrita na Aula 4.

## Limites de `super`

`super` não é uma variável que possa ser armazenada ou retornada:

```java
// Employee employee = super; // não compila
```

Ele é uma palavra especial usada no acesso a membros da superclasse e na invocação de seu construtor.

## Exercícios de fixação

1. Por que uma subclasse não deve acessar diretamente um campo `private`?
2. Diferencie acesso de pacote e `protected`.
3. Em uma subclasse, o que `super.value` seleciona quando a subclasse também declara `value`?
4. Explique por que `protected` não significa “público para qualquer objeto quando existe herança”.
5. Reescreva uma subclasse que tenta usar `name` privado para que ela utilize `getName()`.

---

<div align="center">

⬅️ [A1 · Herança e relação “é um”](./A1%20-%20Heranca%20e%20relacao%20e-um.md) &nbsp;·&nbsp; 📂 [Seção 10](./README.md) &nbsp;·&nbsp; [A3 · Construtores em hierarquias e ordem de inicialização](./A3%20-%20Construtores%20em%20hierarquias%20e%20ordem%20de%20inicializacao.md) ➡️

</div>
