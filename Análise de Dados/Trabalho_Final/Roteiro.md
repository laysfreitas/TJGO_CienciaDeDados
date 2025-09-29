# Relatório Final: A Desigualdade Oculta da Infraestrutura Digital na Educação Básica Brasileira

**Autora:** Lays Fraga
**Data:** 28 de setembro de 2025
**Disciplina:** Cientista de Dados

---

## 1. Definição do Problema

O presente projeto de Ciência de Dados aborda um problema central para o desenvolvimento da educação no Brasil: a qualidade e a equidade do acesso à infraestrutura digital nas escolas de educação básica.

A **pergunta de pesquisa** que norteia este trabalho é:

> A simples existência de um laboratório de informática ou de acesso à internet é um indicador suficiente da inclusão digital escolar, ou uma análise mais aprofundada da proporção de dispositivos por aluno e da qualidade da conexão revela desigualdades estruturais ocultas?

A **relevância** desta questão é acentuada no cenário pós-pandemia, onde a tecnologia se consolidou como ferramenta pedagógica essencial. Compreender a diferença entre ter uma infraestrutura nominalmente "existente" e uma infraestrutura *funcional e acessível* é fundamental para orientar políticas públicas que visem a uma modernização educacional verdadeiramente equitativa.

## 2. Coleta de Dados

* **Fonte:** Os dados utilizados são públicos, provenientes dos Microdados do Censo Escolar da Educação Básica de 2024, disponibilizados pelo Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira (INEP).
* **Método de Obtenção:** Download direto do portal de dados abertos do governo brasileiro.
* **Formato:** O arquivo original está no formato CSV (`.csv`), com dados em nível de escola.

## 3. Limpeza e Preparação de Dados

O tratamento dos dados brutos foi uma etapa crucial para garantir a qualidade da análise. As seguintes ações foram tomadas:

1.  **Filtragem Inicial:** O dataset foi filtrado para incluir apenas escolas com `TP_SITUACAO_FUNCIONAMENTO` igual a 1 (Em atividade) e com `QT_MAT_BAS` (total de matrículas) maior que zero.
2.  **Engenharia de Features:** Para responder à pergunta de pesquisa, foi necessário criar novas variáveis que capturassem a qualidade do acesso, e não apenas sua existência.
    * **`QT_TOTAL_DISPOSITIVOS`**: Soma dos desktops, laptops e tablets disponíveis para uso dos alunos.
    * **`ALUNOS_POR_DISPOSITIVO`**: Métrica central do estudo, calculada como `QT_MAT_BAS / QT_TOTAL_DISPOSITIVOS`. Um valor alto indica baixa disponibilidade de equipamentos.
    * **`INDICE_ACESSO_GERAL`**: Classificação categórica da métrica anterior em níveis de qualidade (`Ideal`, `Adequado`, `Baixo`, `Crítico`, `Nenhum`), permitindo uma interpretação mais direta.

## 4. Análise Exploratória (EDA)

A análise exploratória revelou padrões profundos e confirmou a hipótese inicial do projeto.

* **A Falácia da Infraestrutura Existente:** A análise demonstrou que uma grande parcela das escolas que reportam possuir laboratório de informática e acesso à internet, na verdade, se enquadra nas categorias de acesso "Crítico" ou "Baixo", com mais de 25 alunos por dispositivo.
* **Disparidade Socioeconômica e Regional:** Foi identificada uma clara divisão: escolas `Privadas` possuem uma qualidade de acesso digital imensamente superior às `Públicas` (Estaduais e, principalmente, Municipais). Geograficamente, as regiões `Norte` e `Nordeste` concentram a maior proporção de escolas com acesso "Crítico".
* **Vulnerabilidade Social:** A análise aprofundada em escolas com `TP_LOCALIZACAO_DIFERENCIADA` mostrou que aquelas localizadas em **Terras Indígenas** e **Áreas de Quilombos** apresentam os piores indicadores de acesso digital do país, evidenciando uma sobreposição de desigualdades históricas e tecnológicas.

## 5. Modelagem

* **Algoritmo Escolhido:** Foi utilizado o **K-Means Clustering**, um algoritmo de aprendizado não supervisionado.
* **Justificativa:** O objetivo não era prever um valor específico, mas sim descobrir "perfis" ou agrupamentos naturais de escolas com base em suas características de infraestrutura e demografia. A clusterização é a abordagem ideal para essa tarefa de segmentação e descoberta de padrões.
* **Avaliação de Desempenho:** A escolha do número ótimo de clusters (k=4) foi validada pelo "Método do Cotovelo" (Elbow Method). A avaliação final da qualidade dos clusters foi qualitativa, baseada na coesão e na interpretabilidade dos perfis encontrados, que se mostraram distintos e alinhados com as descobertas da EDA.

## 6. Interpretação dos Resultados

A aplicação do modelo de clusterização permitiu traduzir os dados complexos em quatro perfis claros e acionáveis:

* **Cluster 0 - Gigantes Públicas com Acesso Crítico:** Escolas de grande porte, majoritariamente estaduais e municipais, com muitos alunos, mas com uma proporção de alunos por dispositivo extremamente alta (acesso "Crítico"). Representam o maior desafio de investimento em larga escala.
* **Cluster 1 - Privadas e Federais Bem Equipadas:** Perfil de excelência. Escolas privadas e federais, com um baixo número de alunos por dispositivo (acesso "Ideal" ou "Adequado") e alta prevalência de banda larga.
* **Cluster 2 - Pequenas e Desassistidas:** Escolas de pequeno porte, principalmente municipais e localizadas em zonas rurais, que frequentemente não possuem sequer um laboratório ou banda larga. São os "desertos digitais" do sistema educacional.
* **Cluster 3 - Médias Públicas em Luta:** Um grupo intermediário de escolas públicas de médio porte que possuem alguma infraestrutura, mas lutam com um acesso de qualidade "Baixa" a "Crítica".

## 7. Comunicação dos Resultados

Os resultados deste projeto serão comunicados através de dois artefatos principais:

1.  **Relatório Técnico:** Este documento (`.md`), acompanhado do código-fonte completo (`.py`), que detalha toda a metodologia e as descobertas.
2.  **Apresentação Oral:** Uma apresentação de 10 minutos focada na narrativa dos dados, começando com a provocação inicial (a falácia do "ter laboratório"), passando pelas evidências visuais da desigualdade e culminando na apresentação dos perfis de escolas identificados pelo modelo. A comunicação visual será priorizada para garantir a clareza e o impacto das conclusões.