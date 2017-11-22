---
title: O (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: OR
dev_langs: kbMDX
helpviewer_keywords: OR operator
ms.assetid: 7634c08a-5b70-44cd-9422-6555fed6ae05
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7cddabea47afb791fd4ec9f111d81248edc4c2f8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="or-mdx"></a>OR (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza una disyunción lógica de dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>Parámetros  
 Expression1  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
 Expression2  
 Expresión MDX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve **true** si uno o ambos argumentos se evalúan como **true**; en caso contrario, **false**.  
  
## <a name="remarks"></a>Comentarios  
 El **o** operador trata a ambos argumentos como valores booleanos (cero, 0, como **false**; en caso contrario, **true**) antes de que el operador realice la disyunción lógica. La tabla siguiente se muestra cómo el **o** operador realiza la disyunción lógica.  
  
|*Expression1*|*Expression2*|Valor devuelto|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta contiene una medida calculada que devuelve la cadena "MARRIED OR MALE" si el miembro actual en la jerarquía Gender de la dimensión Customer es Male o el miembro actual de la jerarquía Marital Status de la dimensión Customer es Married; de lo contrario devuelve la cadena "UNMARRIEDA OR FEMALE".  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
