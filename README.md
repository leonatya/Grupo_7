## Projeto Final DS-PY-004

Análise Exploratória — Votação por Seção (TSE 2022)

Este repositório contém o projeto final da disciplina DS-PY-004, cujo objetivo é realizar uma análise exploratória de dados (EDA) utilizando a base oficial do Tribunal Superior Eleitoral (TSE) referente à votação por seção nas eleições de 2022.

A análise foca nos estados:

RJ — Rio de Janeiro

MG — Minas Gerais

SC — Santa Catarina

A base utilizada é DETALHE_VOTACAO_SECAO, disponibilizada pelo TSE.

Estrutura do Repositório

Grupo_7/ ├── dados/ │ ├── detalhe_votacao_secao_2022_SC.csv │ ├── detalhe_votacao_secao_2022_RJ.csv │ └── detalhe_votacao_secao_2022_MG.csv │ ├── notebooks/ │ └── analise.ipynb │ ├── README.md └── .gitignore

Objetivo do Projeto

Realizar uma análise exploratória completa da votação por seção, incluindo:

Diagnóstico de qualidade dos dados

Limpeza e padronização

Tratamento de valores especiais do TSE (#NULO, #NE, -1, -3)

Criação de métricas derivadas

Visualizações

Identificação de padrões e outliers

Comparações entre estados e municípios

Perguntas de Análise

Como a taxa de abstenção varia entre municípios dos três estados?

Existe relação entre o tamanho da seção (QT_APTOS) e a taxa de abstenção?

Quais municípios apresentam maior proporção de votos brancos e nulos?

Há diferenças relevantes entre zonas eleitorais dentro de um mesmo município?

A distribuição de votos válidos por seção apresenta outliers?

Base de Dados

A base utilizada foi baixada diretamente do repositório oficial do TSE:

DETALHE_VOTACAO_SECAO 2022
Disponível em: https://cdn.tse.jus.br/estatistica/sead/odsele/detalhe_votacao_secao/detalhe_votacao_secao_2022.zip

Observações importantes do LEIAME do TSE

Codificação: Latin-1

Separador: ;

Campos entre aspas

Valores especiais:

#NULO → dado ausente

#NE → dado não existente naquele ano

-1 → NULO numérico

-3 → NE numérico

UF pode conter: BR, VT, ZZ

Seções podem estar:

não instaladas (ST_SECAO_INSTALADA = N)

anuladas (ST_SECAO_ANULADA = S)

Esses pontos foram tratados no notebook.

Limpeza e Transformação

As principais etapas de limpeza incluem:

Remoção de seções não instaladas ou anuladas

Padronização de valores especiais

Conversão de colunas numéricas

Filtragem de estados (RJ, MG, SC)

Criação de métricas:

taxa_abstencao

prop_brancos

prop_nulos

faixa_secao (pequena, média, grande)

Visualizações

O notebook inclui gráficos como:

Boxplots por estado

Scatterplots entre aptos e abstenção

Histogramas

Tabelas dinâmicas (pivot tables)

Identificação de outliers por z-score

Tecnologias Utilizadas

Python 3

Pandas

NumPy

Matplotlib

Seaborn

Jupyter Notebook

Git / GitHub

Integrantes do Grupo

Leonardo Antonio Caryane Ribeiro Leonardo Rodrigues

Como Executar

Clone o repositório:

git clone https://github.com/leonatya/Grupo_7 Instale as dependências: pip install -r requirements.txt Abra o notebook: jupyter notebook notebooks/analise.ipynb

Licença Este projeto utiliza dados públicos disponibilizados pelo Tribunal Superior Eleitoral (TSE). O uso dos dados segue as diretrizes do LEIAME oficial incluído no pacote.

Contato Para dúvidas sobre os dados: estatistica@tse.jus.br

Para dúvidas sobre o projeto: Leonardo Rodrigues - (21) 98121-6771 Leonardo Antonio - (34) 99269-7677 Caryane Ribeiro - (49) 98874-8042