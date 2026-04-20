# validador-cadastro-predial-plugin
validador-cadastro-predial-plugin

# Plugin QGIS para validar os dados no ficheiro Geopackage a submeter na Plataforma de Conservação de Cadastro Predial

Para apoio aos Técnicos de Cadastro Predial (TCP) nas operações de conservação cadastral na preparação do ficheiro geopackage a submeter na Plataforma de Conservação de Cadastro Predial, é disponibilizado pela Direção-Geral do Território um plugin para o software livre QGIS.

Este plugin permite auxiliar o Técnico de Cadastro Predial na preparação do ficheiro geopackage, permitindo identificar as situações não conformes e também corrigir essas inconsistências de forma automática. 

# Instalar o plugin
Para instalar o plugin, escolha no menu a opção Plugins → Gerir e instalar plugins...
1.	Escolha a opção "Instalar de um ZIP"
2.	Escolha o arquivo validador_cns.zip em "Ficheiro ZIP:"
3.	Procedimento de instalação, pressionando o botão Instalar plugin

O plugin depois de instalado fica disponível no menu Plugins.

Colocar aqui figuras..

# Utilização do plugin
O plugin tem duas funcionalidades distintas e, por isso, tem desde logo dois separadores (Edição/Validação), dependendo se pretender, corrigir o ficheiro geopackage ou verificar a sua conformidade.

# Separador Edição
Esta opção permite corrigir inconsistências nos polígonos.

<img width="717" height="695" alt="image" src="https://github.com/user-attachments/assets/d8c3b01c-0f16-4400-94ac-54147816cdf8" />

# Edição do ficheiro geopackage

Sobre o ficheiro geopackage submetido são realizadas um conjunto de correções automáticas com o objetivo de eliminar o maior número de inconsistências possível.

Correções automáticas:
 * Ajustar as geometrias entre si do ficheiro geopackage submetido.
 * Ajustar as geometrias dos confinantes submetidos aos confinantes originais.
 * Remover vértices duplicados.
 * Corrigir geometrias inválidas.
 * Converter as geometrias do tipo multipolígono para o tipo polígono.
 * Converter as geometrias do geopackage de 3D para 2D.

# Utilização do separador Edição
* Aceder ao separador Edição.
* Ativar a opção “Corrigir os dados”.
* Clicar em “Geopackage Original” para identificar o ficheiro geopackage com a representação dos dados originais.
* Clicar em “Geopackage a Corrigir” para Identificar o ficheiro geopackage com a representação dos novos dados.
* Para executar clicar em “OK”.
* Como resultado é adicionado ao projeto QGIS o novo geopackage.

# Descrição sobre cada uma das correções:

# Remover vértices duplicados
Elimina vértices (nós) duplicados de cada geometria, garantindo que não resultem geometrias não válidas. O procedimento implica a utilização de uma tolerância, neste caso 0, que determina quando os vértices são iguais.

# Corrigir geometrias inválidas
Garantir que todas as geometrias representadas no ficheiro geopackage submetido são válidas.
Tipos de erros mais comuns:
* Auto intersecção (Quando o anel exterior ou interior cruza-se a si próprio). (Por exemplo: laços)
* Anéis invertidos (anel interno com sentido contrário ao do anel exterior).
Em alguns casos, geometrias muito complexas podem exigir edição manual após a correção automática.

# Ajustar as geometrias dos polígonos
O ajuste é realizado com base numa tolerância (0.001 metros) e segundo o modo de ajuste “Preferir alinhar nós, inserir vértices extra quando necessário”. Sempre que possível, fazer coincidir vértices entre os limites de polígonos vizinhos. Se os limites não se tocam exatamente adiciona novos vértices nos segmentos vizinhos de modo a assegurar a continuidade topológica entre polígonos (sem lacunas nem sobreposições).

# Ajustar as geometrias submetidas entre si
Garantir que não existem sobreposições nem lacunas, inferiores a 0.001 metros, entre todas as geometrias de polígonos no ficheiro geopackage submetido. É realizado um ajuste entre as geometrias da própria camada, e com todas as restantes camadas.

# Ajustar as geometrias dos confinantes submetidos aos confinantes originais
Garantir que não existem diferenças inferiores a 0.001 metros entre os polígonos dos confinantes submetidos e os confinantes originais. É realizado um ajuste entre as geometrias dos confinantes submetidos com as geometrias dos confinantes originais.

# Ficheiro GeoPackage corrigido
Como resultado dos procedimentos automáticos aplicados, o novo ficheiro geopackage contém exclusivamente geometrias bidimensionais (2D) do tipo polígono.


# Separador Validação
Esta opção permite identificar os critérios que não estão a ser cumpridos, e que estão definidos na etapa 5 - Validação, da Plataforma de Conservação Cadastral Predial

<img width="716" height="691" alt="image" src="https://github.com/user-attachments/assets/c9dd2e3a-bffe-481b-956b-103eb587ce1a" />

