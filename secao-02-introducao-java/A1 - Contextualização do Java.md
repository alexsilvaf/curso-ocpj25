# História e contextualização do Java

<sub>📚 [Documentação](../README.md) › [Seção 2 · Introdução à linguagem Java](./README.md) › Material 1 de 8</sub>

Java é, ao mesmo tempo, uma **linguagem de programação** e uma **plataforma de desenvolvimento e execução**.

Como linguagem, Java possui regras léxicas, sintáticas e semânticas. Como plataforma, oferece ferramentas, bibliotecas e um ambiente capaz de executar programas Java em diferentes sistemas.

Antes de estudar essas partes separadamente, vale compreender por que a tecnologia foi criada e como ela chegou até o Java atual.

## O problema que motivou o projeto

No início da década de 1990, a Sun Microsystems pesquisava maneiras de programar dispositivos eletrônicos de consumo. Esses equipamentos podiam usar processadores e sistemas diferentes, o que tornava caro reescrever o software para cada combinação de hardware.

As linguagens mais usadas naquele contexto, como C e C++, permitiam grande controle sobre a máquina, mas exigiam cuidados como gerenciamento manual de memória e adaptação do programa à plataforma de destino.

O novo projeto buscava uma linguagem que fosse:

- portável entre equipamentos diferentes;
- menos dependente do processador e do sistema operacional;
- mais segura no uso da memória;
- adequada a ambientes com recursos limitados;
- simples o bastante para reduzir erros comuns de programação.

## O projeto Green e James Gosling

O trabalho começou na **Sun Microsystems** dentro de uma iniciativa conhecida como **Green Project**. James Gosling foi o principal projetista da nova linguagem, em colaboração com outros engenheiros da Sun.

É comum resumir essa história dizendo que “James Gosling criou o Java”. A frase identifica corretamente seu papel central, mas Java não foi obra de uma pessoa isolada: a linguagem e a plataforma evoluíram com o trabalho de uma equipe.

## Antes de Java, Oak

A linguagem recebeu inicialmente o nome **Oak**. A especificação da linguagem Java registra que Oak foi projetada por James Gosling para sistemas eletrônicos embarcados de consumo.

Em 1992, o antecessor da Java Virtual Machine já era usado para executar programas escritos em Oak. A ideia essencial era separar o programa da máquina física: em vez de produzir uma versão totalmente diferente para cada equipamento, o código seria executado sobre um ambiente intermediário.

O mercado de dispositivos interativos ainda não estava pronto para o projeto como a Sun imaginava. Nos anos seguintes, a equipe percebeu que a mesma portabilidade fazia sentido para uma tecnologia que crescia rapidamente: a **World Wide Web**.

Oak foi então redirecionada para a Internet e recebeu o nome **Java**.

## A chegada pública do Java

Java foi apresentada publicamente em 1995. Naquele momento, páginas da Web começavam a deixar de ser apenas documentos estáticos, e a possibilidade de executar o mesmo programa em computadores diferentes chamou atenção.

Essa proposta ficou conhecida pela expressão:

> **Write once, run anywhere** — escreva uma vez, execute em qualquer lugar.

O programa Java não era compilado diretamente para um único processador. Ele era transformado em **bytecode**, que podia ser executado por uma **Java Virtual Machine**, ou JVM, disponível para cada plataforma.

O modelo completo será estudado no próximo material. Por enquanto, guarde esta ideia:

```text
código Java → bytecode → JVM do sistema → execução
```

A portabilidade não significa que todo programa funcionará magicamente em qualquer lugar. Ele ainda pode depender de arquivos, permissões, dispositivos ou bibliotecas específicas. A JVM, porém, cria uma base comum muito mais portátil do que compilar o programa apenas para uma máquina.

## Da Web às aplicações corporativas

Os pequenos programas executados em navegadores, chamados *applets*, ajudaram a divulgar Java, mas deixaram de ser o centro da plataforma.

Java se consolidou principalmente em:

- sistemas corporativos;
- aplicações executadas em servidores;
- ferramentas de desenvolvimento;
- sistemas financeiros e governamentais;
- dispositivos embarcados;
- aplicações móveis, especialmente durante os primeiros anos do Android.

O sucesso não dependeu apenas da linguagem. A biblioteca padrão, as ferramentas do JDK, a JVM e o ecossistema de empresas e desenvolvedores transformaram Java em uma plataforma.

## A crise da Sun e a mudança do mercado

A Sun cresceu vendendo servidores, estações de trabalho e software. Seu negócio foi pressionado por várias mudanças, e não por uma causa única.

Entre os fatores importantes estiveram:

