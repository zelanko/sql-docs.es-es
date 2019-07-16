---
title: Referencia (DMX) de extensiones de minería de datos | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 29454fefde7850e5e45ca6a916540e7d38e2b286
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070897"
---
# <a name="data-mining-extensions-dmx-reference"></a>Referencia de Extensiones de minería de datos (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Extensiones de minería de datos (DMX) es un lenguaje que puede usar para crear y trabajar con modelos de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede usar DMX para crear la estructura de modelos de minería de datos nuevos, para entrenar esos modelos y para explorar, administrar y realizar predicciones con ellos. DMX se compone de instrucciones de lenguaje de definición de datos (DDL), instrucciones de lenguaje de manipulación de datos (DML), y funciones y operadores.  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Especificación Microsoft OLE DB para minería de datos  
 Las características de minería de datos en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se compilan para cumplir con la [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para la especificación de minería de datos.  
  
 El [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para minería de datos de especificación define los siguientes elementos:  
  
-   Una estructura para contener la información que define un modelo de minería de datos.  
  
-   Un lenguaje para crear y trabajar con modelos de minería de datos.  
  
 La especificación define la base de la minería de datos como el objeto virtual de modelo de minería de datos. El objeto de modelo de minería de datos encapsula toda la información conocida acerca de un modelo de minería de datos específico. El objeto de modelo de minería de datos está estructurado como una tabla de SQL, con columnas, tipos de datos y metainformación que describen el modelo. Esta estructura le permite usar el lenguaje DMX (una extensión de SQL) para crear y trabajar con modelos.  
  
 **Para obtener más información:** [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
##  <a name="BKMK_DMXStatements"></a> Instrucciones DMX  
 Puede usar instrucciones DMX para crear, procesar, eliminar, copiar, examinar y realizar predicciones con modelos de minería de datos. Hay dos tipos de instrucciones en DMX: instrucciones de definición de datos e instrucciones de manipulación de datos. Cada tipo de instrucción lleva a cabo distintos tipos de tareas.  
  
 En las siguientes secciones se proporciona más información acerca de cómo trabajar con instrucciones DMX:  
  
-   [Instrucciones de definición de datos](#BKMK_DDL)  
  
-   [Instrucciones de manipulación de datos](#BKMK_DML)  
  
-   [Aspectos básicos de consulta](#BKMK_Queries)  
  
###  <a name="BKMK_DDL"></a> Instrucciones de definición de datos  
 Las instrucciones de definición de datos de DMX sirven para crear y definir nuevas estructuras y modelos de minería de datos, para importar y exportar modelos y estructuras de minería de datos y para quitar modelos existentes de una base de datos. Las instrucciones de definición de datos de DMX forman parte del lenguaje de definición de datos (DDL).  
  
 Puede realizar las siguientes tareas con las instrucciones de definición de datos de DMX:  
  
-   Crear una estructura de minería de datos mediante el [CREATE MINING STRUCTURE](../dmx/create-mining-structure-dmx.md) instrucción y agregar un modelo de minería de datos a la estructura de minería de datos mediante el [ALTER MINING STRUCTURE](../dmx/alter-mining-structure-dmx.md) instrucción.  
  
-   Crear un modelo de minería de datos y una estructura de minería de datos asociados al mismo tiempo mediante la [CREATE MINING MODEL](../dmx/create-mining-model-dmx.md) instrucción para crear un objeto de modelo de minería de datos vacía.  
  
-   Exportar un modelo de minería de datos y una estructura de minería de datos asociados a un archivo mediante el [exportar](../dmx/export-dmx.md) instrucción. Importar un modelo de minería de datos y una estructura de minería de datos asociados desde un archivo que se crea mediante la instrucción EXPORT mediante la [importación](../dmx/import-dmx.md) instrucción.  
  
-   Copiar la estructura de un modelo de minería de datos existente en un modelo nuevo y entrenarla con los mismos datos, mediante el uso de la [SELECT INTO](../dmx/select-into-dmx.md) instrucción.  
  
-   Quitar completamente un modelo de minería de datos de una base de datos mediante el uso de la [DROP MINING MODEL](../dmx/drop-mining-model-dmx.md) instrucción. Quitar completamente una estructura de minería de datos y todos sus modelos de minería de datos asociados de la base de datos mediante el [DROP MINING STRUCTURE](../dmx/drop-mining-structure-dmx.md) instrucción.  
  
 Para obtener más información acerca de las tareas de minería de datos que se pueden realizar mediante el uso de instrucciones DMX, vea [extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [Volver a instrucciones DMX](#BKMK_DMXStatements)  
  
###  <a name="BKMK_DML"></a> Instrucciones de manipulación de datos  
 Use instrucciones de manipulación de datos en DMX para trabajar con modelos de minería de datos existentes con el fin de examinar los modelos y crear predicciones con ellos. Las instrucciones de manipulación de datos de DMX forman parte del lenguaje de manipulación de datos (DML).  
  
 Puede realizar las siguientes tareas con las instrucciones de manipulación de datos de DMX:  
  
-   Entrenar un modelo de minería de datos usando el [INSERT INTO](../dmx/insert-into-dmx.md) instrucción. Esta instrucción no inserta los datos de origen reales en un objeto de modelo de minería de datos de origen, sino que, en su lugar, crea una abstracción que describe el modelo de minería que crea el algoritmo. La consulta de origen para una instrucción INSERT INTO se describe en [ \<consulta de origen de datos >](../dmx/source-data-query.md).  
  
-   Ampliar la instrucción SELECT para examinar la información que se calculan durante el entrenamiento del modelo y se almacena en el modelo de minería de datos, como las estadísticas de los datos de origen. Estas son las cláusulas que se pueden incluir para ampliar la funcionalidad de la instrucción SELECT:  
  
    -   [SELECT DISTINCT FROM &#60;modelo &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [SELECT FROM &#60;modelo&#62;. CONTENIDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
    -   [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [SELECT FROM &#60;modelo&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [SELECT FROM &#60;modelo&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   Crear predicciones que se basan en un modelo de minería de datos existente mediante el uso de la [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) cláusula de la instrucción SELECT. La consulta de origen para una instrucción de PREDICTION JOIN se describe en [ \<consulta de origen de datos >](../dmx/source-data-query.md).  
  
-   Quitar todos los datos entrenados de un modelo o una estructura mediante la [eliminar &#40;DMX&#41; ](../dmx/delete-dmx.md) instrucción.  
  
 Para obtener más información acerca de las tareas de minería de datos que se pueden realizar mediante el uso de instrucciones DMX, vea [extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [Volver a instrucciones DMX](#BKMK_DMXStatements)  
  
###  <a name="BKMK_Queries"></a> Aspectos básicos de consultas DMX  
 La instrucción SELECT es la base para la mayoría de las consultas DMX. En función de las cláusulas que use con esas instrucciones, puede examinar, copiar o realizar predicciones con modelos de minería de datos. La consulta de predicción usa una forma de SELECT para crear predicciones basadas en modelos de minería de datos existente. Las funciones amplían la capacidad de examinar y consultar los modelos de minería de datos más allá de las capacidades intrínsecas del modelo de minería de datos.  
  
 Puede usar funciones DMX para obtener información descubierta durante el entrenamiento de los modelos y para calcular información nueva. Estas funciones pueden utilizarse con muchos fines, por ejemplo, para devolver estadísticas que describan los datos subyacentes o la precisión de una predicción. O bien, para devolver una explicación ampliada de una predicción.  
  
 **Para obtener más información** **información:**  [Descripción de DMX instrucción Select](../dmx/understanding-the-dmx-select-statement.md), [funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), [estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md), [minería de datos Extensiones &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
 [Volver a instrucciones DMX](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
