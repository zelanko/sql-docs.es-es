---
title: Contenido de FORE_COLOR y BACK_COLOR (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e7e22839611c1a9060b66850371d0ac2b551337c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108450"
---
# <a name="forecolor-and-backcolor-contents-mdx"></a>Contenido de FORE_COLOR y BACK_COLOR (MDX)
  Las propiedades de celda `FORE_COLOR` y `BACK_COLOR` se utilizan para almacenar información de color del texto y el fondo de una celda, respectivamente, en el formato rojo-verde-azul (RGB) del sistema operativo Microsoft Windows.  
  
 El intervalo válido de un color RGB normal es de cero (0) a 16,777,215 (&H00FFFFFF). El byte alto de un número de este intervalo es siempre igual a 0; los 3 bytes más bajos, del byte menos significativo al más significativo, determinan la cantidad de rojo, verde y azul, respectivamente. Los componentes rojo, verde y azul se representan mediante un número comprendido entre 0 y 255 (&HFF).  
  
## <a name="see-also"></a>Vea también  
 [Uso de propiedades de celda &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)  
  
  