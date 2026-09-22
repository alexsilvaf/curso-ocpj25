# Sobrescrita de métodos

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Material 4 de 8</sub>

Uma subclasse pode fornecer uma implementação mais específica para um método de instância herdado. Essa operação é chamada de sobrescrita (*overriding*).

## Primeira sobrescrita

```java
class Employee {
    private double baseSalary;

    Employee(double baseSalary) {
        this.baseSalary = baseSalary;
    }

    public double payment() {
        return baseSalary;
    }
}

class Manager extends Employee {
    private double bonus;

    Manager(double baseSalary, double bonus) {
        super(baseSalary);
        this.bonus = bonus;
    }

    @Override
    public double payment() {
        return super.payment() + bonus;
    }
}
```

`Manager.payment()` mantém o contrato básico e acrescenta o bônus. `super.payment()` reutiliza a implementação da superclasse.

## Por que usar `@Override`

`@Override` informa ao compilador que o método deve sobrescrever outro. Se houver um erro no nome ou nos parâmetros, a compilação falha em vez de criar acidentalmente outro método.

```java
class Manager extends Employee {
    @Override
    public double payments() { // não sobrescreve payment
        return 0.0;
    }
}
```

Sem a anotação, `payments()` seria apenas um método novo. Com ela, o erro é detectado.

## Mesma assinatura

Para sobrescrever, o nome e a lista de tipos dos parâmetros precisam corresponder:

```java
class Parent {
    void print(int value) { }
}

class Child extends Parent {
    @Override
    void print(int value) { }

    void print(long value) { } // sobrecarga, não sobrescrita
}
```

O nome do parâmetro pode mudar, pois não faz parte da assinatura:

```java
class Child extends Parent {
    @Override
    void print(int number) { }
}
```

## Retorno compatível

Para tipos primitivos, o retorno deve ser o mesmo:

```java
class Parent {
    double value() { return 1.0; }
}

class Child extends Parent {
    @Override
    double value() { return 2.0; }
}
```

Uma conversão numérica não basta:

```java
// @Override int value() { return 2; } // não compila
```

Para tipos de referência, a sobrescrita pode devolver um subtipo. Isso é um retorno covariante:

```java
class Employee {
    Employee copy() {
        return new Employee();
    }
}

class Manager extends Employee {
    @Override
    Manager copy() {
        return new Manager();
    }
}
```

`Manager` é um subtipo de `Employee`, então o retorno é mais específico e continua compatível.

## Acesso não pode ser reduzido

Uma sobrescrita pode manter ou ampliar a visibilidade, mas não pode restringi-la:

```java
class Parent {
    protected void execute() { }
}

class Child extends Parent {
    @Override
    public void execute() { }
}
```

Transformar `protected` em `public` é permitido. O contrário não é:

```java
class Parent {
    public void execute() { }
}

class Child extends Parent {
    // @Override protected void execute() { } // não compila
}
```

O código que já podia usar o método público da superclasse não pode perder esse acesso ao receber um objeto da subclasse.

## Sobrescrita e sobrecarga

| Sobrescrita | Sobrecarga |
| --- | --- |
| ocorre entre método herdado e método da subclasse | pode ocorrer na mesma classe ou na hierarquia |
| mantém a assinatura | altera a lista de parâmetros |
| especializa o comportamento | oferece outras formas de chamada |
| participa do despacho dinâmico | é resolvida a partir dos tipos disponíveis na compilação |

Uma classe pode fazer as duas coisas ao mesmo tempo:

```java
class Child extends Parent {
    @Override
    void print(int value) { }

    void print(String value) { }
}
```

## Exceções ficam para a seção apropriada

Sobrescritas também possuem regras para exceções declaradas. Elas serão estudadas na Seção 12, depois que a diferença entre checked e unchecked exceptions estiver estabelecida.

## Exercícios de fixação

1. Por que `@Override` ajuda a encontrar erros?
2. `run(int)` sobrescreve `run(long)`? Justifique.
3. Uma sobrescrita pode transformar um método `protected` em `public`?
4. Explique retorno covariante usando `Employee` e `Manager`.
5. Classifique como sobrecarga ou sobrescrita: a superclasse declara `show(int)` e a subclasse declara `show(String)`.

---

<div align="center">

⬅️ [A3 · Construtores em hierarquias e ordem de inicialização](./A3%20-%20Construtores%20em%20hierarquias%20e%20ordem%20de%20inicializacao.md) &nbsp;·&nbsp; 📂 [Seção 10](./README.md) &nbsp;·&nbsp; [A5 · Ocultação, `final` e tipos de membros](./A5%20-%20Ocultacao%20final%20e%20tipos%20de%20membros.md) ➡️

</div>
