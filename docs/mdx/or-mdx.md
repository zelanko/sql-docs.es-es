---
title: O (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45063e9f2aca6a924289d4d52434535d16c9a08e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055709"
---
# <a name="or-mdx"></a>OR (MDX)


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
  
## <a name="remarks"></a>Observaciones  
 El operador **or** trata ambos argumentos como valores booleanos (cero, 0, como **false**; de lo contrario, **true**) antes de que el operador realice la disyunción lógica. En la tabla siguiente se muestra cómo el operador **o** realiza la disyunción lógica.  
  
|*Argumento*|*Expression2*|Valor devuelto|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta contiene una medida calculada que devuelve la cadena "casado o hombre" si el miembro actual de la jerarquía Gender de la dimensión Customer es macho o el miembro actual de la jerarquía de estado civil de la dimensión Customer es casado; en caso contrario, devuelve la cadena "noncasado OR femenino".  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
