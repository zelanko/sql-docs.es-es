---
title: Barra diagonal estrella (comentario) (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- commenting characters
- forward slash-asterisk character pairs
- /*...*/ (comment)
ms.assetid: 163976cc-aa47-4eda-bd98-03c1a397f80e
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ad69726d5cdba7b421c33bdde86f46c187af4049
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="slash-star-comment-dmx"></a>Estrella de barra diagonal (comentario) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. El servidor no evalúa el texto entre los caracteres de comentario / * y \*/. Puede anidar comentarios dentro de una instrucción DMX (Extensiones de minería de datos), incluirlos al final de una línea de código o insertarlos en una línea independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Comentarios  
 Los comentarios con varias líneas deben indicarse con /* y \*/.  
  
 No hay límite de longitud para los comentarios.  
  
 Para obtener más información sobre cómo usar diferentes tipos de comentarios en DMX, vea [comentarios &#40;DMX&#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Vea también  
 [Doble barra diagonal &#40;comentario&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [-- &#40;Comentario&#41; &#40;DMX&#41; resumen](../dmx/comment-dmx-summary.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
