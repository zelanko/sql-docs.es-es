---
title: Barra diagonal (comentario) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5d0b929ba60915f116d9ff6843b4f20b3105a7ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67942843"
---
# <a name="slash-star-comment-dmx"></a>Barra diagonal (comentario) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. El servidor no evalúa el texto entre los caracteres de comentario/* y \*/. Puede anidar comentarios dentro de una instrucción DMX (Extensiones de minería de datos), incluirlos al final de una línea de código o insertarlos en una línea independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
/* Comment_Text */  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Observaciones  
 Los comentarios con varias líneas deben indicarse con /* y \*/.  
  
 No hay límite de longitud para los comentarios.  
  
 Para obtener más información sobre cómo usar diferentes tipos de comentarios en DMX, consulte [comentarios &#40;dmx&#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Consulte también  
 [Barra diagonal doble &#40;comentario&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)   
 [--&#40;comment&#41; &#40;Resumen de&#41; DMX](../dmx/comment-dmx-summary.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
