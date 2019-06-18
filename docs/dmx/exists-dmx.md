---
title: Existe (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 99f6db275fcddaff3e739311ed588fb0ec776aaf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62506099"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve **true** si la subconsulta especificada devuelve al menos una fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *subquery*  
 Una instrucción SELECT, el formato SELECT * FROM \<nombre de columna > [donde \<lista de predicados >].  
  
## <a name="result-type"></a>Tipo de resultado  
 Devuelve **true** si el conjunto de resultados devuelto por la subconsulta contiene al menos una fila; en caso contrario, devuelve **false**.  
  
## <a name="remarks"></a>Comentarios  
 Puede utilizar la palabra clave NOT delante de EXISTS; por ejemplo, `WHERE NOT EXISTS (<subquery>)`.  
  
 La lista de columnas que se agrega al argumento de la subconsulta de EXISTS es irrelevante; la función solo comprueba la existencia de una fila que cumpla la condición.  
  
## <a name="examples"></a>Ejemplos  
 Puede utilizar EXISTS y NOT EXISTS para comprobar las condiciones en una tabla anidada. Esto es útil cuando se crea un filtro que controla los datos que se usan para entrenar o probar un modelo de minería de datos. Para obtener más información, vea [Filtros para modelos de minería &#40;Analysis Services - Minería de datos&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 En el siguiente ejemplo se basa en el `[Association]` estructura de minería de datos y el modelo de minería de datos que creó en el [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La consulta devuelve solo los casos en los que el cliente compró al menos un Patch kit.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 Otra forma de ver los mismos datos que devuelven esta consulta es abrir el modelo en el Visor de asociación, haga clic en el conjunto de elementos **Patch kit = Existing**, seleccione el **Drill Through** opción y, a continuación, Seleccione **solo casos del modelo**.  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Ejemplos y sintaxis de filtro del modelo &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)  
  
  
