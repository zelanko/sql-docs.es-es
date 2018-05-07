---
title: Instrucción DROP ACTION (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP
- DROP ACTION
- Action
- DROP_ACTION
dev_langs:
- kbMDX
helpviewer_keywords:
- DROP ACTION statement
- deleting actions
- removing actions
- actions [MDX]
- dropping actions
ms.assetid: 74b3cfee-dea8-4968-a54c-1754d52ee1bd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: f91406c2af7698067ca31760d6a3984ee1246225
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-action"></a>Definición de datos MDX - acción DROP
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Elimina una acción específica de un cubo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Una expresión de cadena válida que proporciona el nombre del cubo.  
  
 *NombreDeAcción*  
 Expresión de cadena válida que proporciona el nombre de la acción que se va a quitar.  
  
## <a name="see-also"></a>Vea también  
 [Instrucción CREATE ACTION &#40;MDX&#41;](../mdx/mdx-data-definition-create-action.md)   
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
