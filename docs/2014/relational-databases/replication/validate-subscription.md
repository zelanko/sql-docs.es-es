---
title: Validar una suscripción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.validate.validateandresynch.f1
helpviewer_keywords:
- Validate Subscription dialog box
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5f7fae7d5ea40c7914d7f49653e4a8b5530c774f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111539"
---
# <a name="validate-subscription"></a>Validar suscripción
  Use el cuadro de diálogo **Validar suscripción** para especificar que es necesario validar una suscripción a una publicación de combinación la próxima vez que se ejecute el Agente de mezcla para la suscripción. El resultado de la validación se muestra en el Monitor de replicación. Para más información, consulte [Validate Data at the Subscriber](validate-data-at-the-subscriber.md).  
  
 Para validar todas las suscripciones a una publicación de combinación, también puede hacer clic en una publicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y hacer clic en **Validar todas las suscripciones**.  
  
## <a name="options"></a>Opciones  
 **Fecha del último intento de validación**  
 Muestra la fecha de la última sesión del Agente de mezcla en la que se validó la suscripción, independientemente de si la validación se realizó correctamente.  
  
 **Fecha de la última validación correcta**  
 Muestra la fecha de la sesión del Agente de mezcla en la que se realizó correctamente la validación de la suscripción.  
  
 **Validar esta suscripción**  
 Seleccione esta opción para validar la suscripción.  
  
 **Opciones**  
 Haga clic para tener acceso al cuadro de diálogo **Opciones de validación de subscripciones** , que permite especificar si desea usar la validación del recuento de filas o la validación de las sumas de comprobación binarias.  
  
## <a name="see-also"></a>Vea también  
 [Validar datos replicados](validate-replicated-data.md)  
  
  