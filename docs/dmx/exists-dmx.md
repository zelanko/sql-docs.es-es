---
description: Exists (DMX)
title: Exists (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1f45a4a1d0e709c6b8eb9bb7217d268420f31d07
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726239"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Devuelve **true** si la subconsulta especificada devuelve al menos una fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *subquery*  
 Una instrucción SELECT con el formato SELECT * FROM \<column name> [where \<predicate list> ].  
  
## <a name="result-type"></a>Tipo de resultado  
 Devuelve **true** si el conjunto de resultados devuelto por la subconsulta contiene al menos una fila; de lo contrario, devuelve **false**.  
  
## <a name="remarks"></a>Observaciones  
 Puede utilizar la palabra clave NOT delante de EXISTS; por ejemplo, `WHERE NOT EXISTS (<subquery>)`.  
  
 La lista de columnas que se agrega al argumento de la subconsulta de EXISTS es irrelevante; la función solo comprueba la existencia de una fila que cumpla la condición.  
  
## <a name="examples"></a>Ejemplos  
 Puede utilizar EXISTS y NOT EXISTS para comprobar las condiciones en una tabla anidada. Esto es útil cuando se crea un filtro que controla los datos que se usan para entrenar o probar un modelo de minería de datos. Para obtener más información, vea [Filtros para modelos de minería &#40;Analysis Services - Minería de datos&#41;](/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining).  
  
 El ejemplo siguiente se basa en la `[Association]` estructura de minería de datos y el modelo de minería de datos que creó en el [tutorial básico de minería de datos](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130)). La consulta devuelve solo los casos en los que el cliente compró al menos un Patch kit.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 Otra manera de ver los mismos datos que devuelve esta consulta es abrir el modelo en el visor de asociaciones, hacer clic con el botón secundario en el conjunto de la **revisión kit = existente**, seleccionar la opción obtener **detalles** y, a continuación, seleccionar **solo casos del modelo**.  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Sintaxis y ejemplos del filtro de modelos &#40;Analysis Services: Minería de datos&#41;](/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
