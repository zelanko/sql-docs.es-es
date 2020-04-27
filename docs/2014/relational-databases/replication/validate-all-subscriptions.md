---
title: Validar todas las suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.allsubscriptions.f1
helpviewer_keywords:
- Validate All Subscriptions dialog box
ms.assetid: 32e31469-36e4-42d9-a57a-12388bfd229d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b33cfe47cebba4c24c90ad41ce1b218192d128f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63255327"
---
# <a name="validate-all-subscriptions"></a>Validar todas las suscripciones
  Use el cuadro de diálogo **Validar todas las suscripciones** para especificar que todas las suscripciones a una publicación de combinación deben validarse la próxima vez que se ejecute el Agente de mezcla para cada suscripción. El resultado de la validación se muestra en el Monitor de replicación. Para más información, consulte [Validate Data at the Subscriber](validate-data-at-the-subscriber.md).  
  
 También puede validar una sola suscripción si hace clic con el botón secundario en una suscripción en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y hace clic en **Validar suscripción**.  
  
## <a name="options"></a>Opciones  
 **Solo comprobar recuentos de filas**  
 Seleccione esta opción para validar si la tabla del suscriptor tiene el mismo número de filas que la tabla del publicador. Este método no valida si el contenido de las filas coincide. La validación del recuento de filas proporciona una idea sobre validación que puede ponerle al corriente de problemas con los datos.  
  
 **Comprobar los recuentos de filas y comparar las sumas de comprobación para comprobar los datos de las filas**  
 Además de llevar a cabo un recuento de filas en el publicador y en el suscriptor, se calcula una suma de comprobación de todos los datos utilizando el algoritmo binario de suma de comprobación. Si el número de filas da un error, no se lleva a cabo la suma de comprobación. Esta opción no es válida para [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Validar datos replicados](validate-data-at-the-subscriber.md)  
  
  
