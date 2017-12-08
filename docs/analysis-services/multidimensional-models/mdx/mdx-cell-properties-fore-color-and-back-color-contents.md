---
title: Contenido de FORE_COLOR y BACK_COLOR (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
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
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 15eccb9f4951a52bc1cfcf62e15e85eb245eb5f9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-cell-properties---forecolor-and-backcolor-contents"></a>Propiedades de celda MDX: contenido de FORE_COLOR y BACK_COLOR
  Las propiedades de celda **FORE_COLOR** y **BACK_COLOR** se usan para almacenar información de color del texto y el fondo de una celda, respectivamente, en el formato rojo-verde-azul (RGB) del sistema operativo Microsoft Windows.  
  
 El intervalo válido de un color RGB normal es de cero (0) a 16,777,215 (&H00FFFFFF). El byte alto de un número de este intervalo es siempre igual a 0; los 3 bytes más bajos, del byte menos significativo al más significativo, determinan la cantidad de rojo, verde y azul, respectivamente. Los componentes rojo, verde y azul se representan mediante un número comprendido entre 0 y 255 (&HFF).  
  
## <a name="see-also"></a>Vea también  
 [Usar las propiedades de celda &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)  
  
  