As Validações geometricas e não geométricas a efetuar sobre o ficheiro GeoPackage a submeter abrangem os seguintes parâmetros:

Validações não geométricas:
* Formato 
* Sistema de referência
* Número e nome das camadas gráficas

Validações geométricas:
* Dimensão 2D
* Geometria válida
* Tipo de geometria
* Registos sem geometria
* Vértices duplicados/redundantes
* Duplicados
* Sobreposições
* Lacunas
•	Confinantes

# Utilização do separador Validação
* Aceder ao separador Validação.
* Caso pretenda executar todas as validações deve ativar a opção “Ativa todas as opções de Validação”.
* Caso pretenda apenas uma ou um conjunto de validações deve ativar apenas as opções pretendidas.
* Por defeito a tolerância definida paras as duas validações é de 0.001 metros. Poderá sempre alterar.
* Clicar em “Geopackage Original” para identificar o ficheiro geopackage com a representação dos dados originais.
* Clicar em “Geopackage a Submeter” para Identificar o ficheiro geopackage com a representação dos novos dados.
* Para executar clicar em “OK”.
* Como resultado é enviada uma mensagem para o monitor com o resumo dos resultados.
  <img width="661" height="661" alt="image" src="https://github.com/user-attachments/assets/49e339e5-0c2d-4d0b-8e0a-cb033a59410f" />
* Os dados originais são adicionados ao grupo "originais" do projeto QGIS.
* Os dados submetidos são adicionados ao grupo "submetidos" do projeto QGIS.
* As inconsistências detetadas são materializadas em ficheiros geopackage, temporários, e adicionados ao grupo "resultados" do projeto QGIS.


# Descrição de cada uma das validações
# Validações não geométricas

* Formato
Verificar se o formato do ficheiro submetido é válido. O ficheiro deve estar obrigatoriamente em formato GeoPackage (GPKG).

* Sistema de referência
Verificar se o sistema de referência de cada camada gráfica submetida é o sistema oficial definido pela DGT (atualmente o sistema PT-TM06/ETRS89). Apenas são aceites dados no sistema de referência PT-TM06/ETRS89.

* Número e nome de camadas gráficas
Verificar se o ficheiro submetido contém as camadas gráficas definidas. O ficheiro submetido deve conter as seis camadas gráficas: predio, confinantes, area_nao_cadastrada, dominio_publico, dominio_publico_confinante, adicionais). A camada gráfica adicionais não é validada, uma vez que não é considerada para efeitos de integração na Carta Cadastral. Esta camada tem como objetivo auxiliar na preparação do ficheiro GeoPackage a subemeter.


# Validações geométricas

* Dimensão 2D
Verificar se o ficheiro submetido tem as geometrias representadas a 2D.
Não são aceites ficheiros com dimensão 3D.

* Geometria válida
Verificar se os polígonos das camadas gráficas submetidas são geometricamente válidos (por exemplo: não têm auto intersecções, nem auto contatos). Não são aceites geometrias não válidas.

* Tipo de geometria
Verificar se as geometrias das camadas gráficas submetidas não apresentam mais do que um polígono com o mesmo registo na tabela de atributos (multipart polygons).
Não são aceites multipolígonos, apenas são aceites geometrias do tipo polygon.

* Registos sem geometria
Verificar se no ficheiro submetido existem registos nas tabelas sem geometria associada. Não são aceites registos nas tabelas sem geometria associada.

* Duplicados
Verificar se as geometrias das camadas gráficas submetidas não se encontram duplicadas. Não são aceites geometrias duplicadas.

* Sobreposições
Verificar se as geometrias das camadas gráficas submetidas não se sobrepõem (deverá estar preparado para considerar uma tolerância). Não são aceites sobreposições.

* Lacunas
Verificar se as geometrias das camadas gráficas submetidas (predio, confinantes, area_nao_cadastrada e dominio_publico) ” devem preencher a totalidade da área das geometrias da camada original predio. (considerar uma tolerância, definida pelo critério da espessura). Não são aceites lacunas acima da tolerância.

* Vértices duplicados 
Verificar se as geometrias das camadas gráficas apresentam vértices em duplicado. São considerados vértices em duplicado, quando na mesma geometria existam vértices com as mesmas coordenadas (coordenadas são exatamente iguais, utilizando como referência 15 casas decimais). Não são aceites geometrias com vértices duplicados abaixo da tolerância.

* Vértices redundantes 
Verificar se as geometrias das camadas gráficas apresentam vértices muito próximos. São considerados vértices redundantes, quando na mesma geometria existam vértices a uma distância inferior a 1 mm. Não são aceites geometrias com vértices redundantes.

* Confinantes
Verificar se as geometrias dos confinantes submetidos sofreram alterações nas estremas que não são comuns ao prédio a conservar nem são comuns entre confinantes. (não é considerada qualquer tipo de tolerância)
Não são aceites ficheiros onde se verifique que as geometrias da camada gráfica “confinantes” tenham sofrido alterações em estremas que não são comuns ao prédio a conservar nem são comuns entre confinantes. 


