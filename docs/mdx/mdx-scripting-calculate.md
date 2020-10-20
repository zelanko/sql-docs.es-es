---
description: CALCULATE (instrucción MDX)
title: CALCULAte (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ff995f08ffef27abca65db10ff2cd38f2dd01e95
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196969"
---
# <a name="mdx-scripting---calculate"></a>Scripting de MDX: CALCULATE


  Llena cada celda de un cubo con un valor agregado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>Argumentos  
 Ninguno  
  
## <a name="remarks"></a>Observaciones  
 La instrucción CALCULATE se incluye automáticamente como la primera instrucción de un script MDX de un cubo al crearlo mediante [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. La instrucción CALCULATE indica que se agregue cada celda del cubo comenzando por las celdas de menor granularidad. Después de agregar una celda, si se llenan celdas de menor granularidad mediante expresiones, eso repercute en el valor agregado de las celdas de mayor granularidad. Casi siempre se prefiere realizar esta agregación, pero se puede eliminar o hacer que otras instrucciones se ejecuten antes que esta instrucción.  
  
 La instrucción CALCULATE no se puede incluir en un subcubo anidado del script MDX. Un subcubo anidado se define mediante la instrucción SCOPE. Para obtener más información acerca de la instrucción SCOPE, vea [Scope statement &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Los miembros calculados no se agregan.  
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones de scripting de MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [Aspectos básicos de scripting de MDX &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [Definir asignaciones y otros comandos de script](/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
