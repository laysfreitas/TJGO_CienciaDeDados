## **Relatório Final: Análise da Disparidade Tecnológica na Educação Básica do Brasil**

**Goiânia, 10 de Outubro de 2025**

### **1. Resumo**

Este relatório apresenta uma análise aprofundada sobre a desigualdade de acesso a recursos tecnológicos nas escolas de educação básica do Brasil. Utilizando dados do Censo Escolar, foi construída uma métrica para quantificar o número de alunos por dispositivo tecnológico, servindo como um indicador chave de infraestrutura digital. A análise exploratória revelou disparidades críticas entre as diferentes dependências administrativas (Federal, Estadual, Municipal, Privada) e regiões geográficas. Adicionalmente, foi empregada uma técnica de aprendizado não supervisionado (clusterização com K-Means) para segmentar as escolas e identificar quatro perfis distintos, caracterizando os diferentes estratos da realidade educacional e tecnológica do país. Os resultados confirmam um abismo digital significativo, penalizando principalmente as escolas das redes municipal e estadual e as localizadas nas regiões Norte e Nordeste.

### **2. Metodologia**

A análise foi conduzida utilizando a linguagem Python e as bibliotecas Pandas, Matplotlib, Seaborn e Scikit-learn.

**2.1. Fonte e Tratamento dos Dados**
Os dados utilizados foram extraídos de uma amostra do Censo Escolar. O tratamento inicial envolveu a criação de uma variável para o total de dispositivos e a remoção de entradas inválidas ou com dados ausentes que pudessem comprometer a análise.

**2.2. Métrica Principal: Alunos por Dispositivo**
Para medir o nível de acesso tecnológico, foi criada a métrica `ALUNOS_POR_DISPOSITIVO`. Calculada pela fórmula:
$$\text{Índice} = \frac{\text{Total de Matrículas na Educação Básica (QT\_MAT\_BAS)}}{\text{Total de Dispositivos para Alunos (QT\_TOTAL\_DISPOSITIVOS)}}$$
Este índice representa a demanda de alunos por cada recurso tecnológico disponível. **Valores mais altos indicam uma maior carência de dispositivos**, sendo um indicador de precariedade digital.

**2.3. Análise Exploratória de Dados (EDA)**
A investigação das disparidades foi realizada através de duas visualizações principais:

  * **Gráfico de Violino:** Para analisar a distribuição, a densidade e a mediana do índice por dependência administrativa.
  * **Gráfico de Barras:** Para criar um ranking da mediana do índice por região geográfica, comparando-as com a média nacional.

**2.4. Análise de Clusterização**
Para identificar perfis de escolas, foi utilizado o algoritmo **K-Means**. As features selecionadas para a segmentação foram `QT_MAT_BAS`, `ALUNOS_POR_DISPOSITIVO` e características categóricas como `TP_DEPENDENCIA`, `NO_REGIAO` e `TP_LOCALIZACAO`. Os dados foram pré-processados com One-Hot Encoding e normalizados com `StandardScaler`. A escolha do número ideal de clusters (`k=4`) foi validada por dois métodos: o **Método do Cotovelo**, que analisa a inércia, e a **Pontuação de Silhueta**, que mede a coesão e separação dos clusters.

### **3. Resultados e Análise**

**3.1. Disparidade por Dependência Administrativa**

O Gráfico de Violino abaixo ilustra a distribuição do índice `ALUNOS_POR_DISPOSITIVO` para cada rede de ensino.


A análise revela que:

  * **Rede Federal:** Apresenta o melhor desempenho, com a mediana mais baixa e uma distribuição compacta, indicando um padrão de alta qualidade e homogeneidade.
  * **Rede Municipal:** Possui a pior mediana, significando que a escola "típica" desta rede é a mais precária em termos de acesso tecnológico.
  * **Rede Estadual:** Encontra-se em uma situação limítrofe, com uma mediana próxima à média nacional, mas com uma grande quantidade de escolas em situação crítica.
  * **Rede Privada:** É a mais desigual. Embora tenha uma mediana baixa (indicando muitas escolas de elite bem equipadas), possui uma longa cauda de distribuição, revelando a existência de muitas escolas privadas com recursos escassos.

