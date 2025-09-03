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

```python?code_reference&code_event_index=2
import pandas as pd

# Load the data dictionary file, skipping the initial rows
try:
    df = pd.read_csv('dicionário_dados_educação_básica.xlsx - microdados_unidade_coleta.csv', skiprows=7)
except Exception as e:
    print(f"Error loading the file: {e}")
    # If the first attempt fails, try to read without skipping rows to inspect
    try:
        df = pd.read_csv('dicionário_dados_educação_básica.xlsx - microdados_unidade_coleta.csv')
        print("File loaded without skipping rows, showing first 5 rows:")
        print(df.head())
    except Exception as e2:
        print(f"Could not read the file at all: {e2}")
        df = None


if df is not None:
    # List of variables provided by the user
    variables = [
        'CO_ENTIDADE', 'NO_ENTIDADE', 'NO_REGIAO', 'CO_REGIAO', 'NO_UF', 'SG_UF', 'CO_UF',
        'NO_MUNICIPIO', 'CO_MUNICIPIO', 'TP_DEPENDENCIA', 'TP_CATEGORIA_ESCOLA_PRIVADA',
        'TP_LOCALIZACAO', 'TP_LOCALIZACAO_DIFERENCIADA', 'TP_SITUACAO_FUNCIONAMENTO',
        'IN_PREDIO_COMPARTILHADO', 'CO_ORGAO_REGIONAL', 'CO_ESCOLA_SEDE_VINCULADA',
        'CO_IES_OFERTANTE', 'QT_MAT_BAS', 'QT_MAT_INF', 'QT_MAT_INF_CRE', 'QT_MAT_INF_PRE',
        'QT_MAT_FUND', 'QT_MAT_FUND_AI', 'QT_MAT_FUND_AF', 'QT_MAT_MED', 'QT_MAT_FUND_AI_1',
        'QT_MAT_FUND_AI_2', 'QT_MAT_FUND_AI_3', 'QT_MAT_FUND_AI_4', 'QT_MAT_FUND_AI_5',
        'QT_MAT_FUND_AF_6', 'QT_MAT_FUND_AF_7', 'QT_MAT_FUND_AF_8', 'QT_MAT_FUND_AF_9',
        'QT_MAT_BAS_FEM', 'QT_MAT_BAS_MASC', 'QT_MAT_BAS_ND', 'QT_MAT_BAS_BRANCA',
        'QT_MAT_BAS_PRETA', 'QT_MAT_BAS_PARDA', 'QT_MAT_BAS_AMARELA', 'QT_MAT_BAS_INDIGENA',
        'QT_MAT_BAS_0_3', 'QT_MAT_BAS_4_5', 'QT_MAT_BAS_6_10', 'QT_MAT_BAS_11_14',
        'QT_MAT_BAS_15_17', 'QT_MAT_BAS_18_MAIS', 'QT_MAT_INF_INT', 'QT_MAT_INF_CRE_INT',
        'QT_MAT_INF_PRE_INT', 'QT_MAT_FUND_INT', 'QT_MAT_FUND_AI_INT', 'QT_MAT_FUND_AF_INT',
        'QT_MAT_MED_INT', 'QT_mat_bas_ead', 'QT_MAT_BAS_D', 'QT_MAT_BAS_N', 'QT_MAT_ZR_URB',
        'QT_MAT_ZR_RUR', 'QT_MAT_ZR_NA', 'IN_INTERNET', 'IN_BANDA_LARGA',
        'IN_INTERNET_ALUNOS', 'IN_ACESSO_INTERNET_COMPUTADOR',
        'IN_ACES_INTERNET_DISP_PESSOAIS', 'TP_REDE_LOCAL', 'IN_LABORATORIO_INFORMATICA',
        'IN_COMPUTADOR', 'IN_DESKTOP_ALUNO', 'QT_DESKTOP_ALUNO', 'IN_COMP_PORTATIL_ALUNO',
        'QT_COMP_PORTATIL_ALUNO', 'IN_TABLET_ALUNO', 'QT_TABLET_ALUNO',
        'IN_LOCAL_FUNC_PREDIO_ESCOLAR', 'TP_OCUPACAO_PREDIO_ESCOLAR',
        'IN_LOCAL_FUNC_SOCIOEDUCATIVO', 'IN_LOCAL_FUNC_UNID_prisional',
        'IN_LOCAL_FUNC_PRISIONAL_SOCIO', 'IN_LOCAL_FUNC_GALPAO', 'TP_OCUPACAO_GALPAO',
        'IN_LOCAL_FUNC_SALAS_OUTRA_ESC', 'IN_LOCAL_FUNC_OUTROS', 'NU_ANO_CENSO',
        'DT_ANO_LETIVO_INICIO', 'DT_ANO_LETIVO_TERMINO', 'DURACAO_ANO_LETIVO',
        'DURACAO_EM_DIAS', 'PC_TEMPO_INTEGRAL', 'INDICE_TEC'
    ]

    # Normalize variable names to uppercase for matching
    variables_upper = [v.upper() for v in variables]
    df['Nome da Variável'] = df['Nome da Variável'].str.upper()

    # Create the Markdown table
    markdown_table = "| Nome da Variável | Descrição da Variável |\n"
    markdown_table += "|---|---|\n"

    for var in variables_upper:
        description = df[df['Nome da Variável'] == var]['Descrição da Variável'].values
        if len(description) > 0:
            markdown_table += f"| {var} | {description[0]} |\n"
        else:
            # If variable not found, check the other file as a fallback.
            try:
                df_cursos = pd.read_csv('dicionário_dados_educação_básica.xlsx - suplemento_cursos_tecnicos.csv', skiprows=7)
                df_cursos['Nome da Variável'] = df_cursos['Nome da Variável'].str.upper()
                description_curso = df_cursos[df_cursos['Nome da Variável'] == var]['Descrição da Variável'].values
                if len(description_curso) > 0:
                    markdown_table += f"| {var} | {description_curso[0]} |\n"
                else:
                    markdown_table += f"| {var} | Descrição não encontrada |\n"
            except Exception as e:
                markdown_table += f"| {var} | Descrição não encontrada |\n"


    print(markdown_table)

```

