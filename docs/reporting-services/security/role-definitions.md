---
title: Definiciones de roles | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- roles [Reporting Services], security
- security [Reporting Services], role definitions
- role-based security [Reporting Services], role definitions
ms.assetid: d1b8dbf0-4462-402e-92dd-0e4835002b6e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 22087b03c0c11d008d91de80930d98fef79fc3a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570586"
---
# <a name="role-definitions"></a>Definiciones de roles
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], una *definición de rol* es una colección con nombre de tareas que definen las operaciones disponibles en un servidor de informes. Las definiciones de roles proporcionan las reglas que el servidor de informes utiliza para aplicar la seguridad. Cuando un usuario intenta realizar una tarea, como publicar un informe, el servidor de informes comprueba la asignación de roles de dicho usuario para determinar si la tarea está incluida en su definición de roles. Si la tarea está incluida en la definición de roles, se envía la solicitud.  
  
## <a name="using-roles-to-authorize-access-to-a-report-server"></a>Usar roles para autorizar el acceso a un servidor de informes  
 Un rol será operativo solo cuando se utilice en una asignación de roles. Para obtener más información sobre el modo en que los roles proporcionan seguridad, vea [Asignaciones de roles](../../reporting-services/security/role-assignments.md).  
  
## <a name="types-of-role-definitions"></a>Tipos de definiciones de roles  
 Las definiciones de roles pueden ser de nivel de elemento o de nivel de sistema. Una *definición de roles de nivel de elemento* describe tareas relacionadas con elementos almacenados y administrados en un servidor de informes, como informes, carpetas y modelos. Administrar informes, Ver carpetas y Administrar suscripciones individuales son ejemplos de tareas que puede incluir en las definiciones de roles de nivel de elemento. Una *definición de roles del sistema* incluye tareas que se aplican a todo el sitio. Ver propiedades del servidor de informes es un ejemplo de tarea que puede incluir en un rol del sistema.  
  
## <a name="predefined-roles"></a>Roles predefinidos  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye roles predefinidos que corresponden a los distintos niveles de interacción del usuario. La lista siguiente contiene los roles predefinidos que puede utilizar:  
  
-   Administrador de contenido, Publicador, Explorador, Generador de informes y Mis informes son definiciones de roles de nivel de elemento que puede utilizar al crear asignaciones de roles para tener acceso al contenido del servidor de informes.  
  
-   Administrador del sistema y Usuario del sistema son definiciones de roles de nivel de sistema que puede utilizar para autorizar el acceso a las operaciones del sitio.  
  
 Para más información, consulte [Roles predefinidos](../../reporting-services/security/role-definitions-predefined-roles.md).  
  
## <a name="creating-a-role-definition"></a>Crear una definición de rol  
 Para crear un rol, use Management Studio para especificar un nombre y las tareas que contiene. Debe crear definiciones de roles independientes para las tareas de elemento y de sistema. Los roles pueden incluir tareas de nivel de elemento o tareas de nivel de sistema, pero no ambas. La creación de una definición de rol consiste en proporcionar un nombre y elegir un conjunto de tareas para la definición. Para crear una definición de rol, debe poseer el permiso correspondiente. La tarea "Establecer la seguridad de elementos individuales" proporciona estos permisos. De manera predeterminada, los administradores y usuarios asignados al rol predefinido **Administrador de contenido** pueden realizar esta tarea.  
  
 El rol debe tener un nombre único. Asimismo, para ser válido, debe contener al menos una tarea. Para más información, consulte [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md).  
  
 Para crear una definición de rol, use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para más información, consulte [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md).  
  
 Una vez creada la definición de roles, puede usarla seleccionándola en una asignación de roles. Para más información, consulte [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md).  
  
## <a name="customize-or-delete-a-role-definition"></a>Personalizar o eliminar una definición de roles  
 Los roles predefinidos se pueden modificar o reemplazar por roles personalizados. Para modificar un rol, agregue o quite tareas de la definición de roles. No puede cambiar el nombre de un rol. Los cambios que realice en una definición de roles se aplicarán de forma inmediata a todas las asignaciones de roles que la incluyan.  
  
 Puede eliminar una definición de roles si ya no la utiliza. No se puede eliminar la definición de rol seleccionada para la característica Mis informes mientras ésta siga habilitada. Para poder eliminar la definición de rol utilizada por Mis informes, primero debe deshabilitar la característica o seleccionar una definición de rol diferente para usarla con ella.  
  
## <a name="see-also"></a>Consulte también  
 [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md)   
 [Conceder permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)   
 [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)   
 [Modificar o eliminar una asignación de roles &#40;Administrador de informes&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)   
 [Establecer permisos para elementos del servidor de informes en un sitio de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
  
  
