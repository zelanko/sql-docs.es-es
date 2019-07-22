---
title: Validar una suscripción | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.validateandresynch.f1
helpviewer_keywords:
- Validate Subscription dialog box
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b5ebbac49365615b6a2173e2f898fabf8fc72a75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895252"
---
# <a name="validate-subscription"></a>Validar suscripción
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use el cuadro de diálogo **Validar suscripción** para especificar que es necesario validar una suscripción a una publicación de combinación la próxima vez que se ejecute el Agente de mezcla para la suscripción. El resultado de la validación se muestra en el Monitor de replicación. Para más información, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Validar datos replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
