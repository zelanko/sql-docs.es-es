---
title: Error (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ERROR
dev_langs: kbMDX
helpviewer_keywords: Error function
ms.assetid: 2caac19b-b297-443e-9299-648ef88a5039
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 51be756a90d641032453370c214cbd37683a055c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="error-mdx"></a>Error (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera un error y puede, opcionalmente, proporcionar un mensaje de error especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Error_Text*  
 Expresión de cadena válida que contiene el mensaje de error que se devolverá.  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra cómo utilizar el **Error** función dentro de una medida calculada:  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
