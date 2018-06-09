---
title: Instrucción DROP SET (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 26c5ebe206ed9d8530a7158b464e974920dd878e
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742024"
---
# <a name="mdx-data-definition---drop-set"></a>Definición de datos MDX: conjunto de destino


  Quita un conjunto con nombre.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP [SESSION] SET   
   <Cube_Reference>.Set_Name   
               [,<Cube_Reference>.Set_Name ...n]  
  
<Cube_Reference> ::= {CURRENTCUBE | Cube_Name}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Expresión de cadena válida que proporciona el nombre del cubo.  
  
 *Set_Name*  
 Expresión de cadena válida que proporciona el nombre del conjunto con nombre que se va a quitar.  
  
## <a name="remarks"></a>Notas  
 Para obtener más información sobre los conjuntos con nombre, vea [Crear conjuntos con nombre en MDX &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
