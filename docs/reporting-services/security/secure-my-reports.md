---
title: Proteger mis informes | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- denying My Reports folder access
- private folders [Reporting Services]
- user workspace [Reporting Services]
- security [Reporting Services], My Reports folder
- My Reports folder [Reporting Services]
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 162f43fc4f81c228d90839c75d1959d71eff9322
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="secure-my-reports"></a>Proteger Mis informes
  La característica Mis informes proporciona un área de trabajo administrada por el usuario para trabajar con informes. A fin de cumplir su propósito, la carpeta Mis informes precisa permisos menos restrictivos que otras carpetas disponibles para uso general. Los usuarios que solo tienen permisos para ver y ejecutar informes en otras carpetas pueden necesitar un conjunto expandido de permisos para administrar sus carpetas Mis informes y el contenido que poseen. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona una asignación de roles especializada y una definición de roles para este fin.  
  
> [!NOTE]  
>  Mis informes solo está disponible en el Administrador de informes. No está disponible en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="role-assignment-for-my-reports"></a>Asignación de roles para Mis informes  
 La asignación de roles para Mis informes tiene elementos predefinidos y se crea automáticamente para cada usuario que active una carpeta Mis informes. El hecho de que el servidor de informes asigne seguridad automáticamente resulta especialmente útil para las organizaciones que usen Mis informes ampliamente, ya que los administradores no tienen que habilitar el acceso para cada usuario de Mis informes.  
  
 Una asignación de roles de **Mis informes** se compone de los siguientes elementos:  
  
-   El usuario de la carpeta Mis informes, que se encuentra en carpetas de usuarios\\*\<nombre de usuario >*\My carpeta de informes.  
  
-   La cuenta de usuario, que se determina cuando se activa la carpeta Mis informes. La carpeta se activa cuando un usuario hace clic en una carpeta Mis informes en el Administrador de informes o cuando publica un informe a una carpeta Mis informes desde el Diseñador de informes. Esta carpeta también se activa cuando un usuario solicita propiedades en el vínculo Mis informes.  
  
-   La definición de roles predefinida para Mis informes.  
  
## <a name="role-definition-for-my-reports"></a>Definición de roles para Mis informes  
 La definición del rol **Mis informes** incluye tareas que permiten administrar el contenido de una carpeta Mis informes. El rol **Mis informes** está destinado a ser un rol con un solo fin. Aunque puede elegirla para cualquier directiva de seguridad de nivel de elemento, debería evitar hacerlo para reducir al mínimo la posibilidad de que la modifique para adaptarse a otros requisitos de carpetas. Al reservar el rol **Mis informes** para la característica Mis informes, ayudará a lograr que todos los usuarios la puedan utilizar de igual manera.  
  
 De manera predeterminada, solo los administradores del servidor de informes pueden modificar el rol **Mis informes** . Puede personalizar el rol **Mis informes** cambiando las tareas que contiene. También puede sustituir un rol diferente.  
  
## <a name="denying-access-to-my-reports"></a>Denegar acceso a Mis informes  
 Puede impedir que los usuarios tengan acceso a Mis informes:  
  
-   Mediante la deshabilitación de Mis informes en la página Configuración del sitio. Para más información, vea [Habilitar y deshabilitar Mis informes](../../reporting-services/report-server/enable-and-disable-my-reports.md).  
  
-   Mediante la eliminación de todas las tareas del rol **Mis informes** .  
  
 Cuando deshabilite Mis informes, el vínculo a una carpeta Mis informes se quita del Administrador de informes. La estructura de carpetas subyacente que se utiliza para Mis informes (es decir, la carpeta Carpetas de usuarios y sus subcarpetas) todavía está disponible y accesible si el usuario conoce la ruta de la carpeta. La eliminación de tareas del rol **Mis informes** garantiza que se impida el acceso.  
  
## <a name="see-also"></a>Vea también  
 [Proteger los informes y recursos](../../reporting-services/security/secure-reports-and-resources.md)   
 [Carpetas protegidas](../../reporting-services/security/secure-folders.md)   
 [Conceder permisos en un servidor de informes de modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  

