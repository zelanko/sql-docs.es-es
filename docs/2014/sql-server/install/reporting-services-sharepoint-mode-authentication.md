---
title: La autenticación de modo de SharePoint de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade SharePoint Mode [Reporting Services]
- SharePoint integration
- SharePoint Mode
ms.assetid: 2c19794a-dd55-4fe5-b901-6dd93e9f6beb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5c4c0e1536a32fa5aca0bc63ec80e255ad755491
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185309"
---
# <a name="reporting-services-sharepoint-mode-authentication"></a>Autenticación del modo de SharePoint de Reporting Services
  Use la página **Autenticación del modo de SharePoint de Reporting Services** del Asistente para la instalación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar las credenciales de la cuenta de servicio que se usa en la instalación actual de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las credenciales se usarán para crear un nuevo grupo de aplicaciones de SharePoint. Además, se creará una nueva aplicación de servicio de SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . El nombre de la aplicación de servicio contendrá el nombre de la instancia anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
  
-   La opción **Nombre de la cuenta del grupo de aplicaciones SSRS** es de solo lectura. El valor se rellena automáticamente con el valor actual de la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] existente que va a actualizar.  
  
-   La opción **Contraseña de la cuenta del grupo de aplicaciones SSRS** estará deshabilitada si la cuenta del grupo de aplicaciones no requiere una contraseña. Por ejemplo, “NT Authority\NetworkSerivce”. Si la cuenta del grupo de aplicaciones requiere una contraseña, no podrá continuar con la actualización hasta que escriba la contraseña correcta.  
  
 Para obtener más información, consulte [actualizar y migrar Reporting Services](http://go.microsoft.com/fwlink/?LinkID=245628) (http://go.microsoft.com/fwlink/?LinkID=245628).  
  
## <a name="see-also"></a>Vea también  
 [Actualizar y migrar Reporting Services](http://go.microsoft.com/fwlink/?LinkID=245628)  
  
  
