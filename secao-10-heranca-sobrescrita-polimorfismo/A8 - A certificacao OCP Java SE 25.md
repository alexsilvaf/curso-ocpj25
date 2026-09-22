# A certificação OCP Java SE 25 e esta seção

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Material 8 de 8</sub>

Questões de herança na OCP Java SE 25 frequentemente combinam construção, acesso, sobrescrita e o contraste entre tipo da referência e tipo real do objeto. Analise cada categoria de membro separadamente antes de prever a saída.

## Pontos que precisam estar consolidados

- uma classe estende diretamente no máximo uma classe;
- uma classe sem `extends` explícito herda diretamente de `Object`;
- construtores não são herdados;
- `super(...)` invoca um construtor da superclasse direta;
- na ausência de `this(...)` ou `super(...)`, o compilador tenta inserir `super()`;
- a parte da superclasse é inicializada antes da parte da subclasse;
- blocos estáticos da superclasse executam antes dos da subclasse;
- no Java 25, um prólogo restrito pode aparecer antes de `this(...)` ou `super(...)`, inclusive para atribuir campos da própria classe, mas sem lê-los nem chamar métodos da instância;
- sobrescrita mantém a assinatura, não reduz o acesso e usa retorno compatível;
- retornos de referência podem ser covariantes;
- métodos de instância são sobrescritos; métodos estáticos e campos são ocultados;
- métodos `private` não são sobrescritos e métodos `final` não podem ser sobrescritos;
- o tipo da referência controla quais chamadas são aceitas;
- o tipo do objeto controla a implementação de método de instância sobrescrito;
- upcasting é implícito; downcasting é explícito e pode falhar durante a execução;
- `instanceof` com pattern matching testa e declara uma referência mais específica;
- `null instanceof Tipo` é sempre `false`.

## Estratégia para questões

1. Desenhe a hierarquia.
2. Verifique se os construtores conseguem alcançar um `super(...)` válido.
3. Acompanhe inicializadores e construtores da superclasse para a subclasse.
4. Confirme acesso, assinatura e retorno de cada método.
5. Classifique o membro: campo, método de instância, `static` ou `private`.
6. Separe o tipo da referência do tipo real do objeto.
7. Só então determine compilação, execução e saída.

## Questões de leitura de código

### 1. `super()` implícito

```java
class Parent {
    Parent(int value) { }
}

class Child extends Parent {
    Child() { }
}
```

Não compila. O construtor de `Child` tenta chamar `super()`, mas `Parent` só possui `Parent(int)`.

### 2. Ordem de construção

```java
class Parent {
    Parent() { System.out.print("P"); }
}

class Child extends Parent {
    Child() { System.out.print("C"); }
}

new Child();
```

A saída é `PC`.

### 3. Corpos flexíveis no Java 25

```java
class Parent {
    Parent(String text) { }
}

class Child extends Parent {
    Child(String text) {
        String normalized = text.strip();
        super(normalized);
    }
}
```

Compila no Java 25. A variável local é preparada antes da invocação explícita de construtor.

Também é permitido atribuir, sem ler, um campo declarado na própria classe antes de `super(...)`:

```java
class Child extends Parent {
    final int code;

    Child(String text, int code) {
        this.code = code;
        super(text);
    }
}
```

### 4. Acesso reduzido

```java
class Parent {
    public void run() { }
}

class Child extends Parent {
    // protected void run() { }
}
```

A declaração comentada não compila porque reduziria o acesso de `public` para `protected`.

### 5. Parâmetro diferente

```java
class Parent {
    void show(int value) { }
}

class Child extends Parent {
    void show(long value) { }
}
```

`Child.show(long)` sobrecarrega; não sobrescreve `show(int)`.

### 6. Retorno covariante

```java
class Parent {
    Parent create() { return new Parent(); }
}

class Child extends Parent {
    @Override
    Child create() { return new Child(); }
}
```

Compila porque `Child` é subtipo do retorno original `Parent`.

### 7. Despacho dinâmico

```java
class Parent {
    String name() { return "P"; }
}

class Child extends Parent {
    @Override String name() { return "C"; }
}

Parent value = new Child();
System.out.println(value.name());
```

Imprime `C`: o método de instância sobrescrito é escolhido pelo objeto.

### 8. Campo ocultado