```text?code_stderr&code_event_index=2
Traceback (most recent call last):
  File "<string>", line 50, in <module>
  File "frame.py", line 3807, in __getitem__
    indexer = self.columns.get_loc(key)
  File "base.py", line 3804, in get_loc
    raise KeyError(key) from err
KeyError: 'Nome da Variável'

The above exception was the direct cause of the following exception:

KeyError: 'Nome da Variável'

```

```python?code_reference&code_event_index=6
import pandas as pd

# Load the data dictionary file, skipping the initial rows
try:
    df = pd.read_csv('dicionário_dados_educação_básica.xlsx - microdados_unidade_coleta.csv', skiprows=7)
    print("Columns after loading with skiprows=7:")
    print(df.columns)
    print("\nFirst 5 rows of the dataframe:")
    print(df.head())

except Exception as e:
    print(f"Error loading the file: {e}")

# If the columns are not what we expect, let's try to load it differently.
# Based on the file snippets, the header seems to be at row 8 (index 7).
# Let's try to clean up column names if they have extra spaces or characters.
if 'Nome da Variável' not in df.columns:
    print("\n'Nome da Variável' not in columns. Let's try to clean them up.")
    df.columns = df.columns.str.strip()
    print("Cleaned columns:")
    print(df.columns)

# If still not found, there might be an issue with the file parsing itself.
# Let's proceed assuming the columns are now correct.

variables = [
    'CO_ENTIDADE', 'NO_ENTIDADE', 'NO_REGIAO', 'CO_REGIAO', 'NO_UF', 'SG_UF', 'CO_UF',
    'NO_MUNICIPIO', 'CO_MUNICIPIO', 'TP_DEPENDENCIA', 'TP_CATEGORIA_ESCOLA_PRIVADA',
    'TP_LOCALIZACAO', 'TP_LOCALIZACAO_DIFERENCIADA', 'TP_SITUACAO_FUNCIONAMENTO',
    'IN_PREDIO_COMPARTILHADO', 'CO_ORGAO_REGIONAL', 'CO_ESCOLA_SEDE_VINCULADA',
    'CO_IES_OFERTANTE', 'QT_MAT_BAS', 'QT_MAT_INF', 'QT_MAT_INF_CRE', 'QT_MAT_INF_PRE',
    'QT_MAT_FUND', 'QT_MAT_FUND_AI', 'QT_MAT_FUND_AF', 'QT_MAT_MED', 'QT_MAT_FUND_AI_1',
    'QT_MAT_FUND_AI_2', 'QT_MAT_FUND_AI_3', 'QT_MAT_FUND_AI_4', 'QT_MAT_FUND_AI_5',
    'QT_MAT_FUND_AF_6', 'QT_MAT_FUND_AF_7', 'QT_MAT_FUND_AF_8', 'QT_MAT_FUND_AF_9',
    'QT_MAT_BAS_FEM', 'QT_MAT_BAS_MASC', 'QT_MAT_BAS_ND', 'QT_MAT_BAS_BRANCA',
    'QT_MAT_BAS_PRETA', 'QT_MAT_BAS_PARDA', 'QT_MAT_BAS_AMARELA', 'QT_MAT_BAS_INDIGENA',
    'QT_MAT_BAS_0_3', 'QT_MAT_BAS_4_5', 'QT_MAT_BAS_6_10', 'QT_MAT_BAS_11_14',
    'QT_MAT_BAS_15_17', 'QT_MAT_BAS_18_MAIS', 'QT_MAT_INF_INT', 'QT_MAT_INF_CRE_INT',
    'QT_MAT_INF_PRE_INT', 'QT_MAT_FUND_INT', 'QT_MAT_FUND_AI_INT', 'QT_MAT_FUND_AF_INT',
    'QT_MAT_MED_INT', 'QT_MAT_BAS_EAD', 'QT_MAT_BAS_D', 'QT_MAT_BAS_N', 'QT_MAT_ZR_URB',
    'QT_MAT_ZR_RUR', 'QT_MAT_ZR_NA', 'IN_INTERNET', 'IN_BANDA_LARGA',
    'IN_INTERNET_ALUNOS', 'IN_ACESSO_INTERNET_COMPUTADOR',
    'IN_ACES_INTERNET_DISP_PESSOAIS', 'TP_REDE_LOCAL', 'IN_LABORATORIO_INFORMATICA',
    'IN_COMPUTADOR', 'IN_DESKTOP_ALUNO', 'QT_DESKTOP_ALUNO', 'IN_COMP_PORTATIL_ALUNO',
    'QT_COMP_PORTATIL_ALUNO', 'IN_TABLET_ALUNO', 'QT_TABLET_ALUNO',
    'IN_LOCAL_FUNC_PREDIO_ESCOLAR', 'TP_OCUPACAO_PREDIO_ESCOLAR',
    'IN_LOCAL_FUNC_SOCIOEDUCATIVO', 'IN_LOCAL_FUNC_UNID_PRISIONAL',
    'IN_LOCAL_FUNC_PRISIONAL_SOCIO', 'IN_LOCAL_FUNC_GALPAO', 'TP_OCUPACAO_GALPAO',
    'IN_LOCAL_FUNC_SALAS_OUTRA_ESC', 'IN_LOCAL_FUNC_OUTROS', 'NU_ANO_CENSO',
    'DT_ANO_LETIVO_INICIO', 'DT_ANO_LETIVO_TERMINO', 'DURACAO_ANO_LETIVO',
    'DURACAO_EM_DIAS', 'PC_TEMPO_INTEGRAL', 'INDICE_TEC'
]

# Normalize variable names to uppercase for matching
variables_upper = [v.upper() for v in variables]

# Use the correct column names based on debugging output
variable_col_name = 'Nome da Variável'
description_col_name = 'Descrição da Variável'

# Check if columns exist before proceeding
if variable_col_name in df.columns and description_col_name in df.columns:
    df[variable_col_name] = df[variable_col_name].str.upper()

    # Create the Markdown table
    markdown_table = f"| {variable_col_name} | {description_col_name} |\n"
    markdown_table += "|---|---|\n"

    for var in variables_upper:
        description = df[df[variable_col_name] == var][description_col_name].values
        if len(description) > 0:
            markdown_table += f"| {var} | {description[0]} |\n"
        else:
            # If variable not found, check the other file as a fallback.
            try:
                df_cursos = pd.read_csv('dicionário_dados_educação_básica.xlsx - suplemento_cursos_tecnicos.csv', skiprows=7)
                df_cursos.columns = df_cursos.columns.str.strip() # Clean column names
                if variable_col_name in df_cursos.columns and description_col_name in df_cursos.columns:
                    df_cursos[variable_col_name] = df_cursos[variable_col_name].str.upper()
                    description_curso = df_cursos[df_cursos[variable_col_name] == var][description_col_name].values
                    if len(description_curso) > 0:
                        markdown_table += f"| {var} | {description_curso[0]} |\n"
                    else:
                        markdown_table += f"| {var} | Descrição não encontrada |\n"
                else:
                    markdown_table += f"| {var} | Descrição não encontrada |\n"
            except Exception as e:
                markdown_table += f"| {var} | Descrição não encontrada |\n"

    print(markdown_table)
else:
    print(f"'{variable_col_name}' or '{description_col_name}' not found in the dataframe columns.")
```

