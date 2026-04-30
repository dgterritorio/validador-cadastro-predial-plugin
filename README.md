# validador-cadastro-predial-plugin


## Plugin QGIS para validar os dados do ficheiro Geopackage a submeter na Plataforma de Conservação de Cadastro Predial do Sistema Nacional de Informação Cadastral [SNIC](https://www.dgterritorio.gov.pt/snic)

Para apoio aos Técnicos de Cadastro Predial (TCP) na preparação do ficheiro geopackage a submeter na [Plataforma de Conservação de Cadastro Predial](https://snic.dgterritorio.gov.pt/CNS/#/pt-PT/0/CNS/Home), no âmbito das operações de conservação cadastral, é disponibilizado pela Direção-Geral do Território um plugin para o software livre QGIS.

Este plugin permite auxiliar o Técnico de Cadastro Predial na preparação do ficheiro Geopackage, permitindo a deteção de inconformidades topológicas, bem como a sua correção automática. 

## Requisitos
O plugin deve ser instalado numa versão do QGIS 3.40 ou superior.

## Baixe o plugin CadEditCheck_CNS
O plugin está disponível em [CadEditCheck_CNS]( https://github.com/dgterritorio/validador-cadastro-predial-plugin/releases/download/V1.0.0/CadEditCheck_CNS.zip)

## Instalar o plugin
Para instalar o plugin, escolha no menu a opção Plugins → Gerir e instalar plugins...
1.	Escolha a opção "Instalar de um ZIP"
2.	Escolha o arquivo CadEditCheck_CNS.zip em "Ficheiro ZIP:"
3.	Procedimento de instalação, pressionando o botão Instalar plugin

O plugin depois de instalado fica disponível no menu Plugins.

<img width="443" height="74" alt="image" src="https://github.com/user-attachments/assets/e6abf1c8-39e1-4a21-83a7-245f610157d5" />
</p>
<img width="443" height="199" alt="image" src="https://github.com/user-attachments/assets/9388cf4e-f523-4aec-95be-8635ddd2663c" /></p>
<img width="443" height="199" alt="image" src="https://github.com/user-attachments/assets/0b04c690-6e7e-4b5e-9c6d-44a0e6298b74" /></p>


# Utilização do plugin
O plugin tem duas funcionalidades distintas e, por isso, tem desde logo dois separadores (Edição/Validação), dependendo se pretender, corrigir o ficheiro Geopackage ou verificar a sua conformidade.

# Separador Edição
Esta opção permite corrigir inconsistências nos polígonos.

<img width="443" height="394" alt="image" src="https://github.com/user-attachments/assets/054f9103-a45e-4bf8-ac18-2c03b72c37d1" />


## Edição do ficheiro geopackage

Sobre o ficheiro Geopackage a corrigir são realizadas um conjunto de correções automáticas com o objetivo de eliminar o maior número de inconsistências possível.

Correções automáticas:
 * Ajustar as geometrias entre si do ficheiro Geopackage a corrigir.
 * Ajustar as geometrias dos confinantes a corrigir aos confinantes originais.
 * Remover vértices duplicados.
 * Corrigir geometrias inválidas.
 * Converter as geometrias do tipo multipolígono para o tipo polígono.
 * Converter as geometrias do Geopackage de 3D para 2D.
 * Remover registos sem geometria.

## Utilização do separador Edição
* Aceder ao separador Edição.
* Ativar a opção “Corrigir os dados”.
* Clicar em “Geopackage Original” para identificar o ficheiro Geopackage com a representação dos dados originais disponibilizado na    Plataforma de Conservação.
* Clicar em “Geopackage a Corrigir” para Identificar o ficheiro Geopackage com a representação dos novos dados a corrigir.
* Para executar clicar em “OK”.
* Como resultado é adicionado ao projeto QGIS o novo Geopackage corrigido.
* O novo Geopackage é guardado na mesma pasta do "Geopackage a Corrigir", com a designação do "Geopackage a Corrigir" +         "_corrigido.gpkg". Por exemplo: se o ficheiro a corrigir tem a designação "dados.gpkg" o nome do ficheiro corrigido terá a   designação "dados_corrigido.gpkg".

## Descrição sobre cada uma das correções:

### Remover vértices duplicados
Elimina vértices (nós) duplicados de cada geometria, garantindo que não resultem geometrias não válidas. O procedimento implica a utilização de uma tolerância, neste caso 0, que determina quando os vértices são iguais.

### Corrigir geometrias inválidas
Garantir que todas as geometrias representadas no ficheiro Geopackage a corrigir são válidas.
  Tipos de erros mais comuns:
  * Auto intersecção
  * Auto contato
  Em alguns casos, geometrias muito complexas podem exigir uma edição manual após a correção automática.

### Ajustar as geometrias dos polígonos
O ajuste é realizado com base numa tolerância (0.001 metros) e segundo o modo de ajuste “Preferir alinhar nós, inserir vértices extra quando necessário”. Sempre que possível, fazer coincidir vértices entre os segmentos comuns de polígonos confinantes. Se os segmentos comuns não partiharem os mesmos vértices adiciona novos vértices de modo a assegurar a continuidade topológica entre polígonos (sem lacunas nem sobreposições).

### Ajustar as geometrias submetidas entre si
Garantir que não existem sobreposições nem lacunas, inferiores a 0.001 metros, entre todas as geometrias de polígonos no ficheiro geopackage a corrigir. É realizado um ajuste entre as geometrias da própria camada, e com todas as  restantes camadas.

### Ajustar as geometrias dos confinantes submetidos aos confinantes originais
Garantir que não existem diferenças inferiores a 0.001 metros entre os polígonos dos confinantes submetidos e os confinantes originais. É realizado um ajuste entre as geometrias dos confinantes submetidos com as geometrias dos   confinantes originais.

### Remover registos sem geometria
Na situação de existirem registos sem geometria associada estes são eliminados.

### Ficheiro GeoPackage corrigido
Como resultado dos procedimentos automáticos aplicados, o novo ficheiro geopackage contém exclusivamente geometrias bidimensionais (2D) do tipo polígono.


# Separador de Validação
Esta opção permite identificar os critérios que não estão a ser cumpridos, e que estão definidos na etapa 5 - Validação, da Plataforma de Conservação Cadastral Predial

<img width="886" height="802" alt="image" src="https://github.com/user-attachments/assets/5a8b2254-0dbd-4a9a-b213-01b6de8194c9" />


As Validações geometricas e não geométricas a efetuar sobre o ficheiro GeoPackage a submeter abrangem os seguintes parâmetros:

Validações não geométricas:
* Formato 
* Sistema de referência
* Número e nome das camadas gráficas
* Registos sem geometria
* Número de confinantes submetidos igual ao número de confinantes originais
* Geopackage submetido igual ao original

Validações geométricas:
* Dimensão 2D
* Geometria válida
* Tipo de geometria
* Vértices duplicados/redundantes
* Duplicados
* Sobreposições
* Lacunas
* Confinantes

## Utilização do separador Validação
* Aceder ao separador Validação.
* Caso pretenda executar todas as validações deve ativar a opção “Ativa todas as opções de Validação”.
* Caso pretenda apenas uma ou um conjunto de validações deve ativar apenas as opções pretendidas.
* Por defeito a tolerância definida paras as duas validações é de 0.001 metros. Poderá sempre alterar.
* Clicar em “Geopackage Original” para identificar o ficheiro geopackage com a representação dos dados originais.
* Clicar em “Geopackage a Submeter” para Identificar o ficheiro geopackage com a representação dos novos dados.
* Para executar clicar em “OK”.
* Como resultado é enviada uma mensagem para o monitor com o resumo dos resultados.

  
  
  <img width="886" height="920" alt="image" src="https://github.com/user-attachments/assets/1d05d0b2-acd7-431e-8e0d-656e64b84b90" />




* Os dados originais são adicionados ao grupo "originais" do projeto QGIS.
* Os dados submetidos são adicionados ao grupo "submetidos" do projeto QGIS.
* Quando são detetadas inconsistências do tipo “não geométricas” não são executadas as validações geométricas. Primeiro será necessário corrigir essas situações, e só depois submeter o ficheiro a   nova validação.
* As inconsistências detetadas são materializadas em ficheiros geopackage, temporários, e adicionados ao grupo "resultados" do projeto QGIS.

## Descrição de cada uma das validações
## Validações não geométricas

### Formato
Verificar se o formato do ficheiro submetido é válido. O ficheiro deve estar obrigatoriamente em formato GeoPackage (GPKG).

### Sistema de referência
Verificar se o sistema de referência de cada camada gráfica submetida é o sistema oficial definido pela DGT (atualmente o sistema PT-TM06/ETRS89). Apenas são aceites dados no sistema de referência PT-TM06/ETRS89.

### Número e nome de camadas gráficas
Verificar se o ficheiro submetido contém as camadas gráficas definidas. O ficheiro submetido deve conter as seis camadas gráficas: predio, confinantes, area_nao_cadastrada, dominio_publico, dominio_publico_confinante, adicionais). A camada gráfica adicionais não é validada, uma vez que não é considerada para efeitos de integração na Carta Cadastral. Esta camada tem como objetivo auxiliar na preparação do ficheiro GeoPackage a subemeter.

### Registos sem geometria
Verificar se no ficheiro submetido existem registos nas tabelas sem geometria associada. Não são aceites registos nas tabelas sem geometria associada.

### Número de confinantes submetidos igual ao número de confinantes originais
Verificar se no ficheiro submetido o número de confinantes é igual ao número de confinantes do ficheiro original. O número de confinantes da camada confinantes submetida tem de ser igual ao número de confinantes da camada correspondente original.

### Geopackage submetido igual ao original
Verificar se no ficheiro submetido é exatamente igual ao ficheiro original. O ficheiro submetido tem de ser diferente do ficheiro original.


## Validações geométricas

### Dimensão 2D
Verificar se o ficheiro submetido tem as geometrias representadas a 2D.
Não são aceites ficheiros com dimensão 3D.

### Geometria válida
Verificar se os polígonos das camadas gráficas submetidas são geometricamente válidos (por exemplo: não têm auto
intersecções, nem auto contatos). Não são aceites geometrias não válidas.

### Tipo de geometria
Verificar se as geometrias das camadas gráficas submetidas não apresentam mais do que um polígono com o mesmo registo na tabela de atributos (multipart polygons).
Não são aceites multipolígonos, apenas são aceites geometrias do tipo 'polygon'.

### Duplicados
Verificar se as geometrias das camadas gráficas submetidas não se encontram duplicadas. Não são aceites geometrias duplicadas.

### Sobreposições
Verificar se as geometrias das camadas gráficas submetidas não se sobrepõem. Não são aceites sobreposições.

### Lacunas
Verificar se as geometrias das camadas gráficas submetidas (predio, confinantes, area_nao_cadastrada e dominio_publico) preenchem a totalidade da área das geometrias da camada original "predio". (considerar uma tolerância, definida pelo critério da espessura). Não são aceites lacunas acima da tolerância.

### Vértices duplicados 
Verificar se as geometrias das camadas gráficas apresentam vértices em duplicado. São considerados vértices em duplicado, quando na mesma geometria existam vértices com as mesmas coordenadas (coordenadas são exatamente iguais, utilizando como referência 15 casas decimais). Não são aceites geometrias com vértices duplicados abaixo da tolerância.

### Vértices redundantes 
Verificar se as geometrias das camadas gráficas apresentam vértices muito próximos. São considerados vértices redundantes, quando na mesma geometria existam vértices a uma distância inferior a 1 mm. Não são aceites geometrias com vértices redundantes.

### Confinantes
Verificar se as geometrias dos confinantes submetidos sofreram alterações nas estremas que não são comuns ao prédio a conservar nem são comuns entre confinantes. (não é considerada qualquer tipo de tolerância)
Não são aceites ficheiros onde se verifique que as geometrias da camada gráfica “confinantes” tenham sofrido alterações em estremas que não são comuns ao prédio a conservar nem são comuns entre confinantes. 


