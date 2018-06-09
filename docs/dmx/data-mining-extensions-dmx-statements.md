---
title: Referencia de instrucciones de extensiones (DMX) de minería de datos | Documentos de Microsoft
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1baab80455cc5267686bf26251629a1d47065344
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841498"
---
# <a name="data-mining-extensions-dmx-statements"></a>Instrucciones (DMX) de extensiones de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Trabajar con datos de modelos de minería de datos [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] implica las siguientes tareas principales:  
  
-   Crear estructuras y modelos de minería de datos  
  
-   Procesar estructuras y modelos de minería de datos  
  
-   Eliminar o quitar estructuras o modelos de minería de datos  
  
-   Copiar modelos de minería de datos  
  
-   Examinar modelos de minería de datos  
  
-   Realizar predicciones con modelos de minería de datos  
  
 Puede utilizar instrucciones DMX (Extensiones de minería de datos) para llevar a cabo cada una de estas tareas mediante programación.  
  
 Crear estructuras y modelos de minería de datos  
 Use la [CREATE MINING STRUCTURE &#40;DMX&#41; ](../dmx/create-mining-structure-dmx.md) instrucción para agregar una nueva estructura de minería de datos a una base de datos. A continuación, puede usar el [ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md) instrucción para agregar modelos de minería de datos a la estructura de minería de datos.  
  
 Use la [CREATE MINING MODEL &#40;DMX&#41; ](../dmx/create-mining-model-dmx.md) instrucción que se va a generar una nueva estructura de minería de datos asociado y del modelo de minería de datos.  
  
 Procesar estructuras y modelos de minería de datos  
 Use la [INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md) instrucción que se va a procesar una estructura de minería de datos y un modelo de minería de datos.  
  
 Eliminar o quitar estructuras o modelos de minería de datos  
 Use la [eliminar &#40;DMX&#41; ](../dmx/delete-dmx.md) instrucción para quitar todos los datos entrenados de un modelo de minería de datos o la estructura de minería de datos. Use la [DROP MINING STRUCTURE &#40;DMX&#41; ](../dmx/drop-mining-structure-dmx.md) o [DROP MINING MODEL &#40;DMX&#41; ](../dmx/drop-mining-model-dmx.md) instrucciones para quitar completamente una estructura de minería de datos o el modelo de minería de datos de una base de datos.  
  
 Copiar modelos de minería de datos  
 Use la [SELECT INTO &#40;DMX&#41; ](../dmx/select-into-dmx.md) instrucción para copiar la estructura de un modelo de minería de datos existente en un nuevo modelo de minería de datos y para entrenar el modelo nuevo con los mismos datos.  
  
 Examinar modelos de minería de datos  
 Use la [seleccione &#40;DMX&#41; ](../dmx/select-dmx.md) instrucción para examinar la información que el algoritmo de minería de datos se calcula y se almacena en el modelo de minería de datos durante el entrenamiento del modelo. Igual que con [!INCLUDE[tsql](../includes/tsql-md.md)], puede usar varias cláusulas con la instrucción SELECT, para ampliar su funcionalidad. Incluyen estas cláusulas [DISTINCT FROM \<modelo >](../dmx/select-distinct-from-model-dmx.md), [FROM \<modelo >. CASOS](../dmx/select-from-model-cases-dmx.md), [FROM \<modelo >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md), [FROM \<modelo >. CONTENIDO](../dmx/select-from-model-content-dmx.md) y [FROM \<modelo >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md).  
  
 Realizar predicciones con modelos de minería de datos  
 Use la [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) cláusula de la instrucción SELECT para crear predicciones que se basan en un modelo de minería de datos existente.  
  
 También puede importar y exportar modelos mediante el [importar &#40;DMX&#41; ](../dmx/import-dmx.md) y [exportar &#40;DMX&#41; ](../dmx/export-dmx.md) instrucciones.  
  
 Estas tareas se agrupan en dos categorías, instrucciones de definición de datos e instrucciones de manipulación de datos, que se describen en la siguiente tabla.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Extensiones de minería de datos &#40;DMX&#41; las instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)|Forman parte del lenguaje de definición de datos (DDL). Sirven para definir un nuevo modelo de minería de datos (incluido el entrenamiento) o para quitar un modelo de minería de datos existente de una base de datos.|  
|[Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)|Forman parte del lenguaje de manipulación de datos (DML). Sirven para trabajar con modelos de minería de datos existentes, incluida la exploración de un modelo y la creación de predicciones.|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; función referencia](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
