### Microdados do Censo da Educação Básica 2024

Sistema Inepdata, que também permite a execução de consultas sobre os principais dados da Educação Básica do país, inclusive ao nível de municípios:
[https://www.gov.br/inep/pt-br/areas-de-atuacao/pesquisas-estatisticas-e-indicadores/censo-escolar/resultados](Microdados da Educação Básica 2024)

### DADOS

Encontra-se, neste diretório, as bases de dados estruturadas no formato **CSV (Comma-Separated Values)**, delimitados por ponto-e-vírgula (**;**). Esse novo formato dos Microdados, traz dois arquivos de dados que foram dimensionados ao nível de escolas, e contemplam uma série de tabulações que permitem rapidamente obter as principais estatísticas educacionais. Esses dois arquivos consistem em:

1.  **Base estatística por escola**, denominada `microdados_ed_basica_2024`, contendo, além dos dados cadastrais e de infraestrutura dos estabelecimentos de ensino, dentre outros, o número de matrículas por etapa de ensino, turno, tempo integral, sexo, cor/raça e faixa etária dos alunos. Além disso, é possível consultar também o número de docentes e turmas por etapa de ensino.

2.  **Base suplementar**, denominada `suplemento_cursos_tecnicos_2024`, contendo o número de matrículas por curso técnico. Os dados estão dimensionados por estabelecimento de ensino, permitindo o cruzamento entre as duas bases por meio da variável `CO_ENTIDADE`.

---

### Categorias de Dados dos Microdados do Censo Escolar

A estrutura dos Microdados do Censo Escolar do INEP pode ser separada em várias categorias principais para facilitar a análise:

#### 1. Dados de Localização e Cadastro da Escola
Este grupo de variáveis identifica e localiza a escola no território nacional, além de definir sua natureza administrativa.

* **Identificadores Únicos:**
    * `CO_ENTIDADE`: Código único da escola (o principal identificador).
    * `NO_ENTIDADE`: Nome da escola.
* **Localização Geográfica:**
    * `CO_MUNICIPIO`: Código do Município (IBGE).
    * `NO_MUNICIPIO`: Nome do Município.
    * `CO_UF`: Código da Unidade da Federação (Estado).
    * `SG_UF`: Sigla da Unidade da Federação.
    * `CO_REGIAO`: Código da Região (ex: Centro-Oeste).
* **Zona e Dependência:**
    * `TP_LOCALIZACAO`: Tipo de localização (1 = Urbana, 2 = Rural).
    * `TP_DEPENDENCIA`: Dependência administrativa (1 = Federal, 2 = Estadual, 3 = Municipal, 4 = Privada).

#### 2. Dados de Infraestrutura Física e Pedagógica
Este conjunto descreve os recursos físicos e os equipamentos disponíveis na escola para os alunos e professores.

* **Estrutura Física Básica:**
    * Existência de água potável, energia elétrica, esgoto sanitário.
* **Espaços Pedagógicos:**
    * Existência de biblioteca ou sala de leitura.
    * Existência de laboratório de informática e de ciências.
    * Existência de quadra de esportes (coberta ou descoberta).
* **Recursos de Acessibilidade:**
    * Existência de rampas, corrimãos, banheiros adaptados para alunos com deficiência.
* **Recursos Tecnológicos:**
    * Disponibilidade de computadores para alunos e para uso administrativo.
    * Existência de acesso à internet e tipo de banda (larga ou não).

#### 3. Dados Agregados dos Alunos (Matrículas)
Estes não são dados individuais por aluno, mas sim totais agregados por escola, geralmente divididos por características demográficas e etapa de ensino.

* **Totais por Etapa de Ensino:**
    * Número de matrículas na Creche, Pré-escola, Anos Iniciais e Finais do Ensino Fundamental, Ensino Médio, EJA (Educação de Jovens e Adultos), etc.
* **Perfil Demográfico (dividido por etapa):**
    * Número de matrículas por **sexo** (masculino, feminino).
    * Número de matrículas por **cor/raça** (branca, preta, parda, amarela, indígena).
    * Número de matrículas por **faixa etária**.
* **Modalidades Específicas:**
    * Número de matrículas em **tempo integral**.
    * Número de matrículas na **educação especial**.

#### 4. Dados Agregados de Docentes e Turmas
Informações quantitativas sobre os recursos humanos (professores) e a organização das turmas.

* **Turmas (Classes):**
    * Número total de turmas por etapa de ensino (ex: 5 turmas de Ensino Fundamental).
    * Número de turmas por turno (matutino, vespertino, noturno).
* **Docentes (Professores):**
    * Número total de docentes em exercício na escola.
    * *(Em arquivos mais detalhados do Censo, é possível encontrar informações sobre a formação, tipo de contrato, etc., de cada docente).*

#### 5. Dados do Arquivo Suplementar (`suplemento_cursos_tecnicos`)
Este arquivo é mais específico e foca exclusivamente na Educação Profissional Técnica.

* **Matrículas por Curso:**
    * Número de matrículas para cada curso técnico oferecido (ex: Técnico em Informática, Técnico em Enfermagem).
    * As matrículas são detalhadas por **eixo tecnológico** e pelo **tipo de curso** (integrado, concomitante, subsequente).


---


#### **Seleção e Justificativa do Conjunto de Dados**

* **Conjunto de Dados:** O estudo utilizará os **Microdados do Censo Escolar da Educação Básica de 2024**, disponibilizado pelo INEP.

* **Seleção de Colunas:** Do conjunto total de variáveis, foi realizada uma seleção estratégica de **111 colunas**.

| Nome da Variável | Descrição da Variável |
|---|---|
| CO_ENTIDADE | Código da Escola |
| NO_ENTIDADE | Nome da Escola |
| NO_REGIAO | Nome da Região Geográfica |
| CO_REGIAO | Código da Região Geográfica |
| NO_UF | Nome da Unidade da Federação |
| SG_UF | Sigla da Unidade da Federação |
| CO_UF | Código da Unidade da Federação |
| NO_MUNICIPIO | Nome do Município |
| CO_MUNICIPIO | Código do Município |
| TP_DEPENDENCIA | Dependência Administrativa |
| TP_CATEGORIA_ESCOLA_PRIVADA | Categoria da escola privada |
| TP_LOCALIZACAO | Localização |
| TP_LOCALIZACAO_DIFERENCIADA | Localização diferenciada da escola |
| TP_SITUACAO_FUNCIONAMENTO | Situação de funcionamento |
| IN_PREDIO_COMPARTILHADO | Prédio compartilhado com outra escola |
| CO_ORGAO_REGIONAL | Código do Órgão Regional de Ensino |
| CO_ESCOLA_SEDE_VINCULADA | Código da escola sede |
| CO_IES_OFERTANTE | Código da IES vinculada à escola |
| QT_MAT_BAS | Número de Matrículas da Educação Básica
 |
| QT_MAT_INF | Número de Matrículas da Educação Infantil |
| QT_MAT_INF_CRE | Número de Matrículas da Educação Infantil - Creche |
| QT_MAT_INF_PRE | Número de Matrículas da Educação Infantil - Pré-Escola |
| QT_MAT_FUND | Número de Matrículas do Ensino Fundamental |
| QT_MAT_FUND_AI | Número de Matrículas do Ensino Fundamental - Anos Iniciais |
| QT_MAT_FUND_AF | Número de Matrículas do Ensino Fundamental - Anos Finais |
| QT_MAT_MED | Número de Matrículas do Ensino Médio |
| QT_MAT_FUND_AI_1 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 1º Ano |
| QT_MAT_FUND_AI_2 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 2º Ano |
| QT_MAT_FUND_AI_3 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 3º Ano |
| QT_MAT_FUND_AI_4 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 4º Ano |
| QT_MAT_FUND_AI_5 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 5º Ano |
| QT_MAT_FUND_AF_6 | Número de Matrículas do Ensino Fundamental - Anos Finais - 6º Ano |
| QT_MAT_FUND_AF_7 | Número de Matrículas do Ensino Fundamental - Anos Finais - 7º Ano |
| QT_MAT_FUND_AF_8 | Número de Matrículas do Ensino Fundamental - Anos Finais - 8º Ano |
| QT_MAT_FUND_AF_9 | Número de Matrículas do Ensino Fundamental - Anos Finais - 9º Ano |
| QT_MAT_BAS_FEM | Número de Matrículas da Educação Básica - Feminino |
| QT_MAT_BAS_MASC | Número de Matrículas da Educação Básica - Masculino |
| QT_MAT_BAS_ND | Número de Matrículas da Educação Básica - Cor/Raça Não Declarada |
| QT_MAT_BAS_BRANCA | Número de Matrículas da Educação Básica - Cor/Raça Branca |
| QT_MAT_BAS_PRETA | Número de Matrículas da Educação Básica - Cor/Raça Preta |
| QT_MAT_BAS_PARDA | Número de Matrículas da Educação Básica - Cor/Raça Parda |
| QT_MAT_BAS_AMARELA | Número de Matrículas da Educação Básica - Cor/Raça Amarela |
| QT_MAT_BAS_INDIGENA | Número de Matrículas da Educação Básica - Cor/Raça Indígena |
| QT_MAT_BAS_0_3 | Número de Matrículas da Educação Básica - Até 3 anos de idade |
| QT_MAT_BAS_4_5 | Número de Matrículas da Educação Básica - Entre 4 e 5 anos de idade |
| QT_MAT_BAS_6_10 | Número de Matrículas da Educação Básica - Entre 6 e 10 anos de idade |
| QT_MAT_BAS_11_14 | Número de Matrículas da Educação Básica - Entre 11 e 14 anos de idade |
| QT_MAT_BAS_15_17 | Número de Matrículas da Educação Básica - Entre 15 e 17 anos de idade |
| QT_MAT_BAS_18_MAIS | Número de Matrículas da Educação Básica - Com 18 ou mais anos de idade |
| QT_MAT_INF_INT | Número de Matrículas da Educação Infantil - Tempo Integral |
| QT_MAT_INF_CRE_INT | Número de Matrículas da Educação Infantil - Creche - Tempo Integral |
| QT_MAT_INF_PRE_INT | Número de Matrículas da Educação Infantil - Pré-Escola - Tempo Integral |
| QT_MAT_FUND_INT | Número de Matrículas do Ensino Fundamental - Tempo Integral |
| QT_MAT_FUND_AI_INT | Número de Matrículas do Ensino Fundamental - Anos Iniciais - Tempo Integral |
| QT_MAT_FUND_AF_INT | Número de Matrículas do Ensino Fundamental - Anos Finais - Tempo Integral |
| QT_MAT_MED_INT | Número de Matrículas do Ensino Médio - Tempo Integral |
| QT_MAT_BAS_EAD | Número de Matrículas da Educação Básica - Turno não aplicável  para turmas semipresenciais ou de Educação a Distância (EAD) |
| QT_MAT_BAS_D | Número de Matrículas da Educação Básica - Turno Diurno |
| QT_MAT_BAS_N | Número de Matrículas da Educação Básica - Turno Noturno |
| QT_MAT_ZR_URB | Número de Matrículas da Educação Básica - Localização/Zona de residência do Aluno - Urbana |
| QT_MAT_ZR_RUR | Número de Matrículas da Educação Básica - Localização/Zona de residência do Aluno - Rural |
| QT_MAT_ZR_NA | Número de Matrículas da Educação Básica - Localização/Zona de residência do Aluno - Não aplicável para alunos residentes no exterior |
| IN_INTERNET | Acesso à Internet |
| IN_BANDA_LARGA | Internet Banda Larga |
| IN_INTERNET_ALUNOS | Acesso à Internet - Para uso dos alunos |
| IN_ACESSO_INTERNET_COMPUTADOR | Equipamentos que os alunos usam para acessar a internet da escola - Computadores de mesa, portáteis e tablets da escola (no laboratório de informática, biblioteca, sala de aula etc.) |
| IN_ACES_INTERNET_DISP_PESSOAIS | Equipamentos que os alunos usam para acessar a internet da escola - Dispositivos pessoais (computadores portáteis, celulares, tablets etc.) |
| TP_REDE_LOCAL | Rede local de interligação de computadores |
| IN_LABORATORIO_INFORMATICA | Dependências físicas existentes e utilizadas na escola - Laboratório de informática |
| IN_COMPUTADOR | Equipamentos existentes na escola para uso técnico e administrativo - Computador |
| IN_DESKTOP_ALUNO | Computadores em uso pelos alunos - Computador de mesa (desktop) |
| QT_DESKTOP_ALUNO | Quantidade de computadores em uso pelos alunos - Computador de mesa (desktop) |
| IN_COMP_PORTATIL_ALUNO | Computadores em uso pelos alunos - Computador portátil |
| QT_COMP_PORTATIL_ALUNO | Quantidade de computadores em uso pelos alunos - Computador portátil |
| IN_TABLET_ALUNO | Computadores em uso pelos alunos - Tablet |
| QT_TABLET_ALUNO | Quantidade de computadores em uso pelos alunos - Tablet |
| IN_LOCAL_FUNC_PREDIO_ESCOLAR | Local de funcionamento da escola - Prédio Escolar |
| TP_OCUPACAO_PREDIO_ESCOLAR | Forma de ocupação do Prédio escolar |
| IN_LOCAL_FUNC_SOCIOEDUCATIVO | Local de funcionamento da escola - Unidade de Atendimento socioeducativo |
| IN_LOCAL_FUNC_UNID_PRISIONAL | Local de funcionamento da escola - Unidade Prisional |
| IN_LOCAL_FUNC_PRISIONAL_SOCIO | Local de funcionamento da escola - Unidade Prisional ou Unidade de atendimento socioeducativo |
| IN_LOCAL_FUNC_GALPAO | Local de funcionamento da escola - Galpão/Rancho/Paiol/Barracão |
| TP_OCUPACAO_GALPAO | Forma de ocupação do Galpão/Rancho/Paiol/Barracão |
| IN_LOCAL_FUNC_SALAS_OUTRA_ESC | Local de funcionamento da escola - Salas em outra escola |
| IN_LOCAL_FUNC_OUTROS | Local de funcionamento da escola - Outros |
| NU_ANO_CENSO | Ano do Censo |
| DT_ANO_LETIVO_INICIO | Início do ano letivo |
| DT_ANO_LETIVO_TERMINO | Término (previsão) do ano letivo |
| DURACAO_ANO_LETIVO | Descrição não encontrada |
| DURACAO_EM_DIAS | Descrição não encontrada |
| PC_TEMPO_INTEGRAL | Descrição não encontrada |
| INDICE_TEC | Descrição não encontrada |


```

| Nome da Variável | Descrição da Variável |
|---|---|
| CO\_ENTIDADE | Código da Escola |
| NO\_ENTIDADE | Nome da Escola |
| NO\_REGIAO | Nome da Região Geográfica |
| CO\_REGIAO | Código da Região Geográfica |
| NO\_UF | Nome da Unidade da Federação |
| SG\_UF | Sigla da Unidade da Federação |
| CO\_UF | Código da Unidade da Federação |
| NO\_MUNICIPIO | Nome do Município |
| CO\_MUNICIPIO | Código do Município |
| TP\_DEPENDENCIA | Dependência Administrativa |
| TP\_CATEGORIA\_ESCOLA\_PRIVADA | Categoria da escola privada |
| TP\_LOCALIZACAO | Localização |
| TP\_LOCALIZACAO\_DIFERENCIADA | Localização diferenciada da escola |
| TP\_SITUACAO\_FUNCIONAMENTO | Situação de funcionamento |
| IN\_PREDIO\_COMPARTILHADO | Prédio compartilhado com outra escola |
| CO\_ORGAO\_REGIONAL | Código do Órgão Regional de Ensino |
| CO\_ESCOLA\_SEDE\_VINCULADA | Código da escola sede |
| CO\_IES\_OFERTANTE | Código da IES vinculada à escola |
| QT\_MAT\_BAS | Número de Matrículas da Educação Básica |
| QT\_MAT\_INF | Número de Matrículas da Educação Infantil |
| QT\_MAT\_INF\_CRE | Número de Matrículas da Educação Infantil - Creche |
| QT\_MAT\_INF\_PRE | Número de Matrículas da Educação Infantil - Pré-Escola |
| QT\_MAT\_FUND | Número de Matrículas do Ensino Fundamental |
| QT\_MAT\_FUND\_AI | Número de Matrículas do Ensino Fundamental - Anos Iniciais |
| QT\_MAT\_FUND\_AF | Número de Matrículas do Ensino Fundamental - Anos Finais |
| QT\_MAT\_MED | Número de Matrículas do Ensino Médio |
| QT\_MAT\_FUND\_AI\_1 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 1º Ano |
| QT\_MAT\_FUND\_AI\_2 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 2º Ano |
| QT\_MAT\_FUND\_AI\_3 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 3º Ano |
| QT\_MAT\_FUND\_AI\_4 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 4º Ano |
| QT\_MAT\_FUND\_AI\_5 | Número de Matrículas do Ensino Fundamental - Anos Iniciais - 5º Ano |
| QT\_MAT\_FUND\_AF\_6 | Número de Matrículas do Ensino Fundamental - Anos Finais - 6º Ano |
| QT\_MAT\_FUND\_AF\_7 | Número de Matrículas do Ensino Fundamental - Anos Finais - 7º Ano |
| QT\_MAT\_FUND\_AF\_8 | Número de Matrículas do Ensino Fundamental - Anos Finais - 8º Ano |
| QT\_MAT\_FUND\_AF\_9 | Número de Matrículas do Ensino Fundamental - Anos Finais - 9º Ano |
| QT\_MAT\_BAS\_FEM | Número de Matrículas da Educação Básica - Feminino |
| QT\_MAT\_BAS\_MASC | Número de Matrículas da Educação Básica - Masculino |
| QT\_MAT\_BAS\_ND | Número de Matrículas da Educação Básica - Cor/Raça Não Declarada |
| QT\_MAT\_BAS\_BRANCA | Número de Matrículas da Educação Básica - Cor/Raça Branca |
| QT\_MAT\_BAS\_PRETA | Número de Matrículas da Educação Básica - Cor/Raça Preta |
| QT\_MAT\_BAS\_PARDA | Número de Matrículas da Educação Básica - Cor/Raça Parda |
| QT\_MAT\_BAS\_AMARELA | Número de Matrículas da Educação Básica - Cor/Raça Amarela |
| QT\_MAT\_BAS\_INDIGENA | Número de Matrículas da Educação Básica - Cor/Raça Indígena |
| QT\_MAT\_BAS\_0\_3 | Número de Matrículas da Educação Básica - Até 3 anos de idade |
| QT\_MAT\_BAS\_4\_5 | Número de Matrículas da Educação Básica - Entre 4 e 5 anos de idade |
| QT\_MAT\_BAS\_6\_10 | Número de Matrículas da Educação Básica - Entre 6 e 10 anos de idade |
| QT\_MAT\_BAS\_11\_14 | Número de Matrículas da Educação Básica - Entre 11 e 14 anos de idade |
| QT\_MAT\_BAS\_15\_17 | Número de Matrículas da Educação Básica - Entre 15 e 17 anos de idade |
| QT\_MAT\_BAS\_18\_MAIS | Número de Matrículas da Educação Básica - Com 18 ou mais anos de idade |
| QT\_MAT\_INF\_INT | Número de Matrículas da Educação Infantil - Tempo Integral |
| QT\_MAT\_INF\_CRE\_INT | Número de Matrículas da Educação Infantil - Creche - Tempo Integral |
| QT\_MAT\_INF\_PRE\_INT | Número de Matrículas da Educação Infantil - Pré-Escola - Tempo Integral |
| QT\_MAT\_FUND\_INT | Número de Matrículas do Ensino Fundamental - Tempo Integral |
| QT\_MAT\_FUND\_AI\_INT | Número de Matrículas do Ensino Fundamental - Anos Iniciais - Tempo Integral |
| QT\_MAT\_FUND\_AF\_INT | Número de Matrículas do Ensino Fundamental - Anos Finais - Tempo Integral |
| QT\_MAT\_MED\_INT | Número de Matrículas do Ensino Médio - Tempo Integral |
| QT\_MAT\_BAS\_EAD | Número de Matrículas da Educação Básica - Turno não aplicável para turmas semipresenciais ou de Educação a Distância (EAD) |
| QT\_MAT\_BAS\_D | Número de Matrículas da Educação Básica - Turno Diurno |
| QT\_MAT\_BAS\_N | Número de Matrículas da Educação Básica - Turno Noturno |
| QT\_MAT\_ZR\_URB | Número de Matrículas da Educação Básica - Localização/Zona de residência do Aluno - Urbana |
| QT\_MAT\_ZR\_RUR | Número de Matrículas da Educação Básica - Localização/Zona de residência do Aluno - Rural |
| QT\_MAT\_ZR\_NA | Número de Matrículas da Educação Básica - Localização/Zona de residência do Aluno - Não aplicável para alunos residentes no exterior |
| IN\_INTERNET | Acesso à Internet |
| IN\_BANDA\_LARGA | Internet Banda Larga |
| IN\_INTERNET\_ALUNOS | Acesso à Internet - Para uso dos alunos |
| IN\_ACESSO\_INTERNET\_COMPUTADOR | Equipamentos que os alunos usam para acessar a internet da escola - Computadores de mesa, portáteis e tablets da escola (no laboratório de informática, biblioteca, sala de aula etc.) |
| IN\_ACES\_INTERNET\_DISP\_PESSOAIS | Equipamentos que os alunos usam para acessar a internet da escola - Dispositivos pessoais (computadores portáteis, celulares, tablets etc.) |
| TP\_REDE\_LOCAL | Rede local de interligação de computadores |
| IN\_LABORATORIO\_INFORMATICA | Dependências físicas existentes e utilizadas na escola - Laboratório de informática |
| IN\_COMPUTADOR | Equipamentos existentes na escola para uso técnico e administrativo - Computador |
| IN\_DESKTOP\_ALUNO | Computadores em uso pelos alunos - Computador de mesa (desktop) |
| QT\_DESKTOP\_ALUNO | Quantidade de computadores em uso pelos alunos - Computador de mesa (desktop) |
| IN\_COMP\_PORTATIL\_ALUNO | Computadores em uso pelos alunos - Computador portátil |
| QT\_COMP\_PORTATIL\_ALUNO | Quantidade de computadores em uso pelos alunos - Computador portátil |
| IN\_TABLET\_ALUNO | Computadores em uso pelos alunos - Tablet |
| QT\_TABLET\_ALUNO | Quantidade de computadores em uso pelos alunos - Tablet |
| IN\_LOCAL\_FUNC\_PREDIO\_ESCOLAR | Local de funcionamento da escola - Prédio Escolar |
| TP\_OCUPACAO\_PREDIO\_ESCOLAR | Forma de ocupação do Prédio escolar |
| IN\_LOCAL\_FUNC\_SOCIOEDUCATIVO | Local de funcionamento da escola - Unidade de Atendimento socioeducativo |
| IN\_LOCAL\_FUNC\_UNID\_PRISIONAL | Local de funcionamento da escola - Unidade Prisional |
| IN\_LOCAL\_FUNC\_PRISIONAL\_SOCIO | Local de funcionamento da escola - Unidade Prisional ou Unidade de atendimento socioeducativo |
| IN\_LOCAL\_FUNC\_GALPAO | Local de funcionamento da escola - Galpão/Rancho/Paiol/Barracão |
| TP\_OCUPACAO\_GALPAO | Forma de ocupação do Galpão/Rancho/Paiol/Barracão |
| IN\_LOCAL\_FUNC\_SALAS\_OUTRA\_ESC | Local de funcionamento da escola - Salas em outra escola |
| IN\_LOCAL\_FUNC\_OUTROS | Local de funcionamento da escola - Outros |
| NU\_ANO\_CENSO | Ano do Censo |
| DT\_ANO\_LETIVO\_INICIO | Início do ano letivo |
| DT\_ANO\_LETIVO\_TERMINO | Término (previsão) do ano letivo |
| DURACAO\_ANO\_LETIVO | Descrição não encontrada |
| DURACAO\_EM\_DIAS | Descrição não encontrada |
| PC\_TEMPO\_INTEGRAL | Descrição não encontrada |
| INDICE\_TEC | Descrição não encontrada |

* **Justificativa da Escolha:**
    A seleção foi projetada para criar um subconjunto de dados coeso e otimizado para a análise do **perfil escolar e das condições de oferta de ensino**. A escolha não foi aleatória, mas sim agrupada em temas lógicos para responder a perguntas específicas:
    1.  **Identificação e Localização** (`CO_ENTIDADE`, `NO_MUNICIPIO`, `SG_UF`, etc.): Essencial para análises geográficas e para identificar cada unidade escolar de forma única. Permite comparar estados, regiões e municípios.
    2.  **Características Administrativas** (`TP_DEPENDENCIA`, `TP_LOCALIZACAO`, etc.): Crucial para segmentar as análises e comparar as realidades entre escolas públicas (municipais, estaduais) e privadas, bem como entre zonas urbana e rural.
    3.  **Matrículas** (`QT_MAT_...`): Representam o "coração" da análise, detalhando o corpo discente por etapa de ensino, perfil demográfico (sexo, cor/raça), faixa etária e modalidades especiais (como ensino em tempo integral).
    4.  **Infraestrutura e Tecnologia** (`IN_INTERNET`, `IN_LABORATORIO_INFORMATICA`, etc.): Permitem avaliar as condições físicas e tecnológicas oferecidas pelas escolas, possibilitando cruzar esses dados com o perfil de matrículas para identificar desigualdades.

    A remoção das demais colunas visa reduzir a complexidade e o ruído, focando em variáveis-chave que permitem uma análise robusta da relação entre **localização, infraestrutura e tecnologia e perfil dos estudantes**.