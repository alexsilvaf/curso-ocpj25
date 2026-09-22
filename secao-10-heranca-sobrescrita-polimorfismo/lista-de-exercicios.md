# Lista de exercícios — Seção 10

<sub>📚 [Documentação](../README.md) › [Seção 10 · Herança, sobrescrita e polimorfismo](./README.md) › Lista de exercícios</sub>

## Hierarquias e execução

1. Modele uma relação “é um” adequada e outra relação que não deveria usar herança; justifique.
2. Classifique membros como declarados, herdados, acessíveis ou inacessíveis em uma hierarquia simples.
3. Preveja a ordem de inicialização de superclasse e subclasse.
4. Use `super(...)` para inicializar a parte herdada de um objeto.
5. Identifique quais métodos realmente sobrescrevem e quais apenas formam sobrecarga ou ocultação.
6. Verifique regras de acesso e retorno em três tentativas de sobrescrita.
7. Explique a diferença entre tipo da referência e tipo do objeto.
8. Preveja qual implementação será chamada por despacho dinâmico.
9. Mostre um downcasting seguro e um que compila, mas falha durante a execução.
10. Reescreva uma verificação seguida de cast usando pattern matching com `instanceof`.

## Prática integrada

11. Crie `Salesperson extends Employee` com um campo `commission` e sobrescreva `payment()`.
12. Acrescente vendedores ao array do A7 sem alterar o laço que calcula o total.
13. Exiba a comissão apenas para `Salesperson`, usando pattern matching.
14. Explique por que testar cada subtipo com `if` para calcular o pagamento seria pior do que usar sobrescrita.
15. Marque como `final` um membro que não deve ser alterado ou sobrescrito e justifique a escolha.

---

<div align="center">

⬅️ [Seção 9](../secao-09-arrays-for-each-varargs/README.md) &nbsp;·&nbsp; 📂 [Seção 10](./README.md) &nbsp;·&nbsp; [Seção 11](../secao-11-classes-abstratas-interfaces-object/README.md) ➡️

</div>
