---
title: Los miembros (cadena) (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Members
dev_langs: kbMDX
helpviewer_keywords: Members function
ms.assetid: 21fca354-448b-4b05-93f4-111bde1568f1
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bed8ef7372528320ff18be737c15218d80983690
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="members-string-mdx"></a>Members (String) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un miembro especificado por una expresión de cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Expresión de cadena válida que especifica un nombre de miembro.  
  
## <a name="remarks"></a>Comentarios  
 El **miembros (cadena)** función devuelve un único miembro cuyo nombre se especifica. Normalmente, se utiliza el **miembros (cadena)** función con funciones externas, lo que ofrece a los **miembros (cadena)** función una cadena que identifica un miembro, y el **miembros (cadena)** función devuelve el valor de este miembro especificado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el **miembros (cadena)** función para convertir la cadena especificada en un miembro válido y, a continuación, devuelve la medida predeterminada para el miembro especificado en la cadena. La cadena se especifica entre comillas simples. La medida predeterminada es la medida Reseller Sales Amount.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
