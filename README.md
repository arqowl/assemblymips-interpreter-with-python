# Documentação do Interpretador de Assembly da disciplina de Paradigmas de linguagem de programação

## 🤝 Colaboradores
- [Arquimedes](https://github.com/arqowl)
- [Maca](https://github.com/victormacaubas)
- [Maria do C.](https://github.com/Madu-dev)
- [Mari](https://github.com/marianazanon)
- [Thobias](https://github.com/dashp21)


## Matriz RACI - Atividades vs Responsabilidades
| Atividade                                | Responsável |
|------------------------------------------|-------------|
| Gramática do Assembly MIPS               | Arquimedes  |
| Organização do GITHUB e ambiente Python  | Maca        |
| Analisador Léxico                        | Maria do C. |
| Analisador Sintático                     | Maca        |
| Analisador Semântico                     | Thobias     |
| Gestor de erros                          | Mari        |
| Documentação do Interpretador            | Arquimedes  |

## Pontos importantes do Interpretador `sobre Testes`
- Ele possui duas formas de testes:
    1. Testes unitários a partir da metodologia TDD que facilitaram a construção do código;
    2. Leitura arquivo "sample_app.asm" com a finalidade visualizar a funcionalidade de interpretação em si no *main.py*.


## Pontos importantes do Interpretador `sobre o Código`
- O "sample_app.asm" funciona da seguinte forma:
    1. O código está preso em um loop que continuamente carrega valores da memória, realiza operações aritméticas e verifica condições de igualdade entre os resultados.
    2. O loop só sai da parte condicional (entre label1 e label2) se $t3 for igual a $t4. No entanto, devido à natureza das operações (soma e subtração), $t3 e $t4 só serão iguais se ambos $t0 e $t2 forem zero. Caso contrário, o código continua no loop.
    3. Assim, o código calcula t5 = t3 + 10 sempre que a condição beq é satisfeita e então retorna ao início do loop.
    4. Desta forma, o código é capaz de contemplar as instruções I, R e J, abordando loops e condicionais, algo que uma linguagem de baixo nível como o Assembly precisa ter.

## Pontos importantes do Interpretador `sobre o Tratamento de erros`
- Os tratamentos de erros são tratados pelos *tipos* de erros e pela localização onde eles se encontram.
- Tipos de erros que herdam da classe "MIPSInterpreterError":
    1. Léxico;
    2. Sintático;
    3. Semântico.

## Pontos importantes do Interpretador `sobre a Gramática`
- a Gramática Livre de Contexto foi a primeira atividade feita pelo grupo e também inspirada nas instruções aprendidas durantes as duas disciplinas de Arquitetura de computadores 1 e 2.

## Pontos importantes do Interpretador `sobre Recomendações`
- Algumas observações e recomendações:
    1. Recomendamos que o repositório seja aberto no Gitpod.io para os testes rodem de forma assertiva. Caso não seja possível, tentar executar *pip install pytest* no terminal da sua IDE;
    2. Para rodar o arquivo main.py que carrega e lê o arquivo em assembly o comando que tem a ser executado no terminal é *python src/main.py*

## Pontos importantes do Interpretador `sobre o Interpretador em si`
- O Código criado é um Interpretador propriamente dito e não um compilador, pois o Assembly está sendo interpretado por uma linguagem interpretada.
