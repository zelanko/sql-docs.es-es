---
title: Referencia de instrucciones de extensiones de minería de datos (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a7a9c18599d13c4db510793a1d75c85bbb7a829
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68070863"
---
# <a name="data-mining-extensions-dmx-statements"></a>Instrucciones de Extensiones de minería de datos (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Trabajar con modelos de minería de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] datos en implica las siguientes tareas principales:  
  
-   Crear estructuras y modelos de minería de datos  
  
-   Procesar estructuras y modelos de minería de datos  
  
-   Eliminar o quitar estructuras o modelos de minería de datos  
  
-   Copiar modelos de minería de datos  
  
-   Examinar modelos de minería de datos  
  
-   Realizar predicciones con modelos de minería de datos  
  
 Puede utilizar instrucciones DMX (Extensiones de minería de datos) para llevar a cabo cada una de estas tareas mediante programación.  
  
 Crear estructuras y modelos de minería de datos  
 Use la instrucción [Create Mining structure &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md) para agregar una nueva estructura de minería de datos a una base de datos. Después, puede usar la instrucción [ALTER Mining STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) para agregar modelos de minería de datos a la estructura de minería de datos.  
  
 Use la instrucción [Create Mining model &#40;DMX&#41;](../dmx/create-mining-model-dmx.md) para generar un nuevo modelo de minería de datos y una estructura de minería de datos asociada.  
  
 Procesar estructuras y modelos de minería de datos  
 Use la instrucción [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) para procesar una estructura de minería de datos y un modelo de minería de datos.  
  
 Eliminar o quitar estructuras o modelos de minería de datos  
 Use la instrucción [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) para quitar todos los datos entrenados de un modelo o estructura de minería de datos. Use la instrucción [Drop Mining STRUCTURE &#40;dmx&#41;](../dmx/drop-mining-structure-dmx.md) o [drop Mining model &#40;DMX&#41;](../dmx/drop-mining-model-dmx.md) para quitar completamente una estructura de minería de datos o un modelo de minería de datos de una base de datos.  
  
 Copiar modelos de minería de datos  
 Use la instrucción [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md) para copiar la estructura de un modelo de minería de datos existente en un nuevo modelo de minería de datos y para entrenar el nuevo modelo con los mismos datos.  
  
 Examinar modelos de minería de datos  
 Use la instrucción [SELECT &#40;DMX&#41;](../dmx/select-dmx.md) para examinar la información que el algoritmo de minería de datos calcula y almacena en el modelo de minería de datos durante el entrenamiento del modelo. Al igual que [!INCLUDE[tsql](../includes/tsql-md.md)]con, puede usar varias cláusulas con la instrucción SELECT para ampliar su capacidad. Estas cláusulas incluyen [distintas del \<modelo>](../dmx/select-distinct-from-model-dmx.md), [del \<modelo>. CASOS](../dmx/select-from-model-cases-dmx.md), [desde \<el> del modelo. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md), [del \<> del modelo. CONTENIDO](../dmx/select-from-model-content-dmx.md) y [del \<> del modelo. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md).  
  
 Realizar predicciones con modelos de minería de datos  
 Utilice la cláusula de [combinación de predicción](../dmx/select-from-model-prediction-join-dmx.md) de la instrucción SELECT para crear predicciones basadas en un modelo de minería de datos existente.  
  
 También puede importar y exportar modelos mediante las instrucciones [import &#40;dmx&#41;](../dmx/import-dmx.md) y [export &#40;DMX&#41;](../dmx/export-dmx.md) .  
  
 Estas tareas se agrupan en dos categorías, instrucciones de definición de datos e instrucciones de manipulación de datos, que se describen en la siguiente tabla.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Instrucciones de definición de datos de Extensiones de minería de datos &#40;DMX&#41;](../dmx/dmx-statements-data-definition.md)|Forman parte del lenguaje de definición de datos (DDL). Sirven para definir un nuevo modelo de minería de datos (incluido el entrenamiento) o para quitar un modelo de minería de datos existente de una base de datos.|  
|[Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)|Forman parte del lenguaje de manipulación de datos (DML). Sirven para trabajar con modelos de minería de datos existentes, incluida la exploración de un modelo y la creación de predicciones.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
