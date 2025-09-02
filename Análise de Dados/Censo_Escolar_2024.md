### Microdados do Censo da Educação Básica 2024

Sistema Inepdata, que também permite a execução de consultas sobre os principais dados da Educação Básica do país, inclusive ao nível de municípios:
[https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/inepdata/estatisticas-censo-escolar](https://www.google.com/search?q=https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/inepdata/estatisticas-censo-escolar)

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

* **Justificativa da Escolha:**
    A seleção foi projetada para criar um subconjunto de dados coeso e otimizado para a análise do **perfil escolar e das condições de oferta de ensino**. A escolha não foi aleatória, mas sim agrupada em temas lógicos para responder a perguntas específicas:
    1.  **Identificação e Localização** (`CO_ENTIDADE`, `NO_MUNICIPIO`, `SG_UF`, etc.): Essencial para análises geográficas e para identificar cada unidade escolar de forma única. Permite comparar estados, regiões e municípios.
    2.  **Características Administrativas** (`TP_DEPENDENCIA`, `TP_LOCALIZACAO`, etc.): Crucial para segmentar as análises e comparar as realidades entre escolas públicas (municipais, estaduais) e privadas, bem como entre zonas urbana e rural.
    3.  **Matrículas** (`QT_MAT_...`): Representam o "coração" da análise, detalhando o corpo discente por etapa de ensino, perfil demográfico (sexo, cor/raça), faixa etária e modalidades especiais (como ensino em tempo integral).
    4.  **Infraestrutura e Tecnologia** (`IN_INTERNET`, `IN_LABORATORIO_INFORMATICA`, etc.): Permitem avaliar as condições físicas e tecnológicas oferecidas pelas escolas, possibilitando cruzar esses dados com o perfil de matrículas para identificar desigualdades.

    A remoção das demais colunas visa reduzir a complexidade e o ruído, focando em variáveis-chave que permitem uma análise robusta da relação entre **localização, infraestrutura e tecnologia e perfil dos estudantes**.