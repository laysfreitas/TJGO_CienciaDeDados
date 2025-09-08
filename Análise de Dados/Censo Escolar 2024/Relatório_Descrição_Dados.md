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

* **Seleção de Colunas:** Do conjunto total de variáveis, foi realizada uma seleção estratégica de **73 colunas**.

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
| QT_MAT_BAS | Número de Matrículas da Educação Básica |
| QT_MAT_INF | Número de Matrículas da Educação Infantil |
| QT_MAT_INF_CRE | Número de Matrículas da Educação Infantil - Creche |
| QT_MAT_INF_PRE | Número de Matrículas da Educação Infantil - Pré-Escola |
| QT_MAT_FUND | Número de Matrículas do Ensino Fundamental |
| QT_MAT_FUND_AI | Número de Matrículas do Ensino Fundamental - Anos Iniciais |
| QT_MAT_FUND_AF | Número de Matrículas do Ensino Fundamental - Anos Finais |
| QT_MAT_MED | Número de Matrículas do Ensino Médio |
| QT_MAT_BAS_FEM | Número de Matrículas da Educação Básica - Feminino |
| QT_MAT_BAS_MASC | Número de Matrículas da Educação Básica - Masculino |
| QT_MAT_BAS_ND | Número de Matrículas da Educação Básica - Cor/Raça Não Declarada |
| QT_MAT_BAS_BRANCA | Número de Matrículas da Educação Básica - Cor/Raça Branca |
| QT_MAT_BAS_PRETA | Número de Matrículas da Educação Básica - Cor/Raça Preta |
| QT_MAT_BAS_PARDA | Número de Matrículas da Educação Básica - Cor/Raça Parda |
| QT_MAT_BAS_AMARELA | Número de Matrículas da Educação Básica - Cor/Raça Amarela |
| QT_MAT_BAS_INDIGENA | Número de Matrículas da Educação Básica - Cor/Raça Indígena |
| QT_MAT_INF_INT | Número de Matrículas da Educação Infantil - Tempo Integral |
| QT_MAT_INF_CRE_INT | Número de Matrículas da Educação Infantil - Creche - Tempo Integral |
| QT_MAT_INF_PRE_INT | Número de Matrículas da Educação Infantil - Pré-Escola - Tempo Integral |
| QT_MAT_FUND_INT | Número de Matrículas do Ensino Fundamental - Tempo Integral |
| QT_MAT_FUND_AI_INT | Número de Matrículas do Ensino Fundamental - Anos Iniciais - Tempo Integral |
| QT_MAT_FUND_AF_INT | Número de Matrículas do Ensino Fundamental - Anos Finais - Tempo Integral |
| QT_MAT_MED_INT | Número de Matrículas do Ensino Médio - Tempo Integral |
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
| QT_DESKTOP_ALUNO | Quantidade de computadores em uso pelos alunos - Computador de mesa (desktop) |
| QT_COMP_PORTATIL_ALUNO | Quantidade de computadores em uso pelos alunos - Computador portátil |
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

* **Justificativa da Escolha:**
    A seleção foi projetada para criar um subconjunto de dados coeso e otimizado para a análise do **perfil escolar e das condições de oferta de ensino**. A escolha não foi aleatória, mas sim agrupada em temas lógicos para responder a perguntas específicas:
    1.  **Identificação e Localização** (`CO_ENTIDADE`, `NO_MUNICIPIO`, `SG_UF`, etc.): Essencial para análises geográficas e para identificar cada unidade escolar de forma única. Permite comparar estados, regiões e municípios.
    2.  **Características Administrativas** (`TP_DEPENDENCIA`, `TP_LOCALIZACAO`, etc.): Crucial para segmentar as análises e comparar as realidades entre escolas públicas (municipais, estaduais) e privadas, bem como entre zonas urbana e rural.
    3.  **Matrículas** (`QT_MAT_...`): Representam o "coração" da análise, detalhando o corpo discente por etapa de ensino, perfil demográfico (sexo, cor/raça), faixa etária e modalidades especiais (como ensino em tempo integral).
    4.  **Infraestrutura e Tecnologia** (`IN_INTERNET`, `IN_LABORATORIO_INFORMATICA`, etc.): Permitem avaliar as condições físicas e tecnológicas oferecidas pelas escolas, possibilitando cruzar esses dados com o perfil de matrículas para identificar desigualdades.

    A remoção das demais colunas visa reduzir a complexidade e o ruído, focando em variáveis-chave que permitem uma análise robusta da relação entre **localização, infraestrutura e tecnologia e perfil dos estudantes**.