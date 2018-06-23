---
title: Configurar reglas de negocios para enviar notificaciones (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], configuring notifications
- e-mail [Master Data Services], configuring business rules
- notifications [Master Data Services], configuring business rules
ms.assetid: b24f7b11-ab53-4642-999c-e17b543b3558
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2d0c5d66a15ba476806df39792206c47a31bb26d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105398"
---
# <a name="configure-business-rules-to-send-notifications-master-data-services"></a>Configurar reglas de negocios para enviar notificaciones (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], configure reglas de negocios para enviar notificaciones cuando desee notificar a los usuarios los cambios de los valores de los atributos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso a las áreas funcionales de **Permisos de usuario y de grupo** y de **Administración del sistema** . Si no tiene permiso para el área funcional de **Permisos de usuario y grupo** , no puede ver la lista de usuarios y grupos a los que enviar las notificaciones.  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Ya debe existir una regla de negocio que use una acción de validación. Para obtener más información, consulte [Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
-   El usuario o grupo que recibe la notificación debe tener al menos permiso de **Solo lectura** para el atributo que produce un error en la validación. Los usuarios o grupos a los que se haya denegado explícita o implícitamente el permiso para el atributo recibirán el correo electrónico pero no podrán obtener acceso al atributo en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
-   Si el correo se envía a un grupo, solo los miembros del mismo que hayan tenido acceso a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] recibirán el correo electrónico.  
  
### <a name="to-configure-business-rules-to-send-notifications"></a>Configurar reglas de negocios para enviar notificaciones  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la barra de menús, seleccione **Administrar** y haga clic en **Reglas de negocios**.  
  
3.  En la página **Mantenimiento de reglas de negocios** , en la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Entidad** , seleccione una entidad.  
  
5.  Desde el **tipo de miembro** , seleccione un tipo de miembro.  
  
6.  En la lista **Atributo** , seleccione un atributo o deje el valor predeterminado de **Todos**.  
  
7.  En la cuadrícula, en la fila de la regla de negocios, haga doble clic en el **notificación** campo.  
  
8.  En el submenú, haga clic en un usuario o un grupo al que desea enviar la notificación por correo electrónico.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   Aplique las reglas de negocios a los datos siguiendo uno de estos procedimientos:  
  
    -   [Validar miembros específicos con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   Configure el protocolo de correo electrónico de la manera siguiente:  
  
    -   [Configurar notificaciones por correo electrónico &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Las notificaciones &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)   
 [Configurar notificaciones por correo electrónico &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
  