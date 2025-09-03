### Descrição das Features do Conjunto de Dados (Titanic)

Cada coluna (feature) no conjunto de dados representa uma característica de cada passageiro a bordo.

* **PassengerId:** Um identificador único para cada passageiro.
* **Survived:** O principal dado de resultado. Indica se o passageiro sobreviveu (1) ou não (0).
* **Pclass:** A classe do bilhete do passageiro. É uma variável categórica que pode indicar a classe social ou econômica (1 = Primeira Classe, 2 = Segunda Classe, 3 = Terceira Classe).
* **Name:** O nome completo do passageiro.
* **Sex:** O sexo do passageiro (masculino ou feminino).
* **Age:** A idade do passageiro em anos. Esta coluna é a principal que contém valores ausentes.
* **SibSp:** O número de irmãos/cônjuges a bordo com o passageiro.
* **Parch:** O número de pais/filhos a bordo com o passageiro.
* **Ticket:** O número do bilhete do passageiro.
* **Fare:** O valor da tarifa paga pelo bilhete.
* **Cabin:** O número da cabine do passageiro. Esta coluna contém uma grande quantidade de valores ausentes.
* **Embarked:** O porto de embarque do passageiro. Os portos são identificados por letras: C = Cherbourg, Q = Queenstown, S = Southampton. Esta coluna também pode ter valores ausentes.

---

### Análise de Fraude sob a Perspectiva de um Gestor de Seguros

Sendo um gestor de seguro que assegurou o Titanic, o tipo de informação a ser extraída dessa base de dados para observar fraudes seria:

#### 1. Rastreamento por Bilhete (Ticket)
* **Informação a ser analisada:** A coluna `Ticket` e, em particular, a quantidade de pessoas associadas a cada bilhete.
* **Análise de Fraude:** Fraudes de seguro podem envolver pessoas que não estavam a bordo, mas que reivindicam um bilhete para receber indenização. Eu cruzaria os dados de todos os bilhetes associados a uma mesma família ou grupo e verificaria se o número de sobreviventes declarados corresponde ao número de passageiros que realmente embarcaram com aquele bilhete. Se houver discrepância — como uma família inteira declarada como morta, mas com um ou mais membros aparecendo em listas de sobreviventes — isso seria um alerta.

#### 2. Padrões de Sobrevivência Inconsistentes
* **Informação a ser analisada:** As colunas `Survived`, `Age`, `Sex` e `Pclass`.
* **Análise de Fraude:** O padrão de sobrevivência no Titanic é bem conhecido: mulheres, crianças e passageiros da Primeira Classe tiveram taxas de sobrevivência muito maiores. Eu criaria relatórios para identificar:
    * **Homens que sobreviveram:** Se um homem da Terceira Classe, que teve as menores chances de sobrevivência, for listado como morto em uma reivindicação de seguro, mas aparecer como sobrevivente em outras listas ou testemunhos, isso levantaria uma bandeira vermelha.
    * **Discrepâncias de Idade:** A idade (`Age`) é um dado crucial. Um passageiro idoso ou uma criança pequena, que teriam mais dificuldade para chegar aos botes salva-vidas, mas que são reivindicados como sobreviventes por um familiar, mereceriam uma investigação mais detalhada. A fraude poderia estar na reivindicação do seguro de um passageiro que de fato morreu, mas cuja identidade é assumida por um sobrevivente para obter indenizações duplas ou indevidas.

#### 3. Análise da Cabine e Fatores de Risco (Cabin e Pclass)
* **Informação a ser analisada:** As colunas `Cabin` e `Pclass`.
* **Análise de Fraude:** O valor do seguro de um passageiro da Primeira Classe seria muito maior do que o de um da Terceira Classe. A coluna `Cabin`, embora com muitos valores ausentes, pode ser usada para cruzar informações. Uma reivindicação de seguro de alto valor para um passageiro que, segundo os registros, estava na Terceira Classe ou em uma cabine que não correspondia a um bilhete de Primeira Classe, seria um forte indício de fraude.