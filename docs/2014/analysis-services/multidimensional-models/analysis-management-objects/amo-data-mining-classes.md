---
title: Clases de minería de datos AMO | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: e4108825-b722-417c-9647-ab30ce35e549
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cd0f70d1ce76e3bcb4ed244e765cbeeb2fc44a5a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193775"
---
# <a name="amo-data-mining-classes"></a>Clases de minería de datos de AMO
  Las clases de minería de datos ayudan a crear, modificar, eliminar y procesar objetos de minería de datos. Trabajar con objetos de minería de datos incluye crear estructuras y modelos de minería de datos y procesar los modelos.  
  
 Para obtener más información acerca de cómo configurar el entorno y unos <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, y <xref:Microsoft.AnalysisServices.DataSourceView> objetos, vea [clases fundamentales de AMO](amo-fundamental-classes.md).  
  
 La definición de objetos en AMO requiere establecer varias propiedades en cada objeto para configurar el contexto correcto. Los objetos complejos, como los objetos OLAP y de minería de datos, requieren una codificación larga y detallada.  
  
  
 La ilustración siguiente muestra la relación de las clases que se explican en este tema.  
  
 ![Clases DataMining de AMO](../../../analysis-services/dev-guide/media/amo-dataminingclasses.gif "clases DataMining de AMO")  
  
##  <a name="MiningStructure"></a> Objetos MiningStructure  
 Una estructura de minería de datos es el contenedor de los modelos de minería de datos. La estructura define todas las columnas posibles que pueden utilizar los modelos de minería de datos. Cada modelo de minería de datos define sus propias columnas a partir del conjunto de columnas definidas en la estructura.  
  
 Un objeto <xref:Microsoft.AnalysisServices.MiningStructure> simple se compone de: información básica, una vista del origen de datos, uno o más elementos <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, cero o más elementos <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> y un elemento <xref:Microsoft.AnalysisServices.MiningModelCollection>.  
  
 Entre la información básica se incluye el nombre y el id. (identificador interno) del objeto <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
 El objeto <xref:Microsoft.AnalysisServices.DataSourceView> contiene el modelo de datos subyacente para la estructura de minería de datos.  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> son columnas o atributos que tienen valores únicos.  
  
 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> son columnas o atributos que tienen varios valores para cada caso.  
  
 <xref:Microsoft.AnalysisServices.MiningModelCollection> contiene todos los modelos de minería de datos generados sobre los mismos datos.  
  
 Para crear un objeto <xref:Microsoft.AnalysisServices.MiningStructure>, éste se agrega al elemento <xref:Microsoft.AnalysisServices.MiningStructureCollection> de la base de datos y se actualiza el objeto <xref:Microsoft.AnalysisServices.MiningStructure> en el servidor mediante el método Update.  
  
 Para quitar un objeto <xref:Microsoft.AnalysisServices.MiningStructure>, se tiene que hacer mediante el método Drop del objeto <xref:Microsoft.AnalysisServices.MiningStructure>. Quitar un objeto <xref:Microsoft.AnalysisServices.MiningStructure> de la colección no afecta al servidor.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure> se puede procesar mediante su propio método de proceso o bien cuando un objeto primario se procese con su propio método de proceso.  
  
### <a name="columns"></a>Columnas  
 Las columnas contienen los datos del modelo y puede ser de distintos tipos en función de su uso: Key, Input, Predictable o InputPredictable. Las columnas de predicción son el destino de la generación del modelo de minería de datos.  
  
 Las columnas de un solo valor se conocen como <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> en AMO. Las columnas de varios valores se conocen como <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
