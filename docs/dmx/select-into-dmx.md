---
title: SELECT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a34cdf743ff0bcecbb4b3088d99efdf3bbfef744
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938167"
---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea un nuevo modelo de minería de datos basado en la estructura de minería de datos de un modelo de minería de datos existente. El **SELECT INTO** instrucción crea el nuevo modelo de minería de datos copiando el esquema y otra información que no es específico para el algoritmo real.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>Argumentos  
 *nuevo modelo*  
 Nombre único para el nuevo modelo que se está creando.  
  
 *algorithm*  
 Nombre definido por el proveedor de un algoritmo de minería de datos.  
  
 *lista de parámetros*  
 Opcional. Lista delimitada por comas de parámetros definidos por el proveedor para el algoritmo.  
  
 *expression*  
 Una expresión que se evalúa como una condición de filtro válida en los datos de entrenamiento. Para obtener más información sobre las expresiones que se puede usar como filtros, consulte [filtros para modelos de minería de datos de &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 *modelo existente*  
 Nombre del modelo existente que se va a copiar.  
  
## <a name="remarks"></a>Comentarios  
 Si el modelo existente está entrenado, el nuevo modelo se procesa automáticamente cuando se ejecuta la instrucción. De lo contrario, el nuevo modelo permanece sin procesar.  
  
 El **SELECT INTO** instrucción solo funciona si la estructura del modelo existente es compatible con el algoritmo del nuevo modelo. Por lo tanto, esta instrucción es muy útil para crear y probar rápidamente modelos basados en el mismo algoritmo. Si cambia el tipo de algoritmo, el nuevo algoritmo debe admitir el tipo de datos de cada columna del modelo existente, o se podría producir un error al procesar el modelo.  
  
 El **WITH DRILLTHROUGH** cláusula permite la obtención de detalles en el nuevo modelo de minería de datos. La obtención de detalles solo se puede habilitar al crear el modelo.  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>Ejemplo 1: Modificar los parámetros del modelo  
 En el ejemplo siguiente se crea un nuevo modelo de minería de datos basado en un modelo de minería de datos existente, `TM_Clustering`, que se crean en el [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). En el nuevo modelo, el parámetro CLUSTER_COUNT se modifica de modo que exista un máximo de cinco clústeres en dicho modelo. En cambio, el modelo existente usa el valor predeterminado, que es 10.  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>Ejemplo 2: Agregar un filtro al modelo  
 En el ejemplo siguiente se crea un nuevo modelo de minería de datos basado en un modelo existente, y se agrega un filtro al modelo. El filtro restringe los datos de entrenamiento únicamente a aquellos clientes que viven en una región determinada.  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  Los filtros que se aplican a la tabla de casos se pueden modificar usando la instrucción SELECT INTO tal y como se muestra en este ejemplo; sin embargo, si el modelo original contiene un filtro en una tabla anidada, dicho filtro no se puede modificar ni quitar usando esta sintaxis, y se copia sin modificar del modelo original. Para crear un modelo con un filtro diferente en una tabla anidada, use la sintaxis ALTER STRUCTURE...ADD MODEL.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
