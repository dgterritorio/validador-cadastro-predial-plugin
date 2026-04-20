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

<img width="717" height="695" alt="image" src="https://github.com/user-attachments/assets/d8c3b01c-0f16-4400-94ac-54147816cdf8" />

# Edição do ficheiro geopackage
Esta opção permite corrigir inconsistências nos polígonos.

Sobre o ficheiro geopackage submetido são realizadas um conjunto de correções automáticas com o objetivo de eliminar o maior número de inconsistências possível.
Correções automáticas:
•	Ajustar as geometrias entre si do ficheiro geopackage submetido
•	Ajustar as geometrias dos confinantes submetidos aos confinantes originais
•	Remover vértices duplicados
•	Corrigir geometrias inválidas
•	Converter as geometrias do tipo multipolígono para o tipo polígono
•	Converter as geometrias do geopackage de 3D para 2D

# Utilização do separador Edição
•	Aceder ao separador Edição
•	Ativar a opção “Corrigir os dados”
•	Clicar em “Geopackage Original” para identificar o ficheiro geopackage com a representação dos dados originais.
•	Clicar em “Geopackage a Corrigir” para Identificar o ficheiro geopackage com a representação dos novos dados.
•	Para terminar clicar em “OK” para executar.
•	Como resultado é adicionado ao projeto QGIS o novo geopackage.

# Descrição sobre cada uma das correções:

# Remover vértices duplicados
Elimina vértices (nós) duplicados de cada geometria, garantindo que não resultem geometrias não válidas. O procedimento implica a utilização de uma tolerância, neste caso 0, que determina quando os vértices são iguais.

# Corrigir geometrias inválidas
Garantir que todas as geometrias representadas no ficheiro geopackage submetido são válidas.
Tipos de erros mais comuns:
•	Auto intersecção (Quando o anel exterior ou interior cruza-se a si próprio. (Por exemplo: laços)
•	Anéis invertidos (anel interno com sentido contrário ao do anel exterior)
Em alguns casos, geometrias muito complexas podem exigir edição manual após a correção automática.

# Ajustar as geometrias de polígonos
O ajuste é realizado com base numa tolerância (0.001 metros) e segundo o modo de ajuste “Preferir alinhar nós, inserir vértices extra quando necessário”. Sempre que possível, fazer coincidir vértices entre os limites de polígonos vizinhos. Se os limites não se tocam exatamente adiciona novos vértices nos segmentos vizinhos de modo a assegurar a continuidade topológica entre polígonos (sem lacunas nem sobreposições)

# Ajustar as geometrias submetidas entre si
Garantir que não existem sobreposições nem lacunas, inferiores a 0.001 metros, entre todas as geometrias de polígonos no ficheiro geopackage submetido. É realizado um ajuste entre as geometrias da própria camada, e com todas as restantes camadas.

# Ajustar as geometrias dos confinantes submetidos aos confinantes originais
Garantir que não existem diferenças inferiores a 0.001 metros entre os polígonos dos confinantes submetidos e os confinantes originais. É realizado um ajuste entre as geometrias dos confinantes submetidos com as geometrias dos confinantes originais.

# Ficheiro GeoPackage corrigido
Como resultado dos procedimentos automáticos aplicados, o novo ficheiro geopackage contém exclusivamente geometrias bidimensionais (2D) do tipo polígono.


# Separador Validação
Esta opção permite identificar critérios que não estão a ser cumpridos, e que estão definidos na etapa 5 - Validação, da Plataforma de Conservação Cadastral Predial

<img width="716" height="691" alt="image" src="https://github.com/user-attachments/assets/c9dd2e3a-bffe-481b-956b-103eb587ce1a" />





