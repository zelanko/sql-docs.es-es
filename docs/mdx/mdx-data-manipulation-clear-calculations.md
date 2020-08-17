---
description: 'Manipulación de datos de MDX: CLEAR CALCULATIONS'
title: CLEAR CALCULAtions (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 06f3fc9d29630f3f69b994c2b4e7cf809b6b9efd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387009"
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
  
## <a name="remarks"></a>Observaciones  
 La cláusula **from** se puede omitir cuando se conoce el contexto del cubo, como en un script MDX.  
  
> [!NOTE]  
>  Esta instrucción solo puede ser ejecutada por un administrador de base de datos o de servidor o un miembro de un rol con acceso a los datos de origen del cubo (es decir, ReadSourceData=true)  
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones de manipulación de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