```text?code_stdout&code_event_index=6
Columns after loading with skiprows=7:
Index(['Unnamed: 0', 'Unnamed: 1', 'Unnamed: 2', 'Unnamed: 3', 'Unnamed: 4',
       'Unnamed: 5', '07', '08', '09', '10', '11', '12', '13', '14', '15',
       '16', '17', '18', '19', '20', '21', '22', '23', '24', 'Unnamed: 24'],
      dtype='object')

First 5 rows of the dataframe:
  Unnamed: 0    Unnamed: 1                    Unnamed: 2 Unnamed: 3  Unnamed: 4 Unnamed: 5   07   08   09   10   11   12   13   14   15   16   17   18   19   20   21   22   23   24 Unnamed: 24
0        NaN           NaN                           NaN        NaN         NaN        NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN         NaN
1          1  NU_ANO_CENSO                  Ano do Censo        Num         4.0        NaN    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s         NaN
2          2     NO_REGIAO     Nome da Região Geográfica       Char        20.0        NaN    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s         NaN
3          3     CO_REGIAO   Código da Região Geográfica        Num         1.0        NaN    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s         NaN
4          4         NO_UF  Nome da Unidade da Federação       Char        50.0        NaN    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s         NaN

'Nome da Variável' not in columns. Let's try to clean them up.
Cleaned columns:
Index(['Unnamed: 0', 'Unnamed: 1', 'Unnamed: 2', 'Unnamed: 3', 'Unnamed: 4',
       'Unnamed: 5', '07', '08', '09', '10', '11', '12', '13', '14', '15',
       '16', '17', '18', '19', '20', '21', '22', '23', '24', 'Unnamed: 24'],
      dtype='object')
'Nome da Variável' or 'Descrição da Variável' not found in the dataframe columns.

```

