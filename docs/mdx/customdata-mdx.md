---
description: CustomData (MDX)
title: CustomData (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ed7bfe2841caf9bd5b2c6e6caf102323db6d62ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413171"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  Devuelve el valor de la propiedad de cadena de conexión **CustomData** si está definido; de lo contrario, **es null**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 La función **CustomData** puede recuperar la propiedad de cadena de conexión **CustomData** y pasar un valor de configuración que se utilizará en las funciones e instrucciones MDX (expresiones multidimensionales), como [username (MDX)](../mdx/username-mdx.md) y [Call Statement (MDX](../mdx/mdx-data-manipulation-call.md)). Por ejemplo, esta función se puede usar en una expresión de seguridad dinámica para seleccionar los miembros de conjuntos permitidos o denegados para el valor de cadena en la propiedad de cadena de conexión **CustomData** .  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta muestra el valor devuelto por la función **CustomData** en una medida calculada:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
