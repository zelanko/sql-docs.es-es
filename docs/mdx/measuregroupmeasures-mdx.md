---
title: MeasureGroupMeasures (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: MeasureGroupMeasures function
ms.assetid: 69d9b205-1ca7-4741-9ca9-c7926bc87ead
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: baacb5ee83ecd45bc994cc462b04d35d6d3ca15a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un conjunto de medidas pertenecientes al grupo de medida especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>Argumentos  
 *MeasureGroupName*  
 Expresión de cadena válida que contiene el nombre del grupo de medida del que se recuperará el conjunto de medidas.  
  
## <a name="remarks"></a>Comentarios  
 La cadena especificada debe coincidir exactamente con el nombre del grupo de medida. No es necesario utilizar corchetes para los nombres de los grupos de medida con espacios.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve todas las medidas del grupo de medida Internet Sales del cubo Adventure Works.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
