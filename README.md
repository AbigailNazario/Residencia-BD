# Residencia-BD
Modelos MR e MER do projeto da residência tecnológica

## Modelagem do Banco de Dados

Este diretório contém os artefatos referentes à modelagem do banco de dados do projeto da residência tecnológica do quarto período, responsável por armazenar as informações necessárias para realizar e apresentar as estimativas de impacto ambiental relacionadas ao uso de Inteligência Artificial.

## Estrutura do Banco de Dados

O banco de dados foi desenvolvido utilizando **MySQL** e possui as seguintes entidades principais:

- **ANALISE**: armazena o prompt informado pelo usuário, a quantidade estimada de tokens e informações relacionadas à análise realizada.
- **RESULTADO_IMPACTO**: armazena os resultados estimados de consumo de energia, emissão de CO₂e e consumo indireto de água.
- **METODOLOGIA**: armazena as metodologias utilizadas para realizar os cálculos e suas respectivas versões.
- **PARAMETRO**: armazena os parâmetros utilizados pela metodologia para realizar os cálculos de impacto ambiental.
- **FONTE**: armazena as referências utilizadas para fundamentar os parâmetros e a metodologia.

A relação entre **PARAMETRO** e **FONTE** é realizada por meio da tabela associativa **PARAMETRO_FONTE**, permitindo que um parâmetro possua uma ou mais fontes e que uma fonte possa ser utilizada para diferentes parâmetros.

## Modelo Entidade-Relacionamento (MER)

O Modelo Entidade-Relacionamento representa visualmente as entidades, seus atributos e os relacionamentos existentes entre elas.
<img width="571" height="765" alt="Captura de tela 2026-10-01 201954" src="https://github.com/user-attachments/assets/891fa001-405e-44af-b5f3-e763754fc46f" />

## Modelo Relacional (MR)

O Modelo Relacional foi desenvolvido utilizando o MySQL Workbench e representa a estrutura das tabelas, seus atributos, chaves primárias e chaves estrangeiras.

O arquivo do Modelo Relacional está disponível neste repositório.

## Relacionamento entre as Tabelas

A estrutura do banco segue os seguintes relacionamentos:

- Uma **METODOLOGIA** pode estar associada a várias **ANALISES**.
- Cada **ANALISE** utiliza uma única **METODOLOGIA**.
- Uma **METODOLOGIA** possui vários **PARAMETROS**.
- Cada **PARAMETRO** pertence a uma única **METODOLOGIA**.
- Cada **ANALISE** possui um único **RESULTADO_IMPACTO**.
- Cada **RESULTADO_IMPACTO** está associado a uma única **ANALISE**.
- Um **PARAMETRO** pode possuir uma ou mais **FONTES**.
- Uma **FONTE** pode estar associada a vários **PARAMETROS**.
- A relação entre **PARAMETRO** e **FONTE** é realizada pela tabela **PARAMETRO_FONTE**.

### Representação simplificada

```text
                         ┌───────────────┐
                         │ METODOLOGIA   │
                         └───────┬───────┘
                                 │
                              1:N│
                                 │
                         ┌───────▼───────┐
                         │   PARAMETRO   │
                         └───────┬───────┘
                                 │
                              N:N│
                                 │
                    ┌────────────▼────────────┐
                    │    PARAMETRO_FONTE      │
                    └────────────┬────────────┘
                                 │
                              N:1│
                                 │
                         ┌───────▼───────┐
                         │     FONTE      │
                         └───────────────┘


┌───────────────┐
│ METODOLOGIA   │
└───────┬───────┘
        │
     1:N│
        │
┌───────▼───────┐
│    ANALISE    │
└───────┬───────┘
        │
     1:1│
        │
┌───────▼───────────────┐
│   RESULTADO_IMPACTO   │
└───────────────────────┘
