# Sistema-biblioteca
## Introdução

A gestão de acervos bibliográficos representa um desafio crescente para instituições de ensino e bibliotecas públicas, especialmente diante do aumento do volume de títulos, usuários e demandas por processos ágeis e rastreáveis. Sistemas manuais ou pouco integrados geram gargalos no controle de empréstimos, devoluções e reservas, além de dificultar a geração de relatórios gerenciais. O presente projeto propõe a modelagem de um **Sistema de Gerenciamento de Biblioteca**, com o objetivo de digitalizar e organizar os processos de cadastro de acervo, controle de usuários, empréstimos, devoluções e reservas, oferecendo uma solução eficiente e de fácil manutenção.

---

## Objetivo

Modelar o sistema de informação e o banco de dados de um Sistema de Gerenciamento de Biblioteca, por meio de diagramas UML e modelagem entidade-relacionamento, como base para o desenvolvimento futuro da aplicação.

---

## Domínio do Problema

O sistema atende bibliotecas de instituições de ensino, contemplando os seguintes processos:

- Cadastro e gestão do acervo (livros, exemplares, autores, editoras e categorias)
- Cadastro e autenticação de usuários (alunos e funcionários)
- Realização, renovação e devolução de empréstimos
- Gerenciamento de reservas de exemplares
- Notificação automática de prazos e disponibilidade
- Geração de relatórios gerenciais pelos bibliotecários

---

## Modelagem do Banco de Dados

### MER Conceitual

O modelo conceitual representa as entidades do domínio e seus relacionamentos:

| Entidade | Descrição |
|----------|-----------|
| Usuário | Pessoa cadastrada que realiza empréstimos e reservas |
| Livro | Obra bibliográfica com título, ISBN e ano de publicação |
| Exemplar | Cópia física de um livro disponível no acervo |
| Empréstimo | Registro de retirada de um exemplar por um usuário |
| Reserva | Solicitação de exemplar indisponível |
| Autor | Responsável pela criação da obra |
| Editora | Empresa responsável pela publicação do livro |
| Categoria | Classificação temática dos livros |

> 📁 Imagem: `doc/mer_conceitual.png`

### MER Lógico

O modelo lógico traduz as entidades em tabelas relacionais:

- **USUARIO** (id_usuario PK, nome, email, telefone, tipo, data_cadastro)
- **LIVRO** (id_livro PK, isbn, titulo, ano_publicacao, id_editora FK, id_categoria FK)
- **EXEMPLAR** (id_exemplar PK, id_livro FK, num_tombo, status, localizacao)
- **EMPRESTIMO** (id_emprestimo PK, id_usuario FK, id_exemplar FK, data_emprestimo, data_prevista_dev, data_devolucao)
- **RESERVA** (id_reserva PK, id_usuario FK, id_exemplar FK, data_reserva, status)
- **AUTOR** (id_autor PK, nome, nacionalidade)
- **LIVRO_AUTOR** (id_livro FK, id_autor FK) — tabela associativa N:M
- **EDITORA** (id_editora PK, nome, cidade)
- **CATEGORIA** (id_categoria PK, nome)

> 📁 Imagem: `doc/mer_logico.png`

---

## Modelagem do Sistema (UML)

### Diagrama de Classes

O diagrama de classes representa a estrutura orientada a objetos do sistema, com herança entre `Pessoa`, `Usuário` e `Bibliotecário`, além das classes `Livro`, `Exemplar`, `Empréstimo`, `Reserva`, `Autor`, `Editora` e `Categoria`, com seus respectivos atributos e métodos.

> 📁 Imagem: `doc/diagrama_classes.png`

### Diagrama de Caso de Uso Geral

Atores do sistema:
- **Usuário** — realiza login, busca livros, solicita empréstimos e reservas, renova empréstimos e consulta histórico
- **Bibliotecário** — cadastra livros e exemplares, registra devoluções, gerencia usuários, categorias e gera relatórios
- **Sistema** — envia notificações automáticas de prazo e disponibilidade

> 📁 Imagem: `doc/caso_de_uso.png`

### Diagrama de Sequência

Representa o fluxo de mensagens para o caso de uso **Realizar Empréstimo**, envolvendo os participantes: Usuário, Interface, Sistema, Exemplar e Banco de Dados.

Fluxo principal:
1. Usuário solicita empréstimo
2. Sistema verifica autenticação
3. Sistema busca exemplares disponíveis
4. Sistema registra empréstimo no banco de dados
5. Sistema atualiza status do exemplar
6. Sistema emite comprovante e envia e-mail de confirmação

> 📁 Imagem: `doc/diagrama_sequencia.png`

### Diagrama de Atividades

Foram elaborados dois diagramas de atividades:

**1. Realizar Empréstimo**  
Detalha o fluxo de atividades desde a solicitação até a emissão do comprovante, incluindo decisões como verificação de autenticação e disponibilidade do exemplar.

**2. Devolução de Livro**  
Detalha o processo de devolução, incluindo verificação de prazo, cálculo de multa por atraso e notificação de usuários com reserva pendente.

> 📁 Imagens: `doc/diagrama_atividades_emprestimo.png` e `doc/diagrama_atividades_devolucao.png`

---

## Estrutura do Repositório

```
/
├── app/                  # Código-fonte da aplicação (entregas futuras)
├── doc/                  # Diagramas e documentação
│   ├── mer_conceitual.png
│   ├── mer_logico.png
│   ├── diagrama_classes.png
│   ├── caso_de_uso.png
│   ├── diagrama_sequencia.png
│   ├── diagrama_atividades_emprestimo.png
│   └── diagrama_atividades_devolucao.png
└── README.md
```

---

## Tecnologias e Ferramentas Utilizadas

| Ferramenta | Finalidade |
|-----------|------------|
| BRModelo | Modelagem do banco de dados (MER Conceitual e Lógico) |
| Visual Paradigm Community | Diagramas UML (Classes, Caso de Uso, Sequência, Atividades) |
| GitHub | Versionamento e documentação do projeto |

---

## Palavras-chave

Sistema de Biblioteca. Modelagem de Banco de Dados. UML. Diagrama de Classes. Caso de Uso. Diagrama de Sequência. Diagrama de Atividades. Entidade-Relacionamento.
