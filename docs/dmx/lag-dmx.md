---
title: Lag (DMX) | Documentos de Microsoft
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
- LAG
dev_langs:
- DMX
helpviewer_keywords:
- Lag function
ms.assetid: 2da6df1a-5506-4871-a0f0-83292f1df41e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a376393afd10b36904c7ffad00bf87bbb5cc60e4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="lag-dmx"></a>Lag (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el período de tiempo transcurrido entre la fecha del caso actual y la última fecha del conjunto de entrenamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 Un valor escalar del tipo integer.  
  
## <a name="remarks"></a>Comentarios  
 Si el **Lag** función se utiliza en un modelo donde la columna KEY TIME se encuentra dentro de una tabla anidada, la función debe encontrarse dentro de la expresión Sub-select de la instrucción.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los casos que tienen lugar dentro de los 12 últimos meses de los datos que se han utilizado para formar al modelo.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
