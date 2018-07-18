---
title: Doble barra diagonal (comentario) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca3b7040e5d51c324ddd50d489243b0f67f64feb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981837"
---
# <a name="double-slash-comment-dmx"></a>Doble barra diagonal (comentario) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica una cadena de texto que no debe ejecutar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede anidar comentarios dentro de una instrucción DMX (Extensiones de minería de datos), incluirlos al final de una línea de código o insertarlos en una línea independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>Parámetros  
 *Comment_Text*  
 Cadena que contiene el texto del comentario.  
  
## <a name="remarks"></a>Notas  
 Utilice // solamente para comentarios de una línea. Los comentarios que se insertan con // se delimitan con el carácter de nueva línea.  
  
 No hay límite de longitud para los comentarios.  
  
 Para obtener más información sobre cómo usar diferentes tipos de comentarios en DMX, vea [comentarios &#40;DMX&#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Vea también  
 [Barra diagonal y asterisco &#40;comentario&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [-- &#40;Comentario&#41; &#40;DMX&#41; resumen](../dmx/comment-dmx-summary.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
