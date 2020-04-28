---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45d7adc5e1f4e103790d9d067bc4876fb5b134d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68033876"
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)


  Devuelve un conjunto de medidas pertenecientes al grupo de medida especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>Argumentos  
 *MeasureGroupName*  
 Expresión de cadena válida que contiene el nombre del grupo de medida del que se recuperará el conjunto de medidas.  
  
## <a name="remarks"></a>Observaciones  
 La cadena especificada debe coincidir exactamente con el nombre del grupo de medida. No es necesario utilizar corchetes para los nombres de los grupos de medida con espacios.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve todas las medidas del grupo de medida Internet Sales del cubo Adventure Works.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
