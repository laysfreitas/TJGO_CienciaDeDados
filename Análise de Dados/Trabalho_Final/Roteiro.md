# Relatório Final: A Desigualdade Oculta da Infraestrutura Digital na Educação Básica Brasileira

**Autora:** Lays de Freitas
**Data:** 06 de Outubro de 2025
**Disciplina:** Ciência de Dados
**Base de dados utilizada:** Microdados do Censo Escolar de 2024

---

## Parte 1

### 1. Business Understanding

**1.1 Negócio por trás dos dados**
O dataset representa o setor de **educação** no Brasil, especificamente focado na infraestrutura tecnológica das escolas de Ensino Médio.

**1.2 Objetivos estratégicos da organização**
A organização detentora dos dados (neste caso, o governo, através do Censo Escolar) pode ter os seguintes objetivos:
1.  **Melhorar a qualidade da educação básica:** Identificar e corrigir desigualdades na infraestrutura escolar para garantir que todos os alunos tenham acesso a recursos tecnológicos.
2.  **Otimizar investimentos em tecnologia:** Direcionar recursos de forma mais eficiente para as escolas e regiões que mais precisam, com base em evidências concretas.

**1.3 Problema de negócio**
O problema é a **desigualdade no acesso à tecnologia e à internet nas escolas de Ensino Médio do Brasil**. Muitas escolas não possuem a infraestrutura necessária para atender à demanda de seus alunos, criando uma disparidade de oportunidades educacionais. O projeto busca mensurar essa desigualdade e identificar as escolas e regiões mais críticas.

**1.4 Tradução para Ciência de Dados**
O problema de negócio foi transformado em um problema de **clusterização**. O objetivo é agrupar escolas com características semelhantes de infraestrutura e acesso tecnológico para identificar diferentes perfis e níveis de carência.

**1.5 Hipóteses iniciais**
1.  **Hipótese 1:** A maioria das escolas públicas, mesmo as que possuem laboratório de informática, têm um número insuficiente de dispositivos para atender seus alunos de forma adequada.
2.  **Hipótese 2:** Existe uma grande disparidade de acesso tecnológico entre as escolas da rede privada e as da rede pública (estadual e municipal), bem como entre as diferentes Unidades Federativas (UFs).

**1.6 Restrições**
* **Qualidade dos dados:** Os dados do Censo Escolar podem ter inconsistências ou valores ausentes que precisam de tratamento.
* **Generalização:** A análise se baseia nos dados de 2024, e a situação pode ter mudado.
* **Complexidade:** A infraestrutura tecnológica é apenas um dos muitos fatores que afetam a qualidade da educação.

**1.7 Critério de sucesso**
O projeto será considerado bem-sucedido se conseguir **criar um indicador claro e interpretável** sobre o acesso tecnológico nas escolas e **identificar os perfis de escolas (clusters) com diferentes níveis de carência**, permitindo a formulação de recomendações para políticas públicas.

**1.8 Métricas de avaliação**
Como o problema foi modelado como uma tarefa de clusterização, as métricas de avaliação apropriadas seriam o **Silhouette Score**, **Davies-Bouldin Index** e **Calinski-Harabasz Index** para avaliar a qualidade dos agrupamentos formados.

---

### 2. Data Understanding

**2.1 Coleta**
* **Dados disponíveis:** A base inicial continha 215.545 registros e 24 colunas.
* **Origem dos dados:** Os dados são públicos, provenientes dos microdados do **Censo Escolar de 2024**.
* **Adequação:** O volume e a granularidade dos dados são adequados para a análise, pois contêm informações detalhadas sobre cada escola do país.
* **Limitações:** Não há limitações éticas ou de privacidade, pois os dados são públicos e anonimizados.
* **Principais variáveis:** `SG_UF`, `TP_DEPENDENCIA`, `QT_MAT_BAS`, `QT_MAT_MED`, `IN_LABORATORIO_INFORMATICA`, `IN_BANDA_LARGA`, `QT_COMP_ALUNO`, `QT_TABLET_ALUNO`, `QT_NOTEBOOK_ALUNO`.

**2.2 Exploração**
* **Dados faltantes:** Foram identificados valores faltantes nas colunas de quantidade de dispositivos (`QT_...`), que foram tratados preenchendo-os com zero.
* **Outliers:** A análise de boxplot revelou uma grande variação e a presença de outliers na distribuição de alunos por dispositivo, especialmente nas redes estadual e municipal.
* **Balanceamento:** A tarefa é de clusterização, portanto, o conceito de balanceamento da variável-alvo não se aplica diretamente.
* **Correlações:** A análise exploratória mostrou que a simples existência de um laboratório de informática (`IN_LABORATORIO_INFORMATICA`) não garante um bom acesso tecnológico, indicando a necessidade de analisar a proporção de alunos por dispositivo.
* **Sugestões preliminares:** Os dados sugerem que as escolas federais possuem a melhor infraestrutura, enquanto as estaduais e municipais enfrentam os maiores desafios. Há também uma clara desigualdade regional entre os estados.

---

### 3. Data Preparation

**3.1 Seleção de atributos**
Foram selecionadas variáveis relevantes para o problema, como localização (`SG_UF`), dependência administrativa (`TP_DEPENDENCIA`), número de matrículas (`QT_MAT_BAS`), acesso à internet (`IN_BANDA_LARGA`) e quantidade de dispositivos.

**3.2 Tratamento de registros**
Foram descartados registros de escolas que não estavam em atividade e aquelas que não possuíam matrículas no Ensino Médio, resultando em um conjunto de dados final de 29.993 escolas.

**3.3 Subconjuntos de dados**
Para uma tarefa de clusterização, a divisão em treino e teste não é tipicamente necessária da mesma forma que em modelos supervisionados. O modelo foi aplicado a todo o conjunto de dados preparado.