```java
class Parent {
    String name = "P";
}

class Child extends Parent {
    String name = "C";
}

Parent value = new Child();
System.out.println(value.name);
```

Imprime `P`: o campo é selecionado pelo tipo da referência.

### 9. Método estático ocultado

```java
class Parent {
    static String type() { return "P"; }
}

class Child extends Parent {
    static String type() { return "C"; }
}

Parent value = new Child();
System.out.println(value.type());
```

Imprime `P`. A chamada por variável é permitida, mas o método estático é selecionado pelo tipo `Parent`.

### 10. Método privado

```java
class Parent {
    private void run() { }
}

class Child extends Parent {
    public void run() { }
}
```

Compila. `Child.run()` é um método novo, não uma sobrescrita.

### 11. Chamada aceita pela referência

```java
class Parent { }
class Child extends Parent {
    void play() { }
}

Parent value = new Child();
// value.play();
```

A chamada comentada não compila porque `Parent` não declara `play()`.

### 12. Downcasting válido

```java
Parent parent = new Child();
Child child = (Child) parent;
```

Compila e executa porque o objeto real é `Child`.

### 13. Downcasting inválido em execução

```java
Parent parent = new Parent();
Child child = (Child) parent;
```

Compila, mas lança `ClassCastException` durante a execução.

### 14. Pattern matching e fluxo

```java
static void execute(Parent value) {
    if (!(value instanceof Child child)) {
        return;
    }
    child.play();
}
```

Compila. Depois do `return`, o fluxo restante garante que o padrão correspondeu.

### 15. `null`

```java
Parent value = null;
System.out.println(value instanceof Child);
```

Imprime `false`; o teste não lança `NullPointerException`.

### 16. Sobrecarga e tipo da referência

```java
static void print(Parent value) { System.out.print("P"); }
static void print(Child value)  { System.out.print("C"); }

Parent value = new Child();
print(value);
```

Imprime `P`. A sobrecarga é resolvida usando o tipo da referência na compilação.

### 17. Array covariante

```java
Parent[] values = new Child[1];
values[0] = new Parent();
```

Compila, mas lança `ArrayStoreException`: o objeto real é um array que aceita apenas referências compatíveis com `Child`.

## Armadilhas frequentes

- afirmar que construtores são herdados;
- esquecer o `super()` inserido pelo compilador;
- iniciar pela subclasse ao rastrear a construção;
- confundir membro `protected` com membro público;
- reduzir acesso em uma sobrescrita;
- chamar sobrecarga de sobrescrita apenas porque o nome é igual;
- aplicar despacho dinâmico a campos e métodos estáticos;
- fazer cast para obter um comportamento que a sobrescrita já forneceria;
- assumir que um downcasting muda o objeto;
- usar uma variável de padrão fora de seu fluxo válido;
- esquecer que arrays preservam seu tipo real durante a execução.

## O que continua planejado

Esta seção estabelece a herança entre classes concretas. Ainda faltam:

- classes abstratas, interfaces, `Object`, `equals` e `hashCode`, na Seção 11;
- regras de checked exceptions em sobrescritas, na Seção 12;
- records, tipos selados e padrões mais avançados, na Seção 13;
- generics e suas diferenças em relação à covariância de arrays, na Seção 15.

## Referências

- [JLS 25 — Superclasses and Subclasses](https://docs.oracle.com/javase/specs/jls/se25/html/jls-8.html#jls-8.1.4).
- [JLS 25 — Overriding](https://docs.oracle.com/javase/specs/jls/se25/html/jls-8.html#jls-8.4.8.1).
- [JLS 25 — Casting Contexts](https://docs.oracle.com/javase/specs/jls/se25/html/jls-5.html#jls-5.5).
- [Java 25 Language Guide — Flexible Constructor Bodies](https://docs.oracle.com/en/java/javase/25/language/flexible-constructor-bodies.html).

---

<div align="center">

⬅️ [A7 · Downcasting, `instanceof` e prática integrada](./A7%20-%20Downcasting%20instanceof%20e%20pratica%20integrada.md) &nbsp;·&nbsp; 📂 [Seção 10](./README.md) &nbsp;·&nbsp; [Seção 11 · Classes abstratas, interfaces e `Object`](../secao-11-classes-abstratas-interfaces-object/README.md) ➡️

</div>
