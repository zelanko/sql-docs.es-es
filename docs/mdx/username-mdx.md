---
title: Nombre de usuario (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UserName
dev_langs:
- kbMDX
helpviewer_keywords:
- UserName function
ms.assetid: ecae549b-5c5e-4483-84e6-b713cd297d7e
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e9d9dbf069eab4da9c06e1a387baba47a90c24c5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="username-mdx"></a>UserName (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el nombre de dominio y el nombre de usuario de la conexión actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>Comentarios  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

