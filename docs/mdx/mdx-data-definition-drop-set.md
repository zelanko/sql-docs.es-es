---
description: 'Definición de datos de MDX: DROP SET'
title: DROP SET (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5c4ca356847d75150aa098b331bdf0f8c8368bb6
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195610"
---
# <a name="mdx-data-definition---drop-set"></a>Definición de datos de MDX: DROP SET


  Quita un conjunto con nombre.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP [SESSION] SET   
   <Cube_Reference>.Set_Name   
               [,<Cube_Reference>.Set_Name ...n]  
  
<Cube_Reference> ::= {CURRENTCUBE | Cube_Name}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que proporciona el nombre del cubo.  
  
 *Set_Name*  
 Expresión de cadena válida que proporciona el nombre del conjunto con nombre que se va a quitar.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información sobre los conjuntos con nombre, vea [Crear conjuntos con nombre en MDX &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets).  
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones de definición de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