```python?code_reference&code_event_index=10
import pandas as pd

# Load the data dictionary files, setting the correct header row
try:
    df_microdados = pd.read_csv('dicionário_dados_educação_básica.xlsx - microdados_unidade_coleta.csv', header=7)
    df_cursos = pd.read_csv('dicionário_dados_educação_básica.xlsx - suplemento_cursos_tecnicos.csv', header=7)

    # Clean up column names by stripping leading/trailing whitespace
    df_microdados.columns = df_microdados.columns.str.strip()
    df_cursos.columns = df_cursos.columns.str.strip()

except Exception as e:
    print(f"Error loading the files: {e}")
    df_microdados = None
    df_cursos = None


if df_microdados is not None and df_cursos is not None:
    variables = [
        'CO_ENTIDADE', 'NO_ENTIDADE', 'NO_REGIAO', 'CO_REGIAO', 'NO_UF', 'SG_UF', 'CO_UF',
        'NO_MUNICIPIO', 'CO_MUNICIPIO', 'TP_DEPENDENCIA', 'TP_CATEGORIA_ESCOLA_PRIVADA',
        'TP_LOCALIZACAO', 'TP_LOCALIZACAO_DIFERENCIADA', 'TP_SITUACAO_FUNCIONAMENTO',
        'IN_PREDIO_COMPARTILHADO', 'CO_ORGAO_REGIONAL', 'CO_ESCOLA_SEDE_VINCULADA',
        'CO_IES_OFERTANTE', 'QT_MAT_BAS', 'QT_MAT_INF', 'QT_MAT_INF_CRE', 'QT_MAT_INF_PRE',
        'QT_MAT_FUND', 'QT_MAT_FUND_AI', 'QT_MAT_FUND_AF', 'QT_MAT_MED', 'QT_MAT_FUND_AI_1',
        'QT_MAT_FUND_AI_2', 'QT_MAT_FUND_AI_3', 'QT_MAT_FUND_AI_4', 'QT_MAT_FUND_AI_5',
        'QT_MAT_FUND_AF_6', 'QT_MAT_FUND_AF_7', 'QT_MAT_FUND_AF_8', 'QT_MAT_FUND_AF_9',
        'QT_MAT_BAS_FEM', 'QT_MAT_BAS_MASC', 'QT_MAT_BAS_ND', 'QT_MAT_BAS_BRANCA',
        'QT_MAT_BAS_PRETA', 'QT_MAT_BAS_PARDA', 'QT_MAT_BAS_AMARELA', 'QT_MAT_BAS_INDIGENA',
        'QT_MAT_BAS_0_3', 'QT_MAT_BAS_4_5', 'QT_MAT_BAS_6_10', 'QT_MAT_BAS_11_14',
        'QT_MAT_BAS_15_17', 'QT_MAT_BAS_18_MAIS', 'QT_MAT_INF_INT', 'QT_MAT_INF_CRE_INT',
        'QT_MAT_INF_PRE_INT', 'QT_MAT_FUND_INT', 'QT_MAT_FUND_AI_INT', 'QT_MAT_FUND_AF_INT',
        'QT_MAT_MED_INT', 'QT_MAT_BAS_EAD', 'QT_MAT_BAS_D', 'QT_MAT_BAS_N', 'QT_MAT_ZR_URB',
        'QT_MAT_ZR_RUR', 'QT_MAT_ZR_NA', 'IN_INTERNET', 'IN_BANDA_LARGA',
        'IN_INTERNET_ALUNOS', 'IN_ACESSO_INTERNET_COMPUTADOR',
        'IN_ACES_INTERNET_DISP_PESSOAIS', 'TP_REDE_LOCAL', 'IN_LABORATORIO_INFORMATICA',
        'IN_COMPUTADOR', 'IN_DESKTOP_ALUNO', 'QT_DESKTOP_ALUNO', 'IN_COMP_PORTATIL_ALUNO',
        'QT_COMP_PORTATIL_ALUNO', 'IN_TABLET_ALUNO', 'QT_TABLET_ALUNO',
        'IN_LOCAL_FUNC_PREDIO_ESCOLAR', 'TP_OCUPACAO_PREDIO_ESCOLAR',
        'IN_LOCAL_FUNC_SOCIOEDUCATIVO', 'IN_LOCAL_FUNC_UNID_PRISIONAL',
        'IN_LOCAL_FUNC_PRISIONAL_SOCIO', 'IN_LOCAL_FUNC_GALPAO', 'TP_OCUPACAO_GALPAO',
        'IN_LOCAL_FUNC_SALAS_OUTRA_ESC', 'IN_LOCAL_FUNC_OUTROS', 'NU_ANO_CENSO',
        'DT_ANO_LETIVO_INICIO', 'DT_ANO_LETIVO_TERMINO', 'DURACAO_ANO_LETIVO',
        'DURACAO_EM_DIAS', 'PC_TEMPO_INTEGRAL', 'INDICE_TEC'
    ]

    # Normalize variable names to uppercase for matching
    variables_upper = [v.upper() for v in variables]
    
    variable_col_name = 'Nome da Variável'
    description_col_name = 'Descrição da Variável'

    # Ensure the required columns exist
    if variable_col_name in df_microdados.columns and description_col_name in df_microdados.columns:
        df_microdados[variable_col_name] = df_microdados[variable_col_name].str.upper()
    if variable_col_name in df_cursos.columns and description_col_name in df_cursos.columns:
        df_cursos[variable_col_name] = df_cursos[variable_col_name].str.upper()


    # Create the Markdown table
    markdown_table = f"| {variable_col_name} | {description_col_name} |\n"
    markdown_table += "|---|---|\n"

    for var in variables_upper:
        description = df_microdados[df_microdados[variable_col_name] == var][description_col_name].values
        if len(description) > 0:
            markdown_table += f"| {var} | {description[0]} |\n"
        else:
            description_curso = df_cursos[df_cursos[variable_col_name] == var][description_col_name].values
            if len(description_curso) > 0:
                markdown_table += f"| {var} | {description_curso[0]} |\n"
            else:
                markdown_table += f"| {var} | Descrição não encontrada |\n"

    print(markdown_table)
```

