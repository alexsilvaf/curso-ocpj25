# Ocultação, `final` e tipos de membros

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Material 5 de 8</sub>

Nem todo membro declarado novamente em uma subclasse é sobrescrito. O comportamento depende de ser método de instância, método estático, campo ou método privado.

## Métodos de instância são sobrescritos

```java
class Parent {
    String identify() {
        return "parent";
    }
}

class Child extends Parent {
    @Override
    String identify() {
        return "child";
    }
}
```

Essa é a sobrescrita ensinada na aula anterior.

## Métodos estáticos são ocultados

Um método `static` pertence à classe. Se uma subclasse declara outro método estático com assinatura correspondente, ocorre ocultação, não sobrescrita:

```java
class Parent {
    static String category() {
        return "parent";
    }
}

class Child extends Parent {
    static String category() {
        return "child";
    }
}
```

`@Override` não pode ser usado nessa declaração. A classe ou o tipo da referência determina qual método estático é selecionado:

```java
Parent reference = new Child();

System.out.println(Parent.category());    // parent
System.out.println(Child.category());     // child
System.out.println(reference.category()); // parent
```

Embora Java permita a chamada por uma variável, prefira `Parent.category()` para deixar explícito que o membro é da classe.

Uma subclasse não pode trocar um método de instância por `static`, nem o contrário:

```java
class Parent {
    void run() { }
}

class Child extends Parent {
    // static void run() { } // não compila
}
```

## Campos também são ocultados

Campos não participam do despacho dinâmico:

```java
class Parent {
    String label = "parent";
}

class Child extends Parent {
    String label = "child";
}

Parent reference = new Child();

System.out.println(reference.label); // parent
System.out.println(((Child) reference).label); // child
```

Os dois campos existem no objeto. O tipo usado na expressão determina qual campo é acessado.

## Métodos privados não são sobrescritos

Um método `private` só é acessível dentro da classe que o declarou. Uma subclasse pode declarar um método com a mesma assinatura, mas ele é um método independente:

```java
class Parent {
    private void secret() { }
}

class Child extends Parent {
    void secret() { } // método novo
}
```

Não se usa `@Override`, pois o método privado da superclasse não está acessível para ser sobrescrito.

## Métodos `final`

Um método de instância `final` pode ser herdado, mas não sobrescrito:

```java
class Employee {
    public final String companyId() {
        return "ACME";
    }
}

class Manager extends Employee {
    // public String companyId() { return "OTHER"; } // não compila
}
```

Ele pode continuar sendo chamado normalmente em um objeto `Manager`.

## Classes `final`

Uma classe `final` não pode ser estendida:

```java
final class Utility { }

// class SpecialUtility extends Utility { } // não compila
```

Isso encerra aquela linha da hierarquia. `String`, por exemplo, é uma classe `final`.

Classes seladas fornecerão outro tipo de controle sobre subclasses na Seção 13.

## Variáveis e referências `final`

`final` em uma variável impede a reatribuição, não torna o objeto imutável:

```java
final Employee employee = new Employee();

// employee = new Employee(); // não compila
employee.setName("Ana");      // pode compilar se o método existir
```

Compare os significados:

- classe `final`: não admite subclasses;
- método `final`: não admite sobrescrita;
- variável `final`: recebe valor uma vez.

Construtores não podem ser `final`, pois não são herdados nem sobrescritos.

## Quadro de decisão

| Membro na superclasse | Declaração correspondente na subclasse | Seleção principal |
| --- | --- | --- |
| método de instância acessível | sobrescrita | objeto em tempo de execução |
| método `static` acessível | ocultação | classe ou tipo da referência |
| campo acessível | ocultação | tipo da expressão de acesso |
| método `private` | método novo, sem relação de sobrescrita | cada classe acessa o próprio |
| método `final` | nova declaração correspondente é proibida | implementação herdada |

## Exercícios de fixação

1. Por que um método `static` não pode usar `@Override`?
2. Preveja o campo acessado por `Parent p = new Child(); p.value`.
3. Uma subclasse pode declarar um método com a mesma assinatura de um método `private` da superclasse?
4. Diferencie classe, método e referência `final`.
5. Por que um construtor não pode ser `final`?

---

<div align="center">

⬅️ [A4 · Sobrescrita de métodos](./A4%20-%20Sobrescrita%20de%20metodos.md) &nbsp;·&nbsp; 📂 [Seção 10](./README.md) &nbsp;·&nbsp; [A6 · Polimorfismo, upcasting e despacho dinâmico](./A6%20-%20Polimorfismo%20upcasting%20e%20despacho%20dinamico.md) ➡️

</div>
