---
title: Roles y permisos (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- access controls [Reporting Services]
- permissions [Reporting Services], about permissions
- security [Reporting Services], identity and access control
- authentication [Reporting Services]
- permissions [Reporting Services]
- security [Reporting Services], role-based
- identity [Reporting Services]
ms.assetid: eea655fe-43ed-418d-8233-b288a8f4daa4
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: ce1209ca995b34e1c7ece83e7f5f1d9de7e78bfb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109206"
---
# <a name="roles-and-permissions-reporting-services"></a>Roles y permisos (Reporting Services)
  Reporting Services proporciona un subsistema de autenticación y un modelo de autorización basada en roles. Los modelos de autenticación y autorización varían en función de que el servidor de informes se ejecute en modo nativo o en modo de SharePoint. Si el servidor de informes forma parte de una implementación de SharePoint, los permisos de SharePoint determinarán quién tiene acceso a dicho servidor de informes.  
  
## <a name="identity-and-access-control-for-native-mode"></a>Identidad y control de acceso para el modo nativo  
 La autenticación predeterminada se basa en la autenticación de Windows y en la seguridad integrada. Puede cambiar los valores de autenticación para permitir al servidor de informes responder a solicitudes de autenticación diferentes, o también reemplazar las características de seguridad predeterminadas por una extensión de autenticación personalizada.  
  
 La autorización se basa en roles que el usuario asigna a un principio. Cada rol se compone de un conjunto de tareas relacionadas compuestas, a su vez, de operaciones relacionadas. Por ejemplo, la tarea **Administrar informes** concede acceso a las siguientes operaciones del servidor de informes: ver informes, agregar informe, actualizar informe, eliminar informe, programar informe y actualizar propiedades del informe.  
  
## <a name="identity-and-access-control-for-sharepoint-mode"></a>Identidad y control de acceso para el modo de SharePoint  
 En el modo integrado de SharePoint, la autenticación y la autorización se administran en el sitio de SharePoint, antes de que las solicitudes lleguen al servidor de informes. Dependiendo de cómo configure la autenticación, las solicitudes procedentes de un sitio de SharePoint incluyen un token de seguridad o un nombre de usuario de confianza. Los permisos que establezca para los usuarios y los grupos de SharePoint autorizarán el acceso a los elementos del servidor de informes situados en bibliotecas de SharePoint.  
  
## <a name="in-this-section"></a>En esta sección  
 [Concesión de permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md)  
 Describe el modelo de autorización basada en roles que proporciona acceso al contenido y a las operaciones.  
  
 [Concesión de permisos sobre elementos del servidor de informes en un sitio de SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 Explica cómo se usan los grupos de SharePoint, los niveles de permiso y los permisos para controlar el acceso a un servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Autenticación con el servidor de informes](authentication-with-the-report-server.md)   
 [Concesión de permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  