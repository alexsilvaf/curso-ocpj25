# Polimorfismo, upcasting e despacho dinâmico

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Material 6 de 8</sub>

Polimorfismo permite usar uma referência de um tipo mais geral para trabalhar com objetos de diferentes subclasses. O código chama uma operação comum, e cada objeto executa sua implementação sobrescrita.

## Tipo da referência e tipo do objeto

```java
Employee employee = new Manager("Ana", 8_000.0, 2_000.0);
```

Existem dois tipos importantes:

- tipo da referência: `Employee`, escrito à esquerda;
- tipo real do objeto: `Manager`, criado com `new`.

O objeto não deixa de ser um `Manager`. A referência oferece a visão de `Employee` sobre ele.

## Upcasting

Converter uma referência de subclasse para superclasse é um upcasting:

```java
Manager manager = new Manager("Ana", 8_000.0, 2_000.0);
Employee employee = manager;
```

O cast explícito não é necessário porque todo `Manager` é um `Employee`.

```text
Manager  ---> Employee ---> Object
           upcasting
```

O upcasting não cria outro objeto e não remove a parte específica do objeto. Ele apenas muda o tipo pelo qual a referência é usada.

## O compilador observa a referência

Uma chamada só é aceita se o tipo da referência declarar ou herdar o método:

```java
Employee employee = new Manager("Ana", 8_000.0, 2_000.0);

employee.getName(); // método disponível em Employee
employee.payment(); // método disponível em Employee
// employee.getBonus(); // não compila: Employee não declara esse método
```

Mesmo sabendo que o objeto é `Manager` nessa linha, o compilador protege o código para qualquer objeto que uma variável `Employee` poderia receber.

## O objeto escolhe a implementação sobrescrita

Depois que a chamada é aceita, o método de instância sobrescrito é escolhido pelo tipo real do objeto durante a execução:

```java
class Employee {
    public String role() {
        return "Employee";
    }
}

class Manager extends Employee {
    @Override
    public String role() {
        return "Manager";
    }
}

Employee employee = new Manager();
System.out.println(employee.role()); // Manager
```

Esse mecanismo é o despacho dinâmico.

## Polimorfismo com arrays

Uma referência de superclasse pode apontar para qualquer objeto de suas subclasses. Assim, um array de superclasse pode reuni-los:

```java
Employee[] employees = new Employee[3];

employees[0] = new Employee("Caio", 3_000.0);
employees[1] = new Manager("Ana", 8_000.0, 2_000.0);
employees[2] = new Manager("Bia", 7_000.0, 1_500.0);
```

Um único laço processa todos os objetos:

```java
double total = 0.0;

for (Employee employee : employees) {
    total += employee.payment();
}

System.out.println(total);
```

Quando o elemento é um `Manager`, sua implementação de `payment()` é executada. O laço não precisa decidir manualmente qual fórmula usar.

## Parâmetros polimórficos

O mesmo princípio vale para parâmetros:

```java
static void printPayment(Employee employee) {
    System.out.println(employee.payment());
}

printPayment(new Employee("Caio", 3_000.0));
printPayment(new Manager("Ana", 8_000.0, 2_000.0));
```

O método recebe qualquer objeto que seja um `Employee`.

## Sobrecarga não usa despacho dinâmico

Na sobrecarga, o compilador escolhe a assinatura a partir dos tipos conhecidos na chamada:

```java
static void show(Employee employee) {
    System.out.println("employee parameter");
}

static void show(Manager manager) {
    System.out.println("manager parameter");
}

Employee reference = new Manager();
show(reference); // employee parameter
```

O tipo da variável é `Employee`, portanto `show(Employee)` é selecionado. Dentro de um método de instância sobrescrito, por outro lado, o objeto decide a implementação.

## Arrays também são covariantes

Como `Manager` é `Employee`, Java permite este upcasting de array:

```java
Manager[] managers = new Manager[2];
Employee[] employees = managers;
```

O objeto real ainda é um `Manager[]`. Por isso, esta atribuição de elemento compila, mas falha durante a execução:

```java
employees[0] = new Employee("Caio", 3_000.0);
```

O nome da falha é `ArrayStoreException`: um array criado para `Manager` não pode guardar um `Employee` que não seja gerente. O tratamento desse tipo de situação será estudado com exceções na Seção 12.

## Benefício principal

Sem polimorfismo, o programa precisaria perguntar repetidamente qual é a classe do objeto e duplicar decisões. Com ele, a superclasse define a operação comum e as subclasses fornecem comportamentos específicos.

## Exercícios de fixação

1. Identifique o tipo da referência e o tipo do objeto em `Account account = new SavingsAccount();`.
2. Por que o upcasting não exige cast explícito?
3. Por que uma referência `Employee` não chama diretamente um método existente apenas em `Manager`?
4. Explique como um array `Employee[]` pode calcular pagamentos de subclasses diferentes.
5. Compare a seleção de uma sobrecarga com o despacho de um método sobrescrito.

---

<div align="center">

⬅️ [A5 · Ocultação, `final` e tipos de membros](./A5%20-%20Ocultacao%20final%20e%20tipos%20de%20membros.md) &nbsp;·&nbsp; 📂 [Seção 10](./README.md) &nbsp;·&nbsp; [A7 · Downcasting, `instanceof` e prática integrada](./A7%20-%20Downcasting%20instanceof%20e%20pratica%20integrada.md) ➡️

</div>
