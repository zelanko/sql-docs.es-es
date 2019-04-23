---
title: Proteger Mis informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- denying My Reports folder access
- private folders [Reporting Services]
- user workspace [Reporting Services]
- security [Reporting Services], My Reports folder
- My Reports folder [Reporting Services]
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: de90bbfad9bdd204e4eaf4c7c9afe96e6f8519f0
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59966809"
---
# <a name="secure-my-reports"></a>Proteger Mis informes
  La característica Mis informes proporciona un área de trabajo administrada por el usuario para trabajar con informes. A fin de cumplir su propósito, la carpeta Mis informes precisa permisos menos restrictivos que otras carpetas disponibles para uso general. Los usuarios que solo tienen permisos para ver y ejecutar informes en otras carpetas pueden necesitar un conjunto expandido de permisos para administrar sus carpetas Mis informes y el contenido que poseen. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona una asignación de roles especializada y una definición de roles para este fin.  
  
> [!NOTE]  
>  Mis informes solo está disponible en el Administrador de informes. No se encuentra disponible en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="role-assignment-for-my-reports"></a>Asignación de roles para Mis informes  
 La asignación de roles para Mis informes tiene elementos predefinidos y se crea automáticamente para cada usuario que active una carpeta Mis informes. El hecho de que el servidor de informes asigne seguridad automáticamente resulta especialmente útil para las organizaciones que usen Mis informes ampliamente, ya que los administradores no tienen que habilitar el acceso para cada usuario de Mis informes.  
  
 Una asignación de roles de **Mis informes** se compone de los siguientes elementos:  
  
-   La carpeta Mis informes del usuario, que está ubicada en la carpeta Carpetas de usuarios\\*\<nombre de usuario>* \Mis informes.  
  
-   La cuenta de usuario, que se determina cuando se activa la carpeta Mis informes. La carpeta se activa cuando un usuario hace clic en una carpeta Mis informes en el Administrador de informes o cuando publica un informe a una carpeta Mis informes desde el Diseñador de informes. Esta carpeta también se activa cuando un usuario solicita propiedades en el vínculo Mis informes.  
  
-   La definición de roles predefinida para Mis informes.  
  
## <a name="role-definition-for-my-reports"></a>Definición de roles para Mis informes  
 La definición del rol **Mis informes** incluye tareas que permiten administrar el contenido de una carpeta Mis informes. El rol **Mis informes** está destinado a ser un rol con un solo fin. Aunque puede elegirla para cualquier directiva de seguridad de nivel de elemento, debería evitar hacerlo para reducir al mínimo la posibilidad de que la modifique para adaptarse a otros requisitos de carpetas. Al reservar el rol **Mis informes** para la característica Mis informes, ayudará a lograr que todos los usuarios la puedan utilizar de igual manera.  
  
 De manera predeterminada, solo los administradores del servidor de informes pueden modificar el rol **Mis informes** . Puede personalizar el rol **Mis informes** cambiando las tareas que contiene. También puede sustituir un rol diferente.  
  
## <a name="denying-access-to-my-reports"></a>Denegar acceso a Mis informes  
 Puede impedir que los usuarios tengan acceso a Mis informes:  
  
-   Mediante la deshabilitación de Mis informes en la página Configuración del sitio. Para más información, vea [Habilitar y deshabilitar Mis informes](../report-server/enable-and-disable-my-reports.md).  
  
-   Mediante la eliminación de todas las tareas del rol **Mis informes** .  
  
 Cuando deshabilite Mis informes, el vínculo a una carpeta Mis informes se quita del Administrador de informes. La estructura de carpetas subyacente que se utiliza para Mis informes (es decir, la carpeta Carpetas de usuarios y sus subcarpetas) todavía está disponible y accesible si el usuario conoce la ruta de la carpeta. La eliminación de tareas del rol **Mis informes** garantiza que se impida el acceso.  
  
## <a name="see-also"></a>Vea también  
 [Proteger informes y recursos](secure-reports-and-resources.md)   
 [Proteger carpetas](secure-folders.md)   
 [Concesión de permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  
