---
title: CLEAR CALCULATIONS (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cdc4b2d3e948f0123eb15e38a6140e63009907bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187669"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>Manipulación de datos de MDX: CLEAR CALCULATIONS


  Quita todos los cálculos del cubo y devuelve el cubo al paso de cálculo 0.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Expression*  
 Una expresión de cubo de MDX (Expresiones multidimensionales) válida.  
  
## <a name="remarks"></a>Comentarios  
 El **FROM** cláusula puede omitirse cuando el contexto del cubo es conocido, como en un script MDX.  
  
> [!NOTE]  
>  Esta instrucción solo puede ser ejecutada por un administrador de base de datos o de servidor o un miembro de un rol con acceso a los datos de origen del cubo (es decir, ReadSourceData=true)  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de manipulación de datos MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
