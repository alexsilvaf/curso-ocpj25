# Seção 10 — Herança, sobrescrita e polimorfismo

<sub>📚 [Documentação](../README.md) › Seção 10</sub>

| 🎓 Aulas do curso | 🎬 Aulas de referência | ⏱️ Duração na grade | 🖥️ Slides |
| :---: | :---: | :---: | :---: |
| continuação | a definir | a definir | — |

## 🎯 Objetivos

Ao final desta seção, o aluno deverá ser capaz de:

- modelar relações “é um” com `extends`;
- distinguir membros declarados, herdados e apenas acessíveis;
- aplicar as regras de acesso em uma hierarquia, inclusive para `protected`;
- usar `super` para acessar construtores e implementações da superclasse;
- acompanhar inicialização estática e construção de superclasses e subclasses;
- aplicar corpos flexíveis de construtores do Java 25 com `super(...)`;
- sobrescrever métodos respeitando assinatura, acesso e retorno covariante;
- diferenciar sobrescrita, sobrecarga, ocultação e acesso a campos;
- restringir extensão e sobrescrita com `final`;
- distinguir tipo da referência e tipo do objeto;
- explicar despacho dinâmico de métodos de instância;
- usar upcasting, downcasting e pattern matching com `instanceof`;
- processar objetos de subclasses diferentes por meio de uma superclasse comum.

## 📚 Conteúdos

- **A1** · [Herança e relação “é um”](./A1%20-%20Heranca%20e%20relacao%20e-um.md)
- **A2** · [Membros herdados, acesso e palavra `super`](./A2%20-%20Membros%20herdados%20acesso%20e%20palavra%20super.md)
- **A3** · [Construtores em hierarquias e ordem de inicialização](./A3%20-%20Construtores%20em%20hierarquias%20e%20ordem%20de%20inicializacao.md)
- **A4** · [Sobrescrita de métodos](./A4%20-%20Sobrescrita%20de%20metodos.md)
- **A5** · [Ocultação, `final` e tipos de membros](./A5%20-%20Ocultacao%20final%20e%20tipos%20de%20membros.md)
- **A6** · [Polimorfismo, upcasting e despacho dinâmico](./A6%20-%20Polimorfismo%20upcasting%20e%20despacho%20dinamico.md)
- **A7** · [Downcasting, `instanceof` e prática integrada](./A7%20-%20Downcasting%20instanceof%20e%20pratica%20integrada.md)
- **A8** · [A certificação OCP Java SE 25 e esta seção](./A8%20-%20A%20certificacao%20OCP%20Java%20SE%2025.md)

## 🗓️ Planejamento das aulas

| Aula | Tema | Atividade ou recurso | Observações |
| ---: | --- | --- | --- |
| 1 | Herança | Extrair características comuns de `Employee` e `Manager` | Validar a relação “é um”; ainda sem sobrescrita |
| 2 | Membros e acesso | Classificar o que é herdado, acessível ou privado | Retomar os modificadores da Seção 8 e introduzir `super.membro` |
| 3 | Construção | Rastrear inicialização de uma hierarquia | Retomar `this(...)` e completar corpos flexíveis com `super(...)` |
| 4 | Sobrescrita | Especializar cálculos e usar `@Override` | Comparar lado a lado com sobrecarga |
| 5 | Categorias de membros | Distinguir método de instância, `static`, campo e método `private` | Aplicar `final` somente depois das diferenças |
| 6 | Polimorfismo | Processar um array de empregados por uma referência comum | Separar tipo da referência de tipo do objeto |
| 7 | Casting e padrões | Implementar uma folha de pagamento simples | Fazer teste de tipo antes do downcasting |
| 8 | Revisão e OCPJ25 | Resolver questões de compilação, execução e saída | Consolidar construção, acesso e seleção de membros |

## 📝 Observações

- A seção depende dos objetos e referências da Seção 7, dos construtores e modificadores da Seção 8 e dos arrays da Seção 9.
- As primeiras aulas usam classes concretas. Classes abstratas e interfaces aparecem somente na Seção 11.
- A regra de exceções em sobrescritas será adicionada na Seção 12, depois que checked e unchecked exceptions forem ensinadas.
- Records e tipos selados serão integrados à herança na Seção 13.
- A referência detalhada para aprofundamento é o [capítulo 2 do OCPJ21](../ocpj21-book/ch02.md#inheritance).
- A cobertura global da certificação é acompanhada em [Cobertura OCP Java SE 25](../README.md#cobertura-ocpj25).

---

<div align="center">

⬅️ [Seção 9 · Arrays](../secao-09-arrays-for-each-varargs/README.md) &nbsp;·&nbsp; 📚 [Documentação](../README.md) &nbsp;·&nbsp; [Seção 11 · Abstração e interfaces](../secao-11-classes-abstratas-interfaces-object/README.md) ➡️

</div>
