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
ms.openlocfilehash: 7f6e05ac728f6e1a9dda94dfcb07d26309b3e1f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061672"
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
  
## <a name="remarks"></a>Observaciones  
 Utilice // solamente para comentarios de una línea. Los comentarios que se insertan con // se delimitan con el carácter de nueva línea.  
  
 No hay límite de longitud para los comentarios.  
  
 Para obtener más información sobre cómo usar diferentes tipos de comentarios en DMX, consulte [comentarios &#40;dmx&#41;](../dmx/comments-dmx.md).  
  
## <a name="see-also"></a>Consulte también  
 [Barra diagonal de &#40;comentario&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)   
 [--&#40;comment&#41; &#40;Resumen de&#41; DMX](../dmx/comment-dmx-summary.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