#### <a name="scalarminingstructurecolumn"></a>ScalarMiningStructureColumn  
 Un objeto <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> simple se compone de información básica, tipo, contenido y enlace de datos.  
  
 Entre la información básica se incluye el nombre y el id. (identificador interno) de <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
 El tipo es el tipo de datos del valor: LONG, BOOLEAN, TEXT, DOUBLE, DATE.  
  
 El contenido indica al motor cómo se puede modelar la columna. Los valores pueden ser: Discrete, Continuous, Discretized, Ordered, Cyclical, Probability, Variance, StdDev, ProbabilityVariance, ProbabilityStdDev, Support, Key.  
  
 El enlace de datos vincula la columna de minería de datos con el modelo de datos subyacente mediante un elemento de vista del origen de datos.  
  
 Para crear un objeto <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, éste se agrega al objeto <xref:Microsoft.AnalysisServices.MiningStructureCollection> primario y el objeto <xref:Microsoft.AnalysisServices.MiningStructure> primario se actualiza en el servidor mediante el método Update.  
  
 Para quitar un <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, se debe quitar de la colección del elemento primario <xref:Microsoft.AnalysisServices.MiningStructure>y el elemento primario <xref:Microsoft.AnalysisServices.MiningStructure> objeto debe actualizarse en el servidor mediante el método Update.  
  
#### <a name="tableminingstructurecolumn"></a>TableMiningStructureColumn  
 Un objeto <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> simple se compone de información básica y columnas escalares.  
  
 Entre la información básica se incluye el nombre y el id. (identificador interno) de <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
 Las columnas escalares son <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
 Para crear un objeto <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>, éste se agrega a la colección <xref:Microsoft.AnalysisServices.MiningStructure> primaria y se actualiza el objeto <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> primario en el servidor mediante el método Update.  
  
 Para quitar un objeto <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, éste debe quitarse de la colección del objeto <xref:Microsoft.AnalysisServices.MiningStructure> primario y el objeto <xref:Microsoft.AnalysisServices.MiningStructure> primario debe actualizarse en el servidor mediante el método Update.  
  
##  <a name="MiningModel"></a> Objetos MiningModel  
 <xref:Microsoft.AnalysisServices.MiningModel> es el objeto que permite elegir las columnas de la estructura y el algoritmo que se van a utilizar y, opcionalmente, los parámetros específicos para optimizar el modelo. Por ejemplo, puede que desee definir varios modelos de minería de datos en la misma estructura de minería de datos que utilicen los mismos algoritmos, pero omitir algunas columnas de dicha estructura en un modelo, usarlas como entradas en otro modelo y usarlas como entrada y predicción en un tercer modelo. Esto puede resultar útil si desea tratar una columna como continua en un modelo de minería de datos, pero en otro modelo desea tratarla como columna de datos discretos.  
  
 Un objeto <xref:Microsoft.AnalysisServices.MiningModel> simple se compone de: información básica, definición de algoritmos y columnas.  
  
 Entre la información básica se incluye el nombre y el id. (identificador interno) del modelo de minería de datos.  
  
 Una definición de algoritmo hace referencia a cualquiera de los algoritmos estándar proporcionados en [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o a cualquier algoritmo personalizado habilitado en el servidor.  
  
 Las columnas son una colección de las columnas utilizadas por el algoritmo y su definición de uso.  
  
 Un <xref:Microsoft.AnalysisServices.MiningModel> se crea al agregarlo a la <xref:Microsoft.AnalysisServices.MiningModelCollection> de la base de datos y actualizar la <xref:Microsoft.AnalysisServices.MiningModel> objeto en el servidor mediante el método Update.  
  
 Para quitar un objeto <xref:Microsoft.AnalysisServices.MiningModel>, se tiene que hacer mediante el método Drop de <xref:Microsoft.AnalysisServices.MiningModel>. Quitar un <xref:Microsoft.AnalysisServices.MiningModel> de la colección no afectan al servidor.  
  
 Una vez creado, <xref:Microsoft.AnalysisServices.MiningModel> se puede procesar mediante su propio método de proceso o bien cuando un objeto primario se procese con su propio método de proceso.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Clases fundamentales de AMO](amo-fundamental-classes.md)   
 [Programar objetos de minería de datos AMO](programming-amo-data-mining-objects.md)   
 [Introducción a las clases AMO](amo-classes-introduction.md)   
 [Arquitectura lógica &#40;Analysis Services - datos multidimensionales&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos &#40;Analysis Services - datos multidimensionales&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
