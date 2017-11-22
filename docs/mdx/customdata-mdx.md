---
title: CustomData (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: EXISTS
dev_langs: kbMDX
helpviewer_keywords: Exists function
ms.assetid: 61d9f5a2-6f56-4179-a39b-317c8e0a2cdd
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5a9cb529cf70010c81f42adf42fdfe47e51054b3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="customdata-mdx"></a>CustomData (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor de la **CustomData** propiedad de cadena de conexión si está definida; en caso contrario, **null**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 El **CustomData** función puede recuperar la **CustomData** propiedad de cadena de conexión y pasar de una configuración que va a usar funciones de expresiones multidimensionales (MDX) e instrucciones, como [UserName (MDX)](../mdx/username-mdx.md) y [llamar (instrucción, MDX)](../mdx/mdx-data-manipulation-call.md). Por ejemplo, esta función puede utilizarse en una expresión de la seguridad dinámica para seleccionar los miembros del conjunto permitidos o denegados para el valor de cadena en el **CustomData** propiedad cadena de conexión.  
  
## <a name="example"></a>Ejemplo  
 La consulta siguiente muestra el valor devuelto por la **CustomData** función en una medida calculada:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
