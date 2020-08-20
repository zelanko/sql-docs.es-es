---
description: 'Definición de datos de MDX: DROP MEMBER'
title: DROP MEMBER (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f71232997c24a1bdca9a1294a804e8b30660d704
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483858"
---
# <a name="mdx-data-definition---drop-member"></a>Definición de datos de MDX: DROP MEMBER


  Quita un miembro calculado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que proporciona un nombre de cubo.  
  
 *Member_Identifier*  
 Expresión de cadena válida que proporciona un nombre de miembro o una clave de miembro.  
  
## <a name="see-also"></a>Consulte también  
 [Instrucción CREATE MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Instrucciones de definición de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
