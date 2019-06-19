---
title: CustomData (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 172915d99b231490cbdca24f70d1d38da27a1d3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248320"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  Devuelve el valor de la **CustomData** propiedad de cadena de conexión si define; de lo contrario, **null**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 El **CustomData** función puede recuperar el **CustomData** propiedad de cadena de conexión y pasar una valor de configuración que se utilizan las funciones de expresiones multidimensionales (MDX) e instrucciones, como [UserName (MDX)](../mdx/username-mdx.md) y [llamada (instrucción, MDX)](../mdx/mdx-data-manipulation-call.md). Por ejemplo, esta función puede utilizarse en una expresión de la seguridad dinámica para seleccionar los miembros del conjunto permitidos o denegados para el valor de cadena en el **CustomData** propiedad cadena de conexión.  
  
## <a name="example"></a>Ejemplo  
 La consulta siguiente muestra el valor devuelto por la **CustomData** función en una medida calculada:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