```text?code_stderr&code_event_index=10
Traceback (most recent call last):
  File "<string>", line 65, in <module>
  File "frame.py", line 3807, in __getitem__
    indexer = self.columns.get_loc(key)
  File "base.py", line 3804, in get_loc
    raise KeyError(key) from err
KeyError: 'Nome da Variável'

The above exception was the direct cause of the following exception:

KeyError: 'Nome da Variável'

```

```python?code_reference&code_event_index=14
import pandas as pd

# Load the data dictionary file without a header to inspect its structure
try_df = pd.read_csv('dicionário_dados_educação_básica.xlsx - microdados_unidade_coleta.csv', header=None)
print("First 10 rows of the dataframe, loaded with header=None:")
print(try_df.head(10))

# From the output, we can see the header is on row 7 (0-indexed).
# Let's reload with header=7 and check the columns.
df_microdados = pd.read_csv('dicionário_dados_educação_básica.xlsx - microdados_unidade_coleta.csv', header=7)
print("\nColumns of df_microdados after loading with header=7:")
print(df_microdados.columns)

df_cursos = pd.read_csv('dicionário_dados_educação_básica.xlsx - suplemento_cursos_tecnicos.csv', header=7)
print("\nColumns of df_cursos after loading with header=7:")
print(df_cursos.columns)


# It appears that there are unnamed columns that are being created. Let's find the correct column names for "Nome da Variável" and "Descrição da Variável".
# From the previous attempt, the correct columns seem to be at index 1 and 2 of the original file without header.
# Let's rename the columns to what we expect.

df_microdados.columns = ['N', 'Nome da Variável', 'Descrição da Variável', 'Tipo', 'Tam.(1)', 'Categoria', '07', '08', '09', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24', 'Notas Importantes']
df_cursos.columns = ['N', 'Nome da Variável', 'Descrição da Variável', 'Tipo', 'Tam.(1)', 'Categoria', '07', '08', '09', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24', 'Notas Importantes']


variables = [
    'CO_ENTIDADE', 'NO_ENTIDADE', 'NO_REGIAO', 'CO_REGIAO', 'NO_UF', 'SG_UF', 'CO_UF',
    'NO_MUNICIPIO', 'CO_MUNICIPIO', 'TP_DEPENDENCIA', 'TP_CATEGORIA_ESCOLA_PRIVADA',
    'TP_LOCALIZACAO', 'TP_LOCALIZACAO_DIFERENCIADA', 'TP_SITUACAO_FUNCIONAMENTO',
    'IN_PREDIO_COMPARTILHADO', 'CO_ORGAO_REGIONAL', 'CO_ESCOLA_SEDE_VINCULADA',
    'CO_IES_OFERTANTE', 'QT_MAT_BAS', 'QT_MAT_INF', 'QT_MAT_INF_CRE', 'QT_MAT_INF_PRE',
    'QT_MAT_FUND', 'QT_MAT_FUND_AI', 'QT_MAT_FUND_AF', 'QT_MAT_MED', 'QT_MAT_FUND_AI_1',
    'QT_MAT_FUND_AI_2', 'QT_MAT_FUND_AI_3', 'QT_MAT_FUND_AI_4', 'QT_MAT_FUND_AI_5',
    'QT_MAT_FUND_AF_6', 'QT_MAT_FUND_AF_7', 'QT_MAT_FUND_AF_8', 'QT_MAT_FUND_AF_9',
    'QT_MAT_BAS_FEM', 'QT_MAT_BAS_MASC', 'QT_MAT_BAS_ND', 'QT_MAT_BAS_BRANCA',
    'QT_MAT_BAS_PRETA', 'QT_MAT_BAS_PARDA', 'QT_MAT_BAS_AMARELA', 'QT_MAT_BAS_INDIGENA',
    'QT_MAT_BAS_0_3', 'QT_MAT_BAS_4_5', 'QT_MAT_BAS_6_10', 'QT_MAT_BAS_11_14',
    'QT_MAT_BAS_15_17', 'QT_MAT_BAS_18_MAIS', 'QT_MAT_INF_INT', 'QT_MAT_INF_CRE_INT',
    'QT_MAT_INF_PRE_INT', 'QT_MAT_FUND_INT', 'QT_MAT_FUND_AI_INT', 'QT_MAT_FUND_AF_INT',
    'QT_MAT_MED_INT', 'QT_MAT_BAS_EAD', 'QT_MAT_BAS_D', 'QT_MAT_BAS_N', 'QT_MAT_ZR_URB',
    'QT_MAT_ZR_RUR', 'QT_MAT_ZR_NA', 'IN_INTERNET', 'IN_BANDA_LARGA',
    'IN_INTERNET_ALUNOS', 'IN_ACESSO_INTERNET_COMPUTADOR',
    'IN_ACES_INTERNET_DISP_PESSOAIS', 'TP_REDE_LOCAL', 'IN_LABORATORIO_INFORMATICA',
    'IN_COMPUTADOR', 'IN_DESKTOP_ALUNO', 'QT_DESKTOP_ALUNO', 'IN_COMP_PORTATIL_ALUNO',
    'QT_COMP_PORTATIL_ALUNO', 'IN_TABLET_ALUNO', 'QT_TABLET_ALUNO',
    'IN_LOCAL_FUNC_PREDIO_ESCOLAR', 'TP_OCUPACAO_PREDIO_ESCOLAR',
    'IN_LOCAL_FUNC_SOCIOEDUCATIVO', 'IN_LOCAL_FUNC_UNID_PRISIONAL',
    'IN_LOCAL_FUNC_PRISIONAL_SOCIO', 'IN_LOCAL_FUNC_GALPAO', 'TP_OCUPACAO_GALPAO',
    'IN_LOCAL_FUNC_SALAS_OUTRA_ESC', 'IN_LOCAL_FUNC_OUTROS', 'NU_ANO_CENSO',
    'DT_ANO_LETIVO_INICIO', 'DT_ANO_LETIVO_TERMINO', 'DURACAO_ANO_LETIVO',
    'DURACAO_EM_DIAS', 'PC_TEMPO_INTEGRAL', 'INDICE_TEC'
]

# Normalize variable names to uppercase for matching
variables_upper = [v.upper() for v in variables]
df_microdados['Nome da Variável'] = df_microdados['Nome da Variável'].str.upper().str.strip()
df_cursos['Nome da Variável'] = df_cursos['Nome da Variável'].str.upper().str.strip()

# Create the Markdown table
markdown_table = "| Nome da Variável | Descrição da Variável |\n"
markdown_table += "|---|---|\n"

for var in variables_upper:
    description = df_microdados[df_microdados['Nome da Variável'] == var]['Descrição da Variável'].values
    if len(description) > 0:
        markdown_table += f"| {var} | {description[0]} |\n"
    else:
        description_curso = df_cursos[df_cursos['Nome da Variável'] == var]['Descrição da Variável'].values
        if len(description_curso) > 0:
            markdown_table += f"| {var} | {description_curso[0]} |\n"
        else:
            markdown_table += f"| {var} | Descrição não encontrada |\n"

print(markdown_table)
```