**3.2. Disparidade por Região Geográfica**

O ranking de regiões confirma que a desigualdade de acesso tecnológico no Brasil tem uma forte dimensão geográfica.


As conclusões são claras:

  * **Nordeste e Norte:** Lideram o ranking com os piores indicadores, apresentando medianas de alunos por dispositivo drasticamente superiores à média nacional (marcada pela linha pontilhada). A carência de recursos nessas regiões é crítica.
  * **Centro-Oeste:** Posiciona-se como a região que representa a média brasileira.
  * **Sudeste e Sul:** Apresentam os melhores desempenhos, com a região **Sul** se destacando como a mais bem equipada do país.

**3.3. Identificação de Perfis de Escolas (Clusterização)**

A escolha de **k=4 clusters** foi validada tanto pelo Método do Cotovelo quanto pela Pontuação de Silhueta, que apresentou seu valor máximo em k=4, indicando ser esta a segmentação mais significativa.


A análise das características médias de cada cluster revelou 4 perfis distintos de escolas no Brasil:

  * **Cluster 0 - Gigantes Estaduais Urbanas:** Escolas de grande porte (`QT_MAT_BAS` médio de 1546), predominantemente **Estaduais** e **Urbanas**, com um nível de acesso a dispositivos intermediário, mas ainda precário (média de 65 alunos/dispositivo).
  * **Cluster 1 - Escolas Rurais e Carentes:** Perfil de escolas de pequeno porte (`QT_MAT_BAS` médio de 258), majoritariamente **Rurais** e da rede **Municipal**. Este é o grupo com a **maior carência digital** (média de 123 alunos/dispositivo), representando o estrato mais vulnerável.
  * **Cluster 2 - Pequenas e Médias Urbanas:** O maior grupo, composto por escolas de porte pequeno a médio (`QT_MAT_BAS` médio de 525), quase que totalmente **Urbanas** e majoritariamente **Municipais**. O acesso a dispositivos é melhor que o do Cluster 1, mas ainda assim ruim (média de 47 alunos/dispositivo).
  * **Cluster 3 - Elite Tecnológica:** Grupo de escolas de porte médio (`QT_MAT_BAS` médio de 978), mas que se destaca por ter o **melhor acesso tecnológico** de todos (média de apenas 13 alunos/dispositivo). Este grupo é majoritariamente da rede **Privada**.

A visualização via PCA mostra uma separação razoável entre os clusters, confirmando que os perfis encontrados são estruturalmente distintos.

### **4. Conclusão**

Esta análise confirma, com base em dados, a existência de um profundo abismo digital na educação básica brasileira. A desigualdade não é aleatória, mas estruturada, afetando desproporcionalmente escolas públicas (municipais e estaduais), escolas rurais e as localizadas nas regiões Norte e Nordeste.

A segmentação via K-Means foi eficaz em identificar e caracterizar os diferentes "Brasis" que coexistem no sistema educacional. Os quatro perfis encontrados fornecem um mapa claro dos desafios, permitindo que futuras políticas públicas sejam direcionadas de forma mais eficaz — por exemplo, com ações emergenciais para o perfil "Escolas Rurais e Carentes" (Cluster 1) e planos de modernização para as "Gigantes Estaduais Urbanas" (Cluster 0).

O trabalho cumpre, portanto, todos os objetivos propostos, entregando um diagnóstico claro e multifacetado da disparidade tecnológica educacional no país.

-----

**Apêndice: Código Fonte**
O código completo utilizado para esta análise está disponível no Jupyter Notebook `trabalho_final.ipynb`.