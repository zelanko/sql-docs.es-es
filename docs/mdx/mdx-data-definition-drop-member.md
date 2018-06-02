---
title: Instrucción DROP MEMBER (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5de7a54dd7b6b6ac35a44639c04cc1072117de7b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579587"
---
# <a name="mdx-data-definition---drop-member"></a>Definición de datos MDX - quitar miembro
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quita un miembro calculado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Expresión de cadena válida que proporciona un nombre de cubo.  
  
 *Member_Identifier*  
 Una expresión de cadena válida que proporciona un nombre de miembro o de clave de miembro.  
  
## <a name="see-also"></a>Vea también  
 [Instrucción CREATE MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
