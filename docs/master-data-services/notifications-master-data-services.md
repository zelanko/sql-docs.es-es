---
title: Notificaciones (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
caps.latest.revision: 15
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 75df838645e9fa708d8baa27f3f35b07229044e7
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35331559"
---
# <a name="notifications-master-data-services"></a>Notificaciones (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] se puede configurar para enviar una notificación por correo electrónico cuando se produce un error en la validación de la regla de negocios, cuando cambia el estado de una versión del modelo o cuando cambia el estado de un conjunto de cambios.  
  
## <a name="how-notifications-are-sent"></a>Cómo se envían las notificaciones  
 Las notificaciones se configuran en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Las notificaciones envían mensajes de correo electrónico mediante Correo electrónico de base de datos en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] que hospeda la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información sobre el correo electrónico de base de datos, consulte [Objetos de configuración de Correo electrónico de base de datos](../relational-databases/database-mail/database-mail-configuration-objects.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="when-notifications-are-sent"></a>Cuándo se envían notificaciones  
 Una vez configuradas las notificaciones, se pueden enviar notificaciones por correo electrónico automatizadas en los casos siguientes.  
  
|Instancia|Descripción|  
|--------------|-----------------|  
|Haya un error de los datos en la validación de la regla de negocios|Se deben configurar reglas de negocios individuales para enviar correo electrónico cuando un valor de atributo produce un error en la validación de la regla de negocios. La notificación contiene la información siguiente.<br /><br /> Modelo<br /><br /> Versión<br /><br /> Entidad<br /><br /> Código del miembro<br /><br /> Regla de negocios con error<br /><br /> Vínculo al miembro para el que el valor del atributo produce un error en la regla de negocios<br /><br /> Hora de publicación de la notificación<br /><br /> Para obtener más información, consulte [Configurar reglas de negocios para enviar notificaciones &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md).|  
|El estado de la versión del modelo cambia|Cada vez que el estado de una versión del modelo cambia, los usuarios que son administradores de modelo reciben notificaciones automáticamente. La notificación contiene la información siguiente.<br /><br /> Modelo<br /><br /> Versión<br /><br /> Estado anterior y nuevo estado de la versión.<br /><br /> Hora de publicación de la notificación<br /><br /> Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).|  
|Cambios de estado del conjunto de cambios|Cada vez que cambia el estado de un conjunto de cambios para una entidad que requiere aprobación, los administradores de entidades y/o los propietarios del conjunto de cambios reciben notificaciones automáticamente. La notificación contiene la información siguiente.<br /><br /> Modelo<br /><br /> Versión<br /><br /> Nombre del conjunto de cambios.<br /><br /> Estado anterior<br /><br /> Nuevo estado<br /><br /> Vínculo para aplicar el conjunto de cambios para ver y modificar los cambios pendientes.<br /><br /> Para obtener más información, consulte [Conjuntos de cambios &#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md)|  
  
## <a name="system-settings"></a>Configuración del sistema  
 Hay opciones de [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que afectan a las notificaciones. Puede ajustarlas en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] o directamente en la tabla Configuración del sistema de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Configurar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para enviar notificaciones por correo electrónico.|[Configurar notificaciones por correo electrónico &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)|  
|Configurar [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para enviar notificaciones cuando cambien los valores de atributo.|[Configurar reglas de negocios para enviar notificaciones &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [Versiones &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
-   [Solucionar problemas de notificaciones de correo electrónico (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
