---
title: Notificaciones (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6891bba64da82a1a83f5ea4a44bf3fa1f52ddd67
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971166"
---
# <a name="notifications-master-data-services"></a>Notificaciones (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]se puede configurar para enviar una notificación por correo electrónico cuando se produce un error en la validación de la regla de negocios o cuando el estado de una versión del modelo cambia.  
  
## <a name="how-notifications-are-sent"></a>Cómo se envían las notificaciones  
 Las notificaciones se configuran en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Las notificaciones envían mensajes de correo electrónico mediante Correo electrónico de base de datos en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] que hospeda la [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] base de datos. Para obtener más información sobre el correo electrónico de base de datos, consulte [Objetos de configuración de Correo electrónico de base de datos](../relational-databases/database-mail/database-mail-configuration-objects.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="when-notifications-are-sent"></a>Cuándo se envían notificaciones  
 Una vez configuradas las notificaciones, se pueden enviar notificaciones por correo electrónico automatizadas en los casos siguientes.  
  
|Instancia|Descripción|  
|--------------|-----------------|  
|Haya un error de los datos en la validación de la regla de negocios|Se deben configurar reglas de negocios individuales para enviar correo electrónico cuando un valor de atributo produce un error en la validación de la regla de negocios. Para obtener más información, consulte [Configurar reglas de negocios para enviar notificaciones &#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md).|  
|El estado de la versión del modelo cambia|Cada vez que el estado de una versión del modelo cambia, los usuarios que son administradores de modelo reciben notificaciones automáticamente. Para obtener más información, vea [administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).|  
  
## <a name="system-settings"></a>Configuración del sistema  
 Hay opciones de [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que afectan a las notificaciones. Puede ajustarlas en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] o directamente en la tabla Configuración del sistema de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Configurar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para enviar notificaciones por correo electrónico.|[Configurar notificaciones por correo electrónico &#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)|  
|Configurar [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para enviar notificaciones cuando cambien los valores de atributo.|[Configurar reglas de negocios para enviar notificaciones &#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [Versiones &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
-   [Solucionar problemas de notificaciones de correo electrónico (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
