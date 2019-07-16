---
title: Error (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 91d07c6bbb4eb4731c9a802e47cd8f4c71aa5aeb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031230"
---
# <a name="error-mdx"></a>Error (MDX)


  Genera un error y puede, opcionalmente, proporcionar un mensaje de error especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Error_Text*  
 Expresión de cadena válida que contiene el mensaje de error que se devolverá.  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra cómo usar el **Error** función dentro de una medida calculada:  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