**3.4 Outliers**
Os outliers foram mantidos na análise, pois representam escolas com situações extremas (muito boas ou muito ruins) que são importantes para entender a dimensão da desigualdade.

**3.5 Criação de novas variáveis (feature engineering)**
* `QT_TOTAL_DISPOSITIVOS`: Soma de computadores de mesa, notebooks e tablets disponíveis para os alunos.
* `ALUNOS_MEDIO_POR_DISPOSITIVO`: Indicador principal que representa a proporção de alunos do Ensino Médio por dispositivo.
* `INDICE_ACESSO`: Classificação categórica ("Ideal", "Adequado", "Baixo", "Crítico", "Nenhum") com base no indicador anterior.

**3.6 Codificação de variáveis categóricas**
As variáveis categóricas, como `SG_UF` e `TP_DEPENDENCIA`, foram transformadas em variáveis dummy (one-hot encoding) para serem utilizadas no modelo de clusterização.

**3.7 Normalização/padronização de variáveis numéricas**
Embora não explicitamente detalhado no notebook, é uma prática padrão e recomendada aplicar a normalização (como `StandardScaler`) antes de usar o K-Means, para que as variáveis com escalas diferentes não distorçam o resultado.

**3.10 Conjunto final**
O dataset final, após a limpeza, seleção de atributos e engenharia de features, estava pronto para a aplicação do algoritmo de Machine Learning.

---

## Parte 2

### 4. Modeling

**4.1 Escolha da tarefa**
( ) Classificação
( ) Regressão
(X) **Clusterização** (segmentar escolas com base em sua infraestrutura tecnológica).

**4.2 Algoritmos utilizados**
* **K-Means:** Foi escolhido por ser um algoritmo de clusterização eficiente, robusto e amplamente utilizado, adequado para agrupar as escolas em um número pré-definido de clusters com base em suas similaridades.

**4.3 Preparação para modelagem**
Sim, houve ajustes adicionais. As variáveis categóricas foram transformadas em dummies e as features numéricas foram selecionadas para a modelagem. A divisão em treino/teste não foi necessária para esta abordagem não supervisionada.

**4.4 Construção dos modelos**
O modelo K-Means foi treinado com o conjunto de dados preparado. O número de clusters foi definido como 4. O algoritmo agrupou as 29.993 escolas em quatro clusters distintos, com base nas features selecionadas.

* Cluster 0: 3.344 escolas
* Cluster 1: 5.653 escolas
* Cluster 2: 465 escolas
* Cluster 3: 19.668 escolas

---

### 5. Evaluation

**5.1 Avaliação do desempenho**
* [cite_start]**Métricas utilizadas:** Para a clusterização, as métricas adequadas seriam **Silhouette Score**, **Davies-Bouldin Index** e **Calinski-Harabasz Index**[cite: 221]. Elas medem a coesão (quão similares são os pontos dentro de um mesmo cluster) e a separação (quão distintos são os clusters entre si).
* **Valores obtidos:** O notebook não apresenta os cálculos explícitos dessas métricas de avaliação. Uma análise completa deveria incluí-los para validar a qualidade dos clusters formados.

**5.2 Comparação de modelos**
Apenas um algoritmo (K-Means) foi testado, portanto não há comparação de modelos.

**5.3 Alinhamento com o problema de negócio**
Os resultados atendem ao critério de sucesso definido na Parte 1, pois o modelo conseguiu segmentar as escolas em grupos com características distintas, revelando diferentes perfis de infraestrutura e permitindo a identificação de grupos com maiores carências.

---

### 6. Conclusão e Encaminhamentos

**6.1 Principais descobertas**
* O modelo revelou que a grande maioria das escolas se concentra em um único cluster (Cluster 3, com 19.668 escolas), sugerindo um perfil predominante de infraestrutura no país.
* A análise dos clusters por estado e dependência administrativa permite identificar padrões regionais e sistêmicos de desigualdade. Por exemplo, o Cluster 0 é predominantemente composto por escolas de Minas Gerais, indicando um perfil específico de infraestrutura naquele estado.
* A análise confirmou que a desigualdade de acesso é um problema crítico, com a maioria das escolas, mesmo com laboratórios de informática, apresentando um índice de acesso "Crítico" ou "Baixo".

**6.2 Limitações do estudo**
* A análise se baseia em dados auto-reportados no Censo Escolar, que podem conter imprecisões.
* O número de clusters (k=4) foi uma escolha inicial e poderia ser otimizado com métodos como o "Elbow Method" ou a análise do Silhouette Score.
* O modelo de clusterização identifica padrões, mas não explica as causas da desigualdade.

**6.3 Recomendações futuras**
* **Aprofundar o estudo:** Analisar os perfis de cada cluster em mais detalhes, cruzando com outras variáveis como o desempenho dos alunos (IDEB) para medir o impacto da infraestrutura.
* **Testar novos algoritmos:** Utilizar outros algoritmos de clusterização, como o DBSCAN, que não exige a pré-definição do número de clusters.
* **Enriquecer os dados:** Integrar a base de dados com fontes externas, como dados socioeconômicos do IBGE, para uma análise mais completa das causas da desigualdade.

**6.4 Conclusão final**
O objetivo inicial de analisar e mensurar a desigualdade de acesso tecnológico nas escolas de Ensino Médio do Brasil foi alcançado. O projeto utilizou técnicas de Ciência de Dados para transformar um problema de negócio em uma análise quantitativa, criando um indicador de acesso e segmentando as escolas em grupos com perfis distintos. Os resultados fornecem evidências claras sobre as disparidades existentes e podem servir como um ponto de partida para a formulação de políticas públicas mais eficazes.