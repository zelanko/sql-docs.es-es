---
title: --(Comentario) (DMX) resumen | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- commenting characters
- double hyphens
- -- (comment character)
ms.assetid: 487b580b-5b81-4e52-8868-4fa809e4ef58
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0ab3cef118685094ae96e02dcbf6b994e1157cd0
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="---comment-dmx-summary"></a>--(Comentario) (DMX) resumen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX (Extensiones de minería de datos), incluirlos al final de una línea de código o insertarlos en una línea independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Comentarios  
 Use este operador para comentarios de una línea o anidados. Los comentarios que se insertan con el guión doble (--) se delimitan con un carácter de nueva línea.  
  
 No hay límite de longitud para los comentarios.  
  
 Para obtener más información sobre cómo usar diferentes tipos de comentarios en DMX, vea [comentarios &#40; DMX &#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Vea también  
 [Estrella de barra diagonal &#40; Comentario &#41; &#40; DMX &#41;](../dmx/slash-star-comment-dmx.md)   
 [Doble barra diagonal &#40; Comentario &#41; &#40; DMX &#41;](../dmx/double-slash-comment-dmx.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

