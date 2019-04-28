---
title: Contenido de FORE_COLOR y BACK_COLOR (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb721d04e32e584a312c779db3aadab2ab83ba19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806142"
---
# <a name="mdx-cell-properties---forecolor-and-backcolor-contents"></a>Propiedades de celdas MDX: contenido FORE_COLOR y BACK_COLOR
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Las propiedades de celda **FORE_COLOR** y **BACK_COLOR** se usan para almacenar información de color del texto y el fondo de una celda, respectivamente, en el formato rojo-verde-azul (RGB) del sistema operativo Microsoft Windows.  
  
 El intervalo válido de un color RGB normal es de cero (0) a 16,777,215 (&H00FFFFFF). El byte alto de un número de este intervalo es siempre igual a 0; los 3 bytes más bajos, del byte menos significativo al más significativo, determinan la cantidad de rojo, verde y azul, respectivamente. Los componentes rojo, verde y azul se representan mediante un número comprendido entre 0 y 255 (&HFF).  
  
## <a name="see-also"></a>Vea también  
 [Usar las propiedades de celda &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)  
  
  
