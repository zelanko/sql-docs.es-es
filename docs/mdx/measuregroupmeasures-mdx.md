---
title: MeasureGroupMeasures (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55e00420ad3f941d50d9179dcd4a87d678cc28a0
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742044"
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
  
## <a name="remarks"></a>Notas  
 La cadena especificada debe coincidir exactamente con el nombre del grupo de medida. No es necesario utilizar corchetes para los nombres de los grupos de medida con espacios.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve todas las medidas del grupo de medida Internet Sales del cubo Adventure Works.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
