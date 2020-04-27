---
title: Validar una suscripción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.validateandresynch.f1
helpviewer_keywords:
- Validate Subscription dialog box
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3bd29769b0ba4fd5d9a48fcef07181b7ac70f7c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63255436"
---
# <a name="validate-subscription"></a>Validar suscripción
  Use el cuadro de diálogo **Validar suscripción** para especificar que es necesario validar una suscripción a una publicación de combinación la próxima vez que se ejecute el Agente de mezcla para la suscripción. El resultado de la validación se muestra en el Monitor de replicación. Para más información, consulte [Validate Data at the Subscriber](validate-data-at-the-subscriber.md).  
  
 Para validar todas las suscripciones a una publicación de combinación, también puede hacer clic con el botón derecho en una publicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y hacer clic en **Validar todas las suscripciones**.  
  
## <a name="options"></a>Opciones  
 **Fecha del último intento de validación**  
 Muestra la fecha de la última sesión del Agente de mezcla en la que se validó la suscripción, independientemente de si la validación se realizó correctamente.  
  
 **Fecha de la última validación correcta**  
 Muestra la fecha de la sesión del Agente de mezcla en la que se realizó correctamente la validación de la suscripción.  
  
 **Validar esta suscripción**  
 Seleccione esta opción para validar la suscripción.  
  
 **Opciones**  
 Haga clic para tener acceso al cuadro de diálogo **Opciones de validación de subscripciones** , que permite especificar si desea usar la validación del recuento de filas o la validación de las sumas de comprobación binarias.  
  
## <a name="see-also"></a>Consulte también  
 [Validar datos replicados](validate-data-at-the-subscriber.md)  
  
  
