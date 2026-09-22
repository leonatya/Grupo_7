# Projeto Final DS-PY-004  
## Análise Exploratória — Votação por Seção (TSE 2022)

Este repositório contém o projeto final da disciplina **DS-PY-004**, cujo objetivo é realizar uma **análise exploratória de dados (EDA)** utilizando a base oficial do **Tribunal Superior Eleitoral (TSE)** referente à votação por seção nas eleições de 2022.

A análise foca nos estados:

- **RJ — Rio de Janeiro**  
- **MG — Minas Gerais**  
- **SC — Santa Catarina**

A base utilizada é **DETALHE_VOTACAO_SECAO**, disponibilizada pelo TSE.

---

## Estrutura do Repositório

Grupo_7/ ├── dados/ │ ├── detalhe_votacao_secao_2022_SC.csv │ ├── detalhe_votacao_secao_2022_RJ.csv │ └── detalhe_votacao_secao_2022_MG.csv │ └── (arquivos grandes armazenados via Git LFS) │ ├── notebooks/ │ └── analise.ipynb │ ├── src/ │ └── funcoes_auxiliares.py │ ├── README.md └── .gitignore
Código

---

## Armazenamento de Arquivos Grandes (Git LFS)

Os arquivos CSV do TSE possuem dezenas de MB.  
Para evitar problemas de versionamento e garantir integridade dos dados, este projeto utiliza:

### **Git LFS (Large File Storage)**

Comandos utilizados:

