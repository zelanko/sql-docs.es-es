---
title: Habilitar el modo de diseño de DirectQuery (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93b95dc39c0efb088003af9d5fb8b68cfce11ce9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310415"
---
# <a name="enable-directquery-design-mode-ssas-tabular"></a>Habilitar el modo de diseño de DirectQuery (SSAS tabular)
  Para crear un modelo en el modo DirectQuery, primero debe cambiar el entorno de tiempo de diseño para que admita al usuario del modo DirectQuery. Al hacerlo, el diseñador también hará lo siguiente:  
  
-   Habilitará el uso de las propiedades de implementación de DirectQuery.  
  
-   Cambiará la base de datos del área de trabajo para que se ejecute en un modo híbrido que utilice la caché para el diseño. Cuando implemente definitivamente el modelo, el modo se cambiará de nuevo al valor especificado en las propiedades de implementación del proyecto.  
  
-   Deshabilitará las características de diseño que sean incompatibles con el modo DirectQuery.  
  
-   Validará el modelo existente.  
  
 Este procedimiento describe cómo habilitar el modo DirectQuery en el diseñador.  
  
### <a name="to-enable-use-of-directquery-in-a-model"></a>Para habilitar el uso de DirectQuery en un modelo  
  
1.  Abra el archivo de la solución en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  En el Explorador de objetos, haga doble clic en el archivo Model.bim.  
  
3.  En el panel **Propiedades** , cambie la propiedad **DirectQueryMode**a **On**.  
  
4.  Si hay errores, abra la **Lista de errores** en Visual Studio y solucione los problemas que impiden que el modelo se cambie al modo DirectQuery.  
  
## <a name="see-also"></a>Vea también  
 [El modo DirectQuery &#40;Tabular de SSAS&#41;](directquery-mode-ssas-tabular.md)  
  
  
