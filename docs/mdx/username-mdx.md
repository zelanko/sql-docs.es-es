---
title: Nombre de usuario (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 887af13c84fd06ead5a36564c0dda740a5f6d0b0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581357"
---
# <a name="username-mdx"></a>UserName (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el nombre de dominio y el nombre de usuario de la conexión actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>Notas  
 El valor devuelto es una cadena con el siguiente formato:  
  
 *nombre de dominio ombre de usuario*  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el nombre de usuario del usuario que ejecuta la consulta.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
