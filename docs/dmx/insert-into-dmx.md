---
title: INSERTAR EN (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- INSERT INTO
- INSERT
- INSERT_INTO
dev_langs:
- DMX
helpviewer_keywords:
- SKIP (DMX)
- mapped model columns element
- source data query element
- <mapped model columns> element
- <source data query> element
- INSERT INTO statement
- mining models [Analysis Services], processing
- training mining models
- mining structures [DMX], processing
ms.assetid: 85eed207-396c-4a95-a74e-2acc1abc7e2c
caps.latest.revision: 49
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9ee2a89f60504719b74eb340f9399b8622d06500
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Procesa el objeto de minería de datos especificado. Para obtener más información acerca del procesamiento de modelos de minería de datos y estructuras de minería de datos, vea [consideraciones y requisitos de procesamiento &#40;minería de datos&#41;](../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Si se especifica una estructura de minería de datos, la instrucción procesa la estructura de minería de datos y todos sus modelos de minería de datos asociados. Si se especifica un modelo de minería de datos, la instrucción procesa solamente el modelo de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>Argumentos  
 *model*  
 Identificador de modelo.  
  
 *estructura*  
 Identificador de estructura.  
  
 *columnas del modelo asignadas*  
 Lista delimitada por comas de identificadores de columna e identificadores anidados.  
  
 *consulta de origen de datos*  
 Consulta de origen en el formato definido por el proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Si no se especifica **MINING MODEL** o **estructura de minería de datos**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] busca el tipo de objeto basado en el nombre y procesa el objeto correcto. Si el servidor contiene una estructura y un modelo de minería de datos con el mismo nombre, se devuelve un error.  
  
 Mediante el uso de la segunda forma de sintaxis, INSERT INTO*\<objeto >*. COLUMN_VALUES, puede insertar datos directamente en las columnas del modelo sin entrenar el modelo. Este método proporciona datos de columna al modelo de forma concisa y ordenada que resultan útiles a la hora de trabajar con conjuntos de datos que contienen jerarquías o columnas ordenadas.  
  
 Si usa **INSERT INTO** con un modelo de minería de datos o una estructura de minería de datos y deje desactivada la \<asignar columnas del modelo > y \<consulta de origen de datos > argumentos, la instrucción se comporta como **ProcessDefault**, con enlaces que ya existen. La instrucción devuelve un error cuando no existen enlaces. Para obtener más información acerca de **ProcessDefault**, consulte [opciones de procesamiento y la configuración &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md). En el siguiente ejemplo se muestra la sintaxis:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Si especifica **MINING MODEL** y proporcionar las columnas asignadas y una consulta de datos de origen, el modelo y estructura asociada se procesa.  
  
 La siguiente tabla ofrece una descripción del resultado de distintas formas de la instrucción, en función del estado de los objetos.  
  
|.|Estado de los objetos|Resultado|  
|---------------|----------------------|------------|  
|INSERT INTO MINING MODEL*\<modelo >*|La estructura de minería de datos está procesada.|Se procesa el modelo de minería de datos.|  
||La estructura de minería de datos no está procesada.|Se procesan el modelo y la estructura de minería de datos.|  
||La estructura de minería de datos contiene modelos de minería de datos adicionales.|Se produce un error en el proceso. Deberá volver a procesar la estructura y los modelos de minería de datos asociados.|  
|INSERT INTO MINING STRUCTURE*\<estructura >*|La estructura de minería de datos está procesada o sin procesar.|Se procesan la estructura de minería de datos y los modelos de minería de datos asociados.|  
|INSERT INTO MINING MODEL*\<modelo >* que contiene una consulta de origen<br /><br /> o bien<br /><br /> INSERT INTO MINING STRUCTURE*\<estructura >* que contiene una consulta de origen|La estructura o el modelo ya tienen contenido.|Se produce un error en el proceso. Debe borrar los objetos antes de realizar esta operación, mediante el uso de [eliminar &#40;DMX&#41;](../dmx/delete-dmx.md).|  
  
## <a name="mapped-model-columns"></a>Columnas de modelo asignadas  
 Mediante el uso de la \<asignar columnas del modelo > elemento, puede asignar las columnas del origen de datos a las columnas en el modelo de minería de datos. El \<asignar columnas del modelo > elemento tiene el formato siguiente:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Mediante el uso de **omitir**, puede excluir determinadas columnas que deben existir en la consulta de origen, pero que no existen en el modelo de minería de datos. SKIP es útil cuando no se tiene el control sobre las columnas que se incluyen en el conjunto de filas de entrada. Si está escribiendo su propia instrucción OPENQUERY, lo mejor es omitir la columna en la lista de columnas SELECT en lugar de usar SKIP.  
  
 SKIP también es útil cuando se necesita una columna del conjunto de filas de entrada para realizar una combinación, pero la estructura de minería de datos no utiliza la columna. Un ejemplo típico de esto es una estructura y un modelo de minería de datos que contienen una tabla anidada. El conjunto de filas de entrada para esta estructura tendrá una columna de clave externa que se utiliza para crear un conjunto de filas jerárquico mediante la cláusula SHAPE, pero la columna de clave externa casi nunca se utiliza en el modelo.  
  
 La sintaxis de SKIP requiere que se inserte SKIP en la posición de la columna individual en el conjunto de filas de entrada que no tiene ninguna columna de estructura de minería de datos correspondiente. Por ejemplo, en el ejemplo de tabla anidada siguiente, OrderNumber debe estar seleccionado en la cláusula APPEND para que se pueda utilizar en la cláusula RELATE con el fin de especificar la combinación; sin embargo, no desea insertar los datos de OrderNumber en la tabla anidada de la estructura de minería de datos. Por consiguiente, el ejemplo utiliza la palabra clave SKIP en lugar de OrderNumber en el argumento de INSERT INTO.  
  
## <a name="source-data-query"></a>Consulta de datos de origen  
 El \<consulta de origen de datos > elemento puede incluir los siguientes tipos de orígenes de datos:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **FORMA**  
  
-   Cualquier consulta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que devuelva un conjunto de filas  
  
 Para obtener más información acerca de los tipos de origen de datos, vea [ &#60;consulta de origen de datos&#62;](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Ejemplo básico  
 En el ejemplo siguiente se utiliza **OPENQUERY** para entrenar un modelo Bayes Naive en función de los datos de correo directo en el [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] base de datos.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>Ejemplo de tabla anidada  
 En el ejemplo siguiente se utiliza **forma** para entrenar un modelo de minería de datos de asociación que contiene una tabla anidada. Tenga en cuenta que la primera línea contiene **omitir** en su lugar OrderNumber, que es necesario el **SHAPE_APPEND** instrucción pero no usados en el modelo de minería de datos.  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; las instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos & #40; DMX & #41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
