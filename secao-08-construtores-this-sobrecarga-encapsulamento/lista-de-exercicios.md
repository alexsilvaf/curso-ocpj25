# Lista de exercícios — Seção 8

<sub>📚 [Documentação](../README.md) › [Seção 8 · Construtores, `this`, sobrecarga e encapsulamento](./README.md) › Lista de exercícios</sub>

## Leitura e previsão

1. Explique quando Java fornece um construtor padrão e quando ele deixa de existir.
2. Diferencie assinatura de método, sobrecarga e sobrescrita; a sobrescrita será aprofundada depois.
3. Explique dois usos de `this`: referência ao objeto atual e chamada de outro construtor.
4. Verifique quais pares de métodos podem formar sobrecarga e justifique pelas listas de parâmetros.
5. Preveja a ordem de inicialização de campos, blocos de instância e construtor em um exemplo simples.
6. Explique por que campos devem ser privados e por que nem todo campo precisa de setter.

## Construção

7. Crie uma classe `Student` cujo construtor exija nome e matrícula.
8. Sobrecarregue o construtor para permitir a criação com uma nota inicial opcional e use `this(...)`.
9. Garanta que nome vazio e nota fora do intervalo não alterem o estado para um valor inválido.
10. Crie getters necessários e evite setters que não façam sentido.
11. Na conta bancária do A7, acrescente um método privado que normalize o titular com `strip()`.
12. Explique por que o construtor da conta reutiliza `deposit` para validar o depósito inicial.
13. Preveja o saldo depois de depósito de `200.00` e saque de `50.00` em uma conta que começou zerada.

---

<div align="center">

⬅️ [Seção 7](../secao-07-introducao-poo/README.md) &nbsp;·&nbsp; 📂 [Seção 8](./README.md) &nbsp;·&nbsp; [Seção 9](../secao-09-arrays-for-each-varargs/README.md) ➡️

</div>
