---
title: FREEZE (instrucción, MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FREEZE
dev_langs:
- kbMDX
helpviewer_keywords:
- FREEZE statement
- locking cell values [MDX]
ms.assetid: 59f1e860-6f37-41af-97d6-7708bdaac933
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 981baf5a25d77884444320e832e35d8b16623c46
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
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
  
## <a name="remarks"></a>Comentarios  
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
 [Instrucciones de Scripting de MDX &#40; MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
