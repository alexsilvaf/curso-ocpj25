# Seção 3 — Estrutura sequencial

<sub>📚 [Documentação](../README.md) › Seção 3</sub>

| 🎓 Aulas do curso | 🎬 Aulas de referência |
| :---: | :---: |
| 21 a 32 | 26 a 37 |

## 🎯 Objetivos

Ao final desta seção, o aluno deverá ser capaz de:

- declarar variáveis, escolher o tipo primitivo adequado e reconhecer os oito tipos primitivos;
- distinguir tipos primitivos de tipos por referência, reconhecendo `String` como o primeiro exemplo por referência;
- avaliar expressões aritméticas e prever o resultado da divisão inteira e da divisão real;
- usar o operador `%` e a precedência de operadores para traduzir fórmulas para código;
- identificar as três operações básicas — entrada, processamento e saída — em um programa sequencial;
- imprimir resultados com `print`, `println` e `printf`, controlando casas decimais e alinhamento;
- aplicar conversão implícita e casting explícito, e prever a promoção numérica em expressões;
- ler dados do teclado com `Scanner`, evitando as armadilhas de `nextLine` e de `Locale`;
- usar as funções da classe `Math` mais frequentes;
- fazer o teste de mesa de um programa sequencial antes de executá-lo.

## 🖥️ Apresentação

[apresentacao.html](./apresentacao.html) reúne os seis blocos da aula em slides, incluindo os diagramas desta seção. Basta abrir o arquivo no navegador; navegação por <kbd>←</kbd> <kbd>→</kbd> ou <kbd>Espaço</kbd>, <kbd>Esc</kbd> para a visão geral e <kbd>F</kbd> para tela cheia.

> [!NOTE]
> A imagem do Duke (`duke.svg`) é de autoria de sbmehta, obtida no Wikimedia Commons e distribuída sob **licença BSD** — o Duke foi liberado como código aberto pela Sun Microsystems em 2006.

## 📚 Conteúdos

- **A1** · [Variáveis e tipos básicos em Java](./A1%20-%20Variaveis%20e%20tipos%20basicos.md)
- **A2** · [Expressões aritméticas](./A2%20-%20Expressoes%20aritmeticas.md)
- **A3** · [As três operações básicas de programação](./A3%20-%20As%20tres%20operacoes%20basicas.md)
- **A4** · [Saída de dados em Java](./A4%20-%20Saida%20de%20dados%20em%20Java.md)
- **A5** · [Processamento de dados e casting](./A5%20-%20Processamento%20de%20dados%20e%20casting.md)
- **A6** · [Entrada de dados em Java](./A6%20-%20Entrada%20de%20dados%20em%20Java.md)
- **A7** · [Funções matemáticas em Java](./A7%20-%20Funcoes%20matematicas%20em%20Java.md)
- **A8** · [A certificação OCP Java SE 25 e esta seção](./A8%20-%20A%20certificacao%20OCP%20Java%20SE%2025.md)
- **Prática** · [Lista de exercícios](./lista-de-exercicios.md)

## 🧭 Percurso sugerido

| Conteúdo | Atividade sugerida |
| --- | --- |
| Variáveis e tipos básicos | Usar a tabela e o diagrama do A1; reproduzir os erros de literal (`long` sem `L`, `float` sem `f`) |
| Expressões aritméticas | Percorrer o A2 no `jshell` ou na IDE, comparando `10 / 3` com `10.0 / 3` e praticando os usos do `%` |
| As três operações básicas | Estudar o diagrama do A3 e fazer um teste de mesa |
| Saída de dados | Reproduzir os exemplos de `printf` do A4, incluindo a tabela alinhada e o `Locale.setDefault` |
| Processamento e casting | Testar o casting do A5 e a promoção numérica que impede `byte soma = a + b;` |
| Entrada de dados com `Scanner` | Codar o programa completo do A6, observar a falha do `nextLine` depois do `nextInt` e aplicar a correção |
| Funções matemáticas | Resolver o exercício da distância entre dois pontos do A7 |
| Revisão e exercícios | Retomar os erros comuns e resolver a lista de exercícios para iniciantes |

## 📝 Observações

- Cada um dos seis blocos da apresentação termina com um slide **Mão na massa**: cinco exercícios para o aluno fazer na IDE, na ordem em que o conteúdo foi apresentado. São exercícios de digitar e executar — vários pedem que o erro seja provocado de propósito antes da correção e também podem ser realizados como atividade independente.
- O `Locale` aparece duas vezes com efeitos opostos: na **saída** (`printf`) e na **entrada** (`Scanner`). Vale fixar uma convenção com a turma logo no começo — o curso usa `Locale.setDefault(Locale.US)` — para não misturar vírgula e ponto entre a leitura e a impressão.
- A falha do `nextLine()` depois de um `nextInt()` é a dúvida mais recorrente da seção. Provocar o erro ao vivo, antes de mostrar a correção, costuma fixar melhor do que apenas avisar.
- `var` e *text blocks* aparecem apenas para reconhecimento. Os exemplos principais continuam usando declarações explícitas e strings comuns.
- Operadores cumulativos, incremento, comparações e condições foram retirados desta seção e ficam concentrados na Seção 4.
- Arrays, separação de texto e validação condicional da entrada ficam para as seções em que esses recursos forem ensinados.
- A prática da seção está reunida em [lista-de-exercicios.md](./lista-de-exercicios.md) e pode ser complementada por atividades avaliativas na plataforma do curso.

---

<div align="center">

⬅️ [Seção 2 · Introdução à linguagem Java](../secao-02-introducao-java/README.md) &nbsp;·&nbsp; 📚 [Documentação](../README.md) &nbsp;·&nbsp; [Seção 4 · Estrutura condicional](../secao-04-estrutura-condicional/README.md) ➡️

</div>
