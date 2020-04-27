---
title: Pausar el procesamiento de informes y suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1607637630c507588602dd7e566917ce1eeb6080
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100921"
---
# <a name="pause-report-and-subscription-processing"></a>Pausar el procesamiento de informes y suscripciones
  No es posible pausar un informe o una suscripción directamente. No obstante, se puede interrumpir su procesamiento antes del inicio del proceso o cuando se realiza una conexión al origen de datos. También es posible impedir el procesamiento de un informe o una suscripción haciendo que los usuarios no puedan obtener acceso a los mismos.  
  
 Puede utilizar las siguientes estrategias para impedir temporalmente que se lleve a cabo un proceso.  
  
## <a name="modify-role-assignments-to-prevent-access"></a>Modificar asignaciones de roles para impedir el acceso  
 La mejor manera de hacer que un informe no esté disponible es eliminar temporalmente la asignación de roles que ofrece acceso al informe en cuestión. Este enfoque es válido para todos los informes, independientemente de cómo se efectúe la conexión al origen de datos. Esta opción afecta solo al informe, no al funcionamiento de otros informes o elementos.  
  
 Para eliminar la asignación de roles, abra la página de propiedades Seguridad del informe desde el Administrador de informes. Si el informe hereda la seguridad de otro informe primario, haga clic en **Editar seguridad del elemento** para crear una directiva de seguridad restrictiva que pase por alto las asignaciones de roles que ofrecen un acceso total (por ejemplo, se puede quitar una asignación de roles que conceda acceso a Todos y mantener la asignación que ofrezca acceso a un grupo reducido de usuarios, como los Administradores).  
  
## <a name="disable-a-shared-data-source"></a>Deshabilitar un origen de datos compartido  
 Una de las ventajas de utilizar orígenes de datos compartidos consiste en la posibilidad de deshabilitarlos para evitar la ejecución de un informe o una suscripción controlada por datos. Al deshabilitar un origen de datos compartido, el informe se desconecta de su origen externo. Mientras está deshabilitado, el origen de datos deja de estar disponible para todos los informes y las suscripciones que lo utilizan. Para deshabilitar un origen de datos compartido, abra dicho origen desde el Administrador de informes y desactive la casilla **Habilitar este origen de datos** .  
  
 Tenga en cuenta que el informe se carga igualmente aunque el origen de datos no esté disponible. El informe no contiene datos, pero los usuarios que dispongan de los permisos adecuados pueden tener acceso a las páginas de propiedades, a la configuración de seguridad, al historial del informe y a la información de suscripción asociada al informe.  
  
## <a name="pause-a-shared-schedule"></a>Pausar una programación compartida  
 Cuando un informe o una suscripción se ejecutan desde una programación compartida, es posible pausar la programación para evitar el procesamiento. Cualquier proceso de informes o suscripciones controlado por una programación se pospone hasta que se vuelve a reanudar la programación. Para obtener más información, vea [pausar y reanudar programaciones compartidas](schedules.md).  
  
## <a name="see-also"></a>Consulte también  
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Página de propiedades de seguridad, elementos &#40;Administrador de informes&#41;](../security-properties-page-items-report-manager.md)  
  
  
