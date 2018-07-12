---
title: Contenido de FORE_COLOR y BACK_COLOR (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a4909413bb7847d4254020ed2b4135049baaea4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278259"
---
# <a name="forecolor-and-backcolor-contents-mdx"></a>Contenido de FORE_COLOR y BACK_COLOR (MDX)
  Las propiedades de celda `FORE_COLOR` y `BACK_COLOR` se utilizan para almacenar información de color del texto y el fondo de una celda, respectivamente, en el formato rojo-verde-azul (RGB) del sistema operativo Microsoft Windows.  
  
 El intervalo válido de un color RGB normal es de cero (0) a 16,777,215 (&H00FFFFFF). El byte alto de un número de este intervalo es siempre igual a 0; los 3 bytes más bajos, del byte menos significativo al más significativo, determinan la cantidad de rojo, verde y azul, respectivamente. Los componentes rojo, verde y azul se representan mediante un número comprendido entre 0 y 255 (&HFF).  
  
## <a name="see-also"></a>Vea también  
 [Uso de las propiedades de celda &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)  
  
  