```text?code_stdout&code_event_index=14
First 10 rows of the dataframe, loaded with header=None:
                                            0                                                    1                      2     3        4          5                                   6    7    8    9    10   11   12   13   14   15   16   17   18   19   20   21   22   23                 24
0                                          NaN  Alteração de nomenclatura ou metodologia de cálculo                    NaN   NaN      NaN        NaN                                 NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN                NaN
1                                          NaN                                        Variável nova                    NaN   NaN      NaN        NaN                                 NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN                NaN
2                                          NaN                                      Descontinuidade                    NaN   NaN      NaN        NaN                                 NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN                NaN
3  Dicionário de Variáveis - Tabela de Escolas                                                  NaN                    NaN   NaN      NaN        NaN                                 NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN                NaN
4                                          NaN                                                  NaN                    NaN   NaN      NaN        NaN                                 NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN                NaN
5                                          NaN                                                  NaN                    NaN   NaN      NaN        NaN                                 NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN                NaN
6                                            N                                     Nome da Variável  Descrição da Variável  Tipo  Tam.(1)  Categoria  Coleta por ano ("s"=sim;"n"=não )   NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  Notas Importantes
7                                          NaN                                                  NaN                    NaN   NaN      NaN        NaN                                  07   08   09   10   11   12   13   14   15   16   17   18   19   20   21   22   23   24                NaN
8                                          NaN                                                  NaN                    NaN   NaN      NaN        NaN                                 NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN  NaN                NaN
9                                            1                                         NU_ANO_CENSO           Ano do Censo   Num        4        NaN                                   s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s    s                NaN

Columns of df_microdados after loading with header=7:
Index(['Unnamed: 0', 'Unnamed: 1', 'Unnamed: 2', 'Unnamed: 3', 'Unnamed: 4',
       'Unnamed: 5', '07', '08', '09', '10', '11', '12', '13', '14', '15',
       '16', '17', '18', '19', '20', '21', '22', '23', '24', 'Unnamed: 24'],
      dtype='object')

Columns of df_cursos after loading with header=7:
Index(['Unnamed: 0', 'Unnamed: 1', 'Unnamed: 2', 'Unnamed: 3', 'Unnamed: 4',
       'Unnamed: 5', '07', '08', '09', '10', '11', '12', '13', '14', '15',
       '16', '17', '18', '19', '20', '21', '22', '23', '24', 'Unnamed: 24'],
      dtype='object')
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