# Downcasting, `instanceof` e prática integrada

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Material 7 de 8</sub>

Uma referência de superclasse oferece apenas os membros conhecidos nesse tipo. Quando o programa realmente precisa de uma operação específica da subclasse, pode verificar o objeto e realizar um downcasting.

## Downcasting

```java
Employee employee = new Manager("Ana", 8_000.0, 2_000.0);
Manager manager = (Manager) employee;

System.out.println(manager.getBonus());
```

A conversão de `Employee` para `Manager` precisa ser explícita porque nem todo empregado é gerente.

O cast não transforma o objeto. Ele afirma que a referência aponta para um objeto compatível com `Manager`.

## Cast que falha durante a execução

```java
Employee employee = new Employee("Caio", 3_000.0);
Manager manager = (Manager) employee;
```

O compilador permite o cast porque os tipos pertencem à mesma hierarquia. Durante a execução, porém, o objeto é apenas `Employee`. A conversão falha com `ClassCastException`.

Não é necessário tratar essa exceção neste momento; o importante é compreender que um cast pode compilar e ainda assim ser inválido para o objeto real.

## Testando com `instanceof`

```java
if (employee instanceof Manager) {
    Manager manager = (Manager) employee;
    System.out.println(manager.getBonus());
}
```

`instanceof` devolve `true` quando o objeto é compatível com o tipo indicado. Ele considera a hierarquia completa:

```java
Manager manager = new Manager("Ana", 8_000.0, 2_000.0);

System.out.println(manager instanceof Manager);  // true
System.out.println(manager instanceof Employee); // true
System.out.println(manager instanceof Object);   // true
```

Uma referência nula nunca representa uma instância:

```java
Employee employee = null;
System.out.println(employee instanceof Manager); // false
```

## Pattern matching com `instanceof`

Java pode combinar teste e declaração da referência específica:

```java
if (employee instanceof Manager manager) {
    System.out.println(manager.getBonus());
}
```

`manager` é uma variável de padrão. Ela só existe onde o fluxo garante que o teste foi verdadeiro.

É possível usar a variável à direita de `&&`:

```java
if (employee instanceof Manager manager && manager.getBonus() > 0.0) {
    System.out.println("Manager with bonus");
}
```

Se o primeiro teste for falso, o segundo operando não executa. Portanto, o uso é seguro.

Este caso não compila:

```java
// if (employee instanceof Manager manager || manager.getBonus() > 0.0) { }
```

Com `||`, a expressão da direita pode ser executada justamente quando o padrão falhou.

## Escopo depois de uma saída antecipada

O compilador acompanha o fluxo:

```java
static void printBonus(Employee employee) {
    if (!(employee instanceof Manager manager)) {
        return;
    }

    System.out.println(manager.getBonus());
}
```

Depois do `if`, só é possível continuar quando o objeto era um `Manager`; por isso, a variável permanece disponível.

## Evite casting desnecessário

Se a operação existe na superclasse e é sobrescrita, chame-a pela referência geral:

```java
Employee employee = new Manager("Ana", 8_000.0, 2_000.0);
System.out.println(employee.payment());
```

Não faça downcasting apenas para obter o despacho dinâmico. O cast é necessário somente para membros específicos da subclasse.

## Prática integrada: folha de pagamento

### Superclasse

```java
public class Employee {
    private String name;
    private double baseSalary;

    public Employee(String name, double baseSalary) {
        this.name = name;
        this.baseSalary = baseSalary;
    }

    public String getName() {
        return name;
    }

    protected double getBaseSalary() {
        return baseSalary;
    }

    public double payment() {
        return baseSalary;
    }
}
```

### Subclasse

```java
public class Manager extends Employee {
    private double bonus;

    public Manager(String name, double baseSalary, double bonus) {
        super(name, baseSalary);
        this.bonus = bonus;
    }

    public double getBonus() {
        return bonus;
    }

    @Override
    public double payment() {
        return getBaseSalary() + bonus;
    }
}
```

### Programa

```java
public class Program {
    public static void main(String[] args) {
        Employee[] employees = {
            new Employee("Caio", 3_000.0),
            new Manager("Ana", 8_000.0, 2_000.0),
            new Manager("Bia", 7_000.0, 1_500.0)
        };

        double total = 0.0;

        for (Employee employee : employees) {
            System.out.printf("%s: %.2f%n",
                    employee.getName(), employee.payment());
            total += employee.payment();

            if (employee instanceof Manager manager) {
                System.out.printf("  bonus: %.2f%n", manager.getBonus());
            }
        }

        System.out.printf("Total: %.2f%n", total);
    }
}
```

O cálculo de `payment()` usa polimorfismo. O pattern é reservado à informação que existe somente em `Manager`.

---

<div align="center">

⬅️ [A6 · Polimorfismo, upcasting e despacho dinâmico](./A6%20-%20Polimorfismo%20upcasting%20e%20despacho%20dinamico.md) &nbsp;·&nbsp; 📂 [Seção 10](./README.md) &nbsp;·&nbsp; [A8 · A certificação OCP Java SE 25 e esta seção](./A8%20-%20A%20certificacao%20OCP%20Java%20SE%2025.md) ➡️

</div>
