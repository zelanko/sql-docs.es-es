---
title: Habilitar el modo de diseño de DirectQuery (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 965a3a7c1bfa9549793690e92760ce39f147e0d2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067194"
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
 [Modo DirectQuery &#40;SSAS tabular&#41;](directquery-mode-ssas-tabular.md)  
  
  
