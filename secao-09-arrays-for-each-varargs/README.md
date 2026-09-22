# Seção 9 — Arrays, `for-each`, `var` e varargs

<sub>📚 [Documentação](../README.md) › Seção 9</sub>

| 🎓 Aulas do curso | 🎬 Aulas de referência |
| :---: | :---: |
| continuação | a definir |

## 🎯 Objetivos

Ao final desta seção, o aluno deverá ser capaz de:

- declarar, criar e inicializar arrays de tipos primitivos e de referências;
- acessar posições com segurança e distinguir `length` de outros usos dessa palavra;
- explicar valores padrão, referências compartilhadas e arrays de objetos;
- escolher entre `for` tradicional e `for-each` conforme a necessidade de índices;
- criar e percorrer arrays multidimensionais regulares e irregulares;
- controlar laços aninhados com `break`, `continue` e rótulos;
- usar `Arrays` para exibir, ordenar, buscar, comparar, preencher e copiar;
- aplicar inferência de tipo local com `var` e reconhecer suas restrições;
- declarar e chamar métodos com varargs;
- integrar arrays com `split`, `toCharArray` e variáveis sem nome.

## 📚 Conteúdos

- **A1** · [Introdução aos arrays](./A1%20-%20Introducao%20aos%20arrays.md)
- **A2** · [Valores padrão, referências e arrays de objetos](./A2%20-%20Valores%20padrao%20referencias%20e%20arrays%20de%20objetos.md)
- **A3** · [Percorrendo arrays com `for` e `for-each`](./A3%20-%20Percorrendo%20arrays%20com%20for%20e%20for-each.md)
- **A4** · [Arrays multidimensionais e laços rotulados](./A4%20-%20Arrays%20multidimensionais%20e%20lacos%20rotulados.md)
- **A5** · [Classe `Arrays`: ordenação, busca e cópia](./A5%20-%20Classe%20Arrays%20ordenacao%20busca%20e%20copia.md)
- **A6** · [Inferência local com `var` e variáveis sem nome](./A6%20-%20Inferencia%20local%20com%20var%20e%20variaveis%20sem%20nome.md)
- **A7** · [Varargs, `split`, `toCharArray` e prática integrada](./A7%20-%20Varargs%20split%20toCharArray%20e%20pratica%20integrada.md)
- **A8** · [A certificação OCP Java SE 25 e esta seção](./A8%20-%20A%20certificacao%20OCP%20Java%20SE%2025.md)
- **Prática** · [Lista de exercícios](./lista-de-exercicios.md)

## 🗓️ Planejamento das aulas

| Aula | Tema | Atividade ou recurso | Observações |
| ---: | --- | --- | --- |
| 1 | Primeiros arrays | Armazenar e consultar notas por índice | Começar com `int[]`; ainda sem `Arrays` ou `for-each` |
| 2 | Valores e referências | Comparar arrays de primitivos, textos e produtos | Retomar stack, heap, `null` e aliasing da Seção 7 |
| 3 | Percurso | Calcular soma, média e busca com `for` e `for-each` | Mostrar por que `for-each` não substitui posições |
| 4 | Mais dimensões | Montar tabelas regulares e linhas de tamanhos diferentes | Introduzir rótulos somente depois dos laços aninhados |
| 5 | `Arrays` | Ordenar, buscar, comparar, preencher e copiar | Exigir ordenação antes de `binarySearch` |
| 6 | `var` e `_` | Inferir tipos locais e descartar valores não utilizados | `var` não é tipo dinâmico; `_` não pode ser lido |
| 7 | Varargs e texto | Criar um boletim com quantidade variável de notas | Retomar métodos, `split` e `toCharArray` sem collections |
| 8 | Revisão e OCPJ25 | Resolver questões de compilação, execução e saída | Consolidar sintaxes parecidas e casos com `null` |

## 📝 Observações

- A seção usa apenas tipos básicos, textos, laços, métodos e objetos ensinados nas Seções 1 a 8.
- Arrays vêm antes de collections porque tornam visíveis tamanho fixo, índices, valores padrão e compartilhamento de referências.
- Varargs aparece somente depois dos fundamentos de arrays porque, dentro do método, o parâmetro é tratado como um array.
- Não são usados generics, lambdas, streams nem collections; esses assuntos têm seções próprias.
- `ArrayIndexOutOfBoundsException` e `NullPointerException` são observadas como resultados de execução. A hierarquia e o tratamento de exceções serão ensinados na Seção 12.
- A referência detalhada para aprofundamento é o [capítulo 6 do OCPJ21](../ocpj21-book/ch06.md#arrays); o uso de `for-each` e rótulos também aparece no [capítulo 5](../ocpj21-book/ch05.md#the-for-each-loop).
- A cobertura global da certificação é acompanhada em [Cobertura OCP Java SE 25](../README.md#cobertura-ocpj25).

---

<div align="center">

⬅️ [Seção 8 · Construtores e encapsulamento](../secao-08-construtores-this-sobrecarga-encapsulamento/README.md) &nbsp;·&nbsp; 📚 [Documentação](../README.md) &nbsp;·&nbsp; [Seção 10 · Herança e polimorfismo](../secao-10-heranca-sobrescrita-polimorfismo/README.md) ➡️

</div>
