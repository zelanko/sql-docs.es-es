---
title: SELECT INTO (DMX) | Documentos de Microsoft
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: acc30b259a9fa327c7f5d48fb0f77fdc3b8bf110
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842238"
---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea un nuevo modelo de minería de datos basado en la estructura de minería de datos de un modelo de minería de datos existente. El **SELECT INTO** instrucción crea el nuevo modelo de minería de datos copiando el esquema y otra información que no es específico del propio algoritmo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>Argumentos  
 *nuevo modelo*  
 Nombre único para el nuevo modelo que se está creando.  
  
 *Algoritmo*  
 Nombre definido por el proveedor de un algoritmo de minería de datos.  
  
 *Lista de parámetros*  
 Opcional. Lista delimitada por comas de parámetros definidos por el proveedor para el algoritmo.  
  
 *expression*  
 Una expresión que se evalúa como una condición de filtro válida en los datos de entrenamiento. Para obtener más información acerca de las expresiones que pueden utilizarse como filtros, consulte [filtros para los modelos de minería de datos &#40;Analysis Services: minería de datos&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 *modelo existente*  
 Nombre del modelo existente que se va a copiar.  
  
## <a name="remarks"></a>Notas  
 Si el modelo existente está entrenado, el nuevo modelo se procesa automáticamente cuando se ejecuta la instrucción. De lo contrario, el nuevo modelo permanece sin procesar.  
  
 El **SELECT INTO** instrucción solo funciona si la estructura del modelo existente es compatible con el algoritmo del nuevo modelo. Por lo tanto, esta instrucción es muy útil para crear y probar rápidamente modelos basados en el mismo algoritmo. Si cambia el tipo de algoritmo, el nuevo algoritmo debe admitir el tipo de datos de cada columna del modelo existente, o se podría producir un error al procesar el modelo.  
  
 El **WITH DRILLTHROUGH** cláusula permite la obtención de detalles en el nuevo modelo de minería de datos. La obtención de detalles solo se puede habilitar al crear el modelo.  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>Ejemplo 1: modificar los parámetros del modelo  
 En el ejemplo siguiente se crea un nuevo modelo de minería de datos basado en un modelo de minería de datos existente, `TM_Clustering`, que se crean en el [Tutorial básico de minería de datos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). En el nuevo modelo, el parámetro CLUSTER_COUNT se modifica de modo que exista un máximo de cinco clústeres en dicho modelo. En cambio, el modelo existente usa el valor predeterminado, que es 10.  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>Ejemplo 2: agregar un filtro al modelo  
 En el ejemplo siguiente se crea un nuevo modelo de minería de datos basado en un modelo existente, y se agrega un filtro al modelo. El filtro restringe los datos de entrenamiento únicamente a aquellos clientes que viven en una región determinada.  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  Los filtros que se aplican a la tabla de casos se pueden modificar usando la instrucción SELECT INTO tal y como se muestra en este ejemplo; sin embargo, si el modelo original contiene un filtro en una tabla anidada, dicho filtro no se puede modificar ni quitar usando esta sintaxis, y se copia sin modificar del modelo original. Para crear un modelo con un filtro diferente en una tabla anidada, use la sintaxis ALTER STRUCTURE...ADD MODEL.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; las instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
