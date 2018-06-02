---
title: FREEZE (instrucción, MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b7eb3a3939ce8525dc57d27a24ac005ecb2cf2d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579907"
---
# <a name="mdx-scripting---freeze"></a>Scripting de MDX - INMOVILIZAR
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Bloquea los valores de celda de un subcubo especificado a sus valores actuales. Cuando se bloquean los valores de celda, los cambios en otras celdas no tienen efecto sobre las celdas bloqueadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>Argumentos  
 *Subcube_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un subcubo.  
  
## <a name="remarks"></a>Notas  
 El **INMOVILIZAR** instrucción bloquea los valores de las celdas de un subcubo especificado, impidiendo que instrucciones posteriores en un MDX pasa de script de cambio de sus valores de cálculo posteriores.  
  
 En el siguiente ejemplo, A y B representan subcubos en un script de cálculo MDX:  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 En este punto, tanto A como B equivalen a 3.  
  
 Insertamos ahora la **inmovilizar** función para bloquear las celdas en el subcubo:  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 Ahora, A es igual a 2 y B es igual a 3.  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de Scripting MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