```bash
git lfs install
git lfs track "*.csv"
git add .
git commit -m "adiciona arquivos grandes via LFS"
Para clonar corretamente:
bash
git lfs install
git clone https://github.com/leonatya/Grupo_7
Objetivo do Projeto
Realizar uma análise exploratória completa da votação por seção, incluindo:
•	Diagnóstico de qualidade dos dados
•	Limpeza e padronização
•	Tratamento de valores especiais do TSE (#NULO, #NE, -1, -3)
•	Criação de métricas derivadas
•	Visualizações
•	Identificação de padrões e outliers
•	Comparações entre estados e municípios
•	Interpretação dos resultados com base estatística
Perguntas de Análise
1.	Como a taxa de abstenção varia entre municípios dos três estados?
2.	Existe relação entre o tamanho da seção (QT_APTOS) e a taxa de abstenção?
3.	Quais municípios apresentam maior proporção de votos brancos e nulos?
4.	Há diferenças relevantes entre zonas eleitorais dentro de um mesmo município?
5.	A distribuição de votos válidos por seção apresenta outliers?
6.	Como RJ, MG e SC se comparam em termos de engajamento eleitoral?
Base de Dados
A base utilizada foi baixada diretamente do repositório oficial do TSE:
DETALHE_VOTACAO_SECAO 2022 Disponível em: https://cdn.tse.jus.br/estatistica/sead/odsele/detalhe_votacao_secao/detalhe_votacao_secao_2022.zip
Observações importantes do LEIAME do TSE
•	Codificação: Latin-1
•	Separador: ;
•	Campos entre aspas
•	Valores especiais:
o	#NULO → dado ausente
o	#NE → dado não existente naquele ano
o	-1 → NULO numérico
o	-3 → NE numérico
•	UF pode conter: BR, VT, ZZ
•	Seções podem estar:
o	não instaladas (ST_SECAO_INSTALADA = N)
o	anuladas (ST_SECAO_ANULADA = S)
Todos esses pontos foram tratados no notebook.
Limpeza e Transformação
As principais etapas incluem:
•	Remoção de seções não instaladas ou anuladas
•	Padronização de valores especiais
•	Conversão de colunas numéricas
•	Filtragem dos estados RJ, MG e SC
•	Criação de métricas derivadas:
o	taxa_abstencao
o	prop_brancos
o	prop_nulos
o	prop_brancos_nulos
o	prop_validos
o	faixa_secao (pequena, média, grande)
Visualizações
O notebook inclui gráficos como:
•	Boxplots por estado
•	Scatterplots entre aptos e abstenção
•	Histogramas
•	Tabelas dinâmicas (pivot tables)
•	Identificação de outliers por z-score
•	Comparações entre estados
•	Análises por município e zona eleitoral
 Tecnologias Utilizadas
•	Python 3
•	Pandas
•	NumPy
•	Matplotlib
•	Seaborn
•	Plotly Express
•	Jupyter Notebook
•	Git / GitHub
•	Git LFS (para arquivos grandes)
Integrantes do Grupo
•	Leonardo Antonio
•	Caryane Ribeiro
•	Leonardo Rodrigues
Como Executar
Clone o repositório:
bash
git clone https://github.com/leonatya/Grupo_7
Instale as dependências:
bash
pip install -r requirements.txt
Abra o notebook:
bash
jupyter notebook notebooks/analise.ipynb
Licença
Este projeto utiliza dados públicos disponibilizados pelo Tribunal Superior Eleitoral (TSE). O uso dos dados segue as diretrizes do LEIAME oficial incluído no pacote.
 Contato
Dúvidas sobre os dados: estatistica@tse.jus.br
Dúvidas sobre o projeto:
•	Leonardo Rodrigues — (21) 98121-6771
•	Leonardo Antonio — (34) 99269-7677
•	Caryane Ribeiro — (49) 98874-8042

Explicação dos Principais Códigos do Projeto Final DS-PY-004
1. Introdução
Este documento apresenta explicações detalhadas dos principais trechos de código utilizados no projeto de análise exploratória dos dados eleitorais do TSE. O objetivo é esclarecer o propósito de cada etapa, justificando as decisões técnicas adotadas e facilitando a compreensão do fluxo lógico da análise.
As explicações foram elaboradas com linguagem didática, como um professor orientando o aluno, destacando boas práticas de programação e análise de dados.
2. Importação das Bibliotecas
import pandas as pd
import numpy as np
import plotly.express as px
import matplotlib.pyplot as plt
import seaborn as sns
Por que este código é importante?
•	pandas: biblioteca essencial para manipulação de dados tabulares.
•	numpy: usada para operações matemáticas e vetoriais.
•	plotly.express: gera gráficos interativos, úteis para explorar padrões.
•	matplotlib / seaborn: bibliotecas tradicionais para visualização estática.
3. Leitura das Bases do TSE
df_rj = pd.read_csv("C:/Users/leona/Downloads/TEC_PROGAMACAO/Grupo_7/dados/detalhe_votacao_secao_2022_RJ.csv", encoding="latin1", sep=";",)
df_mg = pd.read_csv("C:/Users/leona/Downloads/TEC_PROGAMACAO/Grupo_7/dados/detalhe_votacao_secao_2022_MG.csv", encoding="latin1", sep=";",)
df_sc = pd.read_csv("C:/Users/leona/Downloads/TEC_PROGAMACAO/Grupo_7/dados/detalhe_votacao_secao_2022_SC.csv", encoding="latin1", sep=";",)
Motivo do código
•	Os arquivos do TSE utilizam ponto e vírgula como separador.
•	O encoding latin1 evita erros de acentuação.
4. Identificação do Estado
df_mg["estado"] = "MG"
df_rj["estado"] = "RJ"
df_sc["estado"] = "SC"
Motivo do código
•	Permite identificar a origem de cada linha após a consolidação das bases.
•	Essencial para análises comparativas entre estados.
5. Consolidação das Bases
df = pd.concat([df_mg, df_rj, df_sc], ignore_index=True)
Motivo do código
•	Junta as três bases em um único DataFrame.
•	Facilita análises globais e comparações.
•	ignore_index=True evita duplicação de índices.
6. Inspeção Inicial
df.info()
df.describe()
df.head()
Motivo do código
•	Verificar tipos de dados.
•	Identificar colunas numéricas e categóricas.
•	Detectar possíveis problemas (nulos, tipos incorretos).
7. Verificação de Duplicidades
duplicados = df.duplicated(subset=["estado", "NM_MUNICIPIO", "NR_ZONA", "NR_SECAO"]).sum()
Motivo do código
•	Garante que não existam seções duplicadas.
•	Usa a combinação correta de identificadores.
8. Criação das Métricas Derivadas
df["taxa_abstencao"] = df["QT_ABSTENCOES"] / df["QT_APTOS"]
df["prop_brancos"] = df["QT_VOTOS_BRANCOS"] / df["QT_COMPARECIMENTO"]
df["prop_nulos"] = df["QT_VOTOS_NULOS"] / df["QT_COMPARECIMENTO"]
df["prop_brancos_nulos"] = (df["QT_VOTOS_BRANCOS"] + df["QT_VOTOS_NULOS"]) / df["QT_COMPARECIMENTO"]
df["prop_validos"] = df["QT_VOTOS_VALIDOS"] / df["QT_COMPARECIMENTO"]
Motivo do código
•	Permite comparar seções de tamanhos diferentes.
•	Transforma valores absolutos em proporções.
•	Facilita análises estatísticas e gráficos.
9. Gráficos Exploratórios
px.box(df, x="estado", y="taxa_abstencao")
Motivo do código
•	Boxplots são ideais para identificar outliers e comparar distribuições.
•	A escolha de Plotly permite interação e melhor interpretação.
10. Análises por Estado
df_rj.groupby("NM_MUNICIPIO")["taxa_abstencao"].mean().sort_values()
Motivo do código
•	Permite identificar municípios com maior ou menor engajamento.
•	groupby é a ferramenta correta para agregações.
11. Identificação de Outliers
python
Q1 = df["prop_validos"].quantile(0.25)
Q3 = df["prop_validos"].quantile(0.75)
IQR = Q3 - Q1

outliers = df[(df["prop_validos"] < Q1 - 1.5*IQR) | (df["prop_validos"] > Q3 + 1.5*IQR)]
Motivo do código
•	Método IQR é padrão para detectar valores extremos.
•	Ajuda a identificar seções com comportamento atípico.
12. Conclusões
As conclusões do projeto foram baseadas nos gráficos e métricas derivadas, seguindo boas práticas de EDA. Você identificou corretamente:
•	padrões distintos entre estados,
•	ausência de relação entre tamanho da seção e abstenção,
•	diferenças internas relevantes,
•	comportamento estrutural dos outliers.
Observação sobre Git LFS
Durante o desenvolvimento, os arquivos CSV do TSE apresentaram tamanho elevado (dezenas de MB). Para garantir versionamento seguro, foi utilizado:
bash
git lfs install
git lfs track "*.csv"

