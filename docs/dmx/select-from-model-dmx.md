---
title: SELECT FROM &lt;modelo&gt; (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- empty prediction joins [DMX]
- SELECT FROM <model> statement
ms.assetid: dc5b9a01-e308-4ee8-84fc-ba4b991c60aa
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c51d5d3f3a5a1c8e9b94f72367739d592f1918c8
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgt-dmx"></a>SELECT FROM &lt;modelo&gt; (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza una combinación de predicción vacía que devuelve el valor o valores más probables para las columnas especificadas. Para crear la predicción, solo se emplea el contenido del modelo de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT <expression list> [TOP <n>] FROM <model>   
[WHERE <condition list>]   
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *lista de expresiones*  
 Lista delimitada por comas de expresiones o de columnas PREDICT o PREDICT ONLY.  
  
 *n*  
 Opcional. Entero que especifica el número de filas que se devuelven.  
  
 *model*  
 Identificador de modelo.  
  
 *lista de condiciones*  
 Opcional. Condiciones para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 Las columnas de la *lista de expresiones* debe ser definida como predict o predict only o relacionados con una columna de predicción.  
  
## <a name="naive-bayes-example"></a>Ejemplo de Bayes naive  
 En el siguiente ejemplo se realiza una combinación de predicción vacía en la columna Bike Buyer, que devuelve el estado más probable del modelo de minería de datos TM Naive Bayes.  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>Ejemplo de serie temporal  
 En el siguiente ejemplo se realiza una predicción en la columna Amount del modelo Forecasting, que devuelve los siguientes cuatro estadios temporales. La columna Model Region combina modelos de bicicleta y regiones en un único identificador. La consulta utiliza la [PredictTimeSeries &#40; DMX &#41;](../dmx/predicttimeseries-dmx.md) función para realizar la predicción.  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40; DMX &#41;](../dmx/select-dmx.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