- o fim da bolha das empresas ponto-com, que reduziu investimentos em infraestrutura;
- a expansão de servidores mais baratos baseados na arquitetura x86;
- o crescimento de Linux e de software de código aberto nesses servidores;
- a concorrência e a mudança na economia do mercado de hardware;
- dificuldades financeiras acumuladas pela própria Sun.

Portanto, dizer apenas que “a Sun entrou em crise por causa do Linux” é incompleto. Linux participou de uma transformação maior: empresas passaram a considerar servidores padronizados e mais baratos em vez de depender exclusivamente de máquinas proprietárias. A própria Sun passou a oferecer produtos compatíveis com Linux e com processadores x86.

## A compra pela Oracle

Em abril de 2009, a Oracle anunciou o acordo para adquirir a Sun Microsystems. No anúncio, a Oracle destacou Java e Solaris como ativos estratégicos.

A aquisição foi concluída em janeiro de 2010. A partir dela, a Oracle assumiu a condução da plataforma Java. Isso não significa que Java tenha se tornado um projeto desenvolvido apenas internamente pela Oracle: a tecnologia também evolui por meio do OpenJDK, do Java Community Process e da participação de outras empresas e da comunidade.

## Linha do tempo resumida

| Período | Marco |
| --- | --- |
| início dos anos 1990 | a Sun inicia o Green Project para pesquisar software portátil para dispositivos |
| 1992 | o antecessor da JVM executa programas da linguagem Oak |
| anos seguintes | o projeto é redirecionado dos dispositivos de consumo para a Internet; Oak passa a se chamar Java |
| 1995 | Java é apresentada publicamente |
| fim dos anos 1990 e anos 2000 | a plataforma cresce em servidores, sistemas corporativos, dispositivos e ferramentas |
| abril de 2009 | a Oracle anuncia o acordo para adquirir a Sun Microsystems |
| janeiro de 2010 | a aquisição é concluída e a Oracle assume a condução da plataforma |
| atualmente | Java continua evoluindo com versões regulares, participação do OpenJDK e um amplo ecossistema |

## Linguagem e plataforma

Agora é possível separar os dois usos da palavra Java:

| Java como linguagem | Java como plataforma |
| --- | --- |
| palavras, símbolos e regras para escrever programas | JVM, bibliotecas e ferramentas para desenvolver e executar programas |
| define o que o código significa | oferece o ambiente no qual o código funciona |
| será praticada ao longo de todo o curso | será detalhada nos próximos materiais desta seção |

## Edições da plataforma

Historicamente, a plataforma foi organizada em edições voltadas a necessidades diferentes:

- **Java SE — Java Platform, Standard Edition:** base da linguagem, da JVM e das principais bibliotecas; é a edição estudada neste curso;
- **Java ME — Java Platform, Micro Edition:** voltada a dispositivos com recursos limitados e sistemas embarcados;
- **Java EE — Java Platform, Enterprise Edition:** conjunto de especificações para aplicações corporativas; foi transferido para a Eclipse Foundation e hoje se chama **Jakarta EE**.

Essas edições não representam três linguagens diferentes. Todas partem de Java, mas reúnem APIs e ambientes destinados a contextos distintos.

## O que levar para o próximo material

1. Java nasceu na Sun Microsystems e teve James Gosling como seu principal projetista.
2. A linguagem se chamava Oak e buscava portabilidade para dispositivos diferentes.
3. O projeto foi redirecionado para a Web e apresentado como Java em 1995.
4. Bytecode e JVM ajudam a separar o programa da máquina em que ele será executado.
5. A crise da Sun teve várias causas; a mudança para servidores x86 e Linux foi parte desse contexto.
6. A Oracle anunciou a compra da Sun em 2009 e concluiu a aquisição em 2010.

## Referências históricas

- [Prefácio histórico da Java Language Specification](https://docs.oracle.com/javase/specs/jls/se6/html/j.preface.html)
- [Prefácio histórico da Java Virtual Machine Specification](https://docs.oracle.com/javase/specs/jvms/se7/html/jvms-0-preface1.html)
- [Oracle anuncia o acordo para adquirir a Sun](https://www.oracle.com/corporate/pressrelease/oracle-buys-sun-042009.html)
- [Perguntas e respostas sobre a aquisição da Sun pela Oracle](https://www.oracle.com/ocom/groups/public/%40ocom/documents/webcontent/042646.pdf)
- [Relatório anual da Sun Microsystems de 2009](https://www.sec.gov/Archives/edgar/data/709519/000119312509183962/d10k.htm)

---

<div align="center">

📂 [Seção 2](./README.md) &nbsp;·&nbsp; [A2 · Plataforma Java SE](./A2%20-%20Plataforma%20Java%20SE.md) ➡️

</div>
