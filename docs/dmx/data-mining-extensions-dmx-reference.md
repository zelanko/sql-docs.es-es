---
title: Referencia de extensiones de minería de datos (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c47514f551ec07a8c8837533cb38c0e6283645cd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892884"
---
# <a name="data-mining-extensions-dmx-reference"></a>Referencia de Extensiones de minería de datos (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Extensiones de minería de datos (DMX) es un lenguaje que puede usar para crear y trabajar con modelos de minería [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]de datos en. Puede usar DMX para crear la estructura de modelos de minería de datos nuevos, para entrenar esos modelos y para explorar, administrar y realizar predicciones con ellos. DMX se compone de instrucciones de lenguaje de definición de datos (DDL), instrucciones de lenguaje de manipulación de datos (DML), y funciones y operadores.  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Especificación Microsoft OLE DB para minería de datos  
 Las características de minería de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] datos de se crean para cumplir [!INCLUDE[msCoName](../includes/msconame-md.md)] con el OLE DB para la especificación de minería de datos.  
  
 El [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para la especificación de minería de datos define lo siguiente:  
  
-   Una estructura para contener la información que define un modelo de minería de datos.  
  
-   Un lenguaje para crear y trabajar con modelos de minería de datos.  
  
 La especificación define la base de la minería de datos como el objeto virtual de modelo de minería de datos. El objeto de modelo de minería de datos encapsula toda la información conocida acerca de un modelo de minería de datos específico. El objeto de modelo de minería de datos está estructurado como una tabla de SQL, con columnas, tipos de datos y metainformación que describen el modelo. Esta estructura le permite usar el lenguaje DMX (una extensión de SQL) para crear y trabajar con modelos.  
  
 **Para obtener más información:** [estructuras de minería de datos &#40;Analysis Services-Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining)  
  
##  <a name="dmx-statements"></a><a name="BKMK_DMXStatements"></a>Instrucciones DMX  
 Puede usar instrucciones DMX para crear, procesar, eliminar, copiar, examinar y realizar predicciones con modelos de minería de datos. Hay dos tipos de instrucciones en DMX: instrucciones de definición de datos e instrucciones de manipulación de datos. Cada tipo de instrucción lleva a cabo distintos tipos de tareas.  
  
 En las siguientes secciones se proporciona más información acerca de cómo trabajar con instrucciones DMX:  
  
-   [Instrucciones de definición de datos](#BKMK_DDL)  
  
-   [Instrucciones de manipulación de datos](#BKMK_DML)  
  
-   [Aspectos básicos de las consultas](#BKMK_Queries)  
  
###  <a name="data-definition-statements"></a><a name="BKMK_DDL"></a>Instrucciones de definición de datos  
 Las instrucciones de definición de datos de DMX sirven para crear y definir nuevas estructuras y modelos de minería de datos, para importar y exportar modelos y estructuras de minería de datos y para quitar modelos existentes de una base de datos. Las instrucciones de definición de datos de DMX forman parte del lenguaje de definición de datos (DDL).  
  
 Puede realizar las siguientes tareas con las instrucciones de definición de datos de DMX:  
  
-   Crear una estructura de minería de datos utilizando la instrucción [Create Mining Structure](../dmx/create-mining-structure-dmx.md) y agregar un modelo de minería de datos a la estructura de minería de datos mediante la instrucción [ALTER Mining Structure](../dmx/alter-mining-structure-dmx.md) .  
  
-   Crear un modelo de minería de datos y una estructura de minería de datos asociada simultáneamente mediante la instrucción [Create Mining Model](../dmx/create-mining-model-dmx.md) para generar un objeto de modelo de minería de datos vacío.  
  
-   Exportar un modelo de minería de datos y la estructura de minería de datos asociada a un archivo mediante la instrucción [Export](../dmx/export-dmx.md) . Importar un modelo de minería de datos y la estructura de minería de datos asociada desde un archivo creado mediante la instrucción de exportación mediante la instrucción [Import](../dmx/import-dmx.md) .  
  
-   Copiar la estructura de un modelo de minería de datos existente en un modelo nuevo y entrenarlo con los mismos datos mediante la instrucción [SELECT INTO](../dmx/select-into-dmx.md) .  
  
-   Quitar completamente un modelo de minería de datos de una base de datos mediante la instrucción [Drop Mining Model](../dmx/drop-mining-model-dmx.md) . Quitar completamente una estructura de minería de datos y todos sus modelos de minería de datos asociados de la base de datos mediante la instrucción [Drop Mining Structure](../dmx/drop-mining-structure-dmx.md) .  
  
 Para obtener más información acerca de las tareas de minería de datos que puede realizar mediante instrucciones DMX, consulte referencia de instrucciones de [extensiones de minería de datos &#40;dmx&#41;](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [Volver a Instrucciones DMX](#BKMK_DMXStatements)  
  
###  <a name="data-manipulation-statements"></a><a name="BKMK_DML"></a>Instrucciones de manipulación de datos  
 Use instrucciones de manipulación de datos en DMX para trabajar con modelos de minería de datos existentes con el fin de examinar los modelos y crear predicciones con ellos. Las instrucciones de manipulación de datos de DMX forman parte del lenguaje de manipulación de datos (DML).  
  
 Puede realizar las siguientes tareas con las instrucciones de manipulación de datos de DMX:  
  
-   Entrenar un modelo de minería de datos mediante la instrucción [Insert Into](../dmx/insert-into-dmx.md) . Esta instrucción no inserta los datos de origen reales en un objeto de modelo de minería de datos de origen, sino que, en su lugar, crea una abstracción que describe el modelo de minería que crea el algoritmo. La consulta de origen de una instrucción INSERT INTO se describe en [ \<>de consultas de datos de origen ](../dmx/source-data-query.md).  
  
-   Extienda la instrucción SELECT para examinar la información que se calcula durante el entrenamiento del modelo y se almacena en el modelo de minería de datos, como las estadísticas de los datos de origen. A continuación se indican las cláusulas que puede incluir para ampliar la eficacia de la instrucción SELECT:  
  
    -   [Seleccione DISTINCt FROM &#60;Model &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [Seleccione entre &#60;modelo&#62;. CONTENIDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
    -   [Seleccione entre &#60;modelo&#62;. CASOS &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [Seleccione entre &#60;modelo&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [Seleccione entre &#60;modelo&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   Cree predicciones basadas en un modelo de minería de datos existente mediante la cláusula de [combinación de predicción](../dmx/select-from-model-prediction-join-dmx.md) de la instrucción SELECT. La consulta de origen de una instrucción de combinación de predicción se describe en [ \<>de consultas de datos de origen ](../dmx/source-data-query.md).  
  
-   Quite todos los datos entrenados de un modelo o una estructura mediante la instrucción [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) .  
  
 Para obtener más información acerca de las tareas de minería de datos que puede realizar mediante instrucciones DMX, consulte referencia de instrucciones de [extensiones de minería de datos &#40;dmx&#41;](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [Volver a Instrucciones DMX](#BKMK_DMXStatements)  
  
###  <a name="dmx-query-fundamentals"></a><a name="BKMK_Queries"></a>Aspectos básicos de las consultas DMX  
 La instrucción SELECT es la base de la mayoría de las consultas DMX. En función de las cláusulas que use con esas instrucciones, puede examinar, copiar o realizar predicciones con modelos de minería de datos. La consulta de predicción usa una forma de SELECT para crear predicciones basadas en modelos de minería de datos existentes. Las funciones amplían la capacidad de examinar y consultar los modelos de minería de datos más allá de las capacidades intrínsecas del modelo de minería de datos.  
  
 Puede usar funciones DMX para obtener información descubierta durante el entrenamiento de los modelos y para calcular información nueva. Estas funciones pueden utilizarse con muchos fines, por ejemplo, para devolver estadísticas que describan los datos subyacentes o la precisión de una predicción. O bien, para devolver una explicación ampliada de una predicción.  
  
 **Para obtener más**  **información:** [Descripción de la instrucción SELECT de DMX](../dmx/understanding-the-dmx-select-statement.md), [funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), [estructura y uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md), [extensiones de minería de datos &#40;referencia de funciones DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
 [Volver a Instrucciones DMX](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
