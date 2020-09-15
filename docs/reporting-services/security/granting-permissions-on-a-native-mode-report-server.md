---
description: Concesión de permisos en un servidor de informes en modo nativo
title: Concesión de permisos en un servidor de informes en modo nativo | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- authorization [Reporting Services]
- server security [Reporting Services]
- role-based security [Reporting Services]
- items [Reporting Services], security
- permissions [Reporting Services], native mode
- published reports [Reporting Services], security
- reports [Reporting Services], security
- report items [Reporting Services], security
- role-based security [Reporting Services], about role-based security
- security [Reporting Services], role-based
ms.assetid: 260dc2e9-546c-4f04-9fa1-977e23c9d68c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 82fba1144cdb970d97b8aac4938fd7c3e8fe0980
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88373301"
---
# <a name="grant-permissions-on-a-native-mode-report-server"></a>Concesión de permisos en un servidor de informes en modo nativo
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa la autorización basada en roles y un subsistema de autenticación para determinar quién puede realizar operaciones y tener acceso a los elementos de un servidor de informes. La autorización basada en roles divide en roles el conjunto de acciones que puede realizar un usuario o un grupo. La autenticación se basa en la autenticación de Windows integrada o en un módulo de autenticación personalizado proporcionado por el usuario. Puede usar los roles predefinidos o los personalizados con cualquier tipo de autenticación.
  
## <a name="use-roles-to-grant-report-server-access"></a>Uso de roles para conceder acceso al servidor de informes
 Todos los usuarios interactúan con un servidor de informes dentro del contexto de un rol que define un nivel de acceso concreto. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye roles predefinidos que se pueden asignar a usuarios y a grupos para proporcionar acceso inmediato a un servidor de informes. **Administrador de contenido**, **Publicador** y **Explorador** son ejemplos de roles predefinidos. Cada rol define una recopilación de tareas relacionadas. Por ejemplo, un **publicador** tiene permiso para agregar informes y crear carpetas para almacenar esos informes.
  
 Las asignaciones de roles normalmente se heredan de un nodo primario, pero se puede anular la herencia de permisos creando una nueva asignación de roles para un elemento determinado. Es posible que un usuario que sea miembro del rol **Administrador de contenido** de un informe pertenezca al rol **Explorador** de otro.
  
 Para conceder el acceso a los elementos y las operaciones del servidor de informes:
  
1. Revise los roles predefinidos para determinar si puede utilizarlos tal y como están. Si tiene que ajustar las tareas o definir roles adicionales, realice estas acciones antes de asignar usuarios a roles específicos. Para obtener más información sobre cada rol, vea [Roles predefinidos](../../reporting-services/security/role-definitions-predefined-roles.md).
  
1. Identifique qué usuarios y grupos requieren acceso al servidor de informes y en qué nivel. Asigne a la mayoría de los usuarios el rol **Explorador** o **Generador de informes**. Asigne el rol **Publicador** a un número de usuarios más reducido. Asigne el rol **Administrador de contenido** solo a unos pocos usuarios.
  
1. Use el portal web para asignar roles en la carpeta Inicio de cada usuario o grupo que requiera acceso. La carpeta Inicio es la carpeta de nivel superior de la jerarquía de carpetas del servidor de informes.
  
1. En el nivel de sitio, en la página **Configuración del sitio** del portal web, cree una asignación de roles de nivel de sistema para cada usuario y grupo mediante los roles predefinidos **Usuario del sistema** y **Administrador del sistema**.
  
1. Cree las asignaciones de roles adicionales que necesite para carpetas, informes y otros elementos específicos. No cree un número elevado de asignaciones de roles. Si crea demasiadas, resulta difícil realizar el seguimiento de los distintos niveles de permisos para cada usuario.
  
> [!NOTE]  
>  Si ha configurado un servidor de informes para que se ejecute en el modo integrado de SharePoint, debe establecer permisos en el sitio de SharePoint para conceder acceso a los elementos del servidor de informes. Para obtener más información, vea [Concesión de permisos sobre elementos del servidor de informes en un sitio de SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md).
> 
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.
  
## <a name="who-sets-permissions"></a>Quién establece los permisos
 Inicialmente, solo los usuarios que son miembros del grupo local de administradores pueden tener acceso al servidor de informes. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está instalado con dos asignaciones de roles predeterminadas que conceden acceso de nivel de elemento y de nivel de sistema para los miembros del grupo local de administradores. Los administradores locales pueden usar estas asignaciones de roles integrados para conceder a los demás usuarios acceso al servidor de informes y administrar los elementos del servidor de informes. Las asignaciones de roles integrados no se pueden eliminar. Un administrador local siempre tiene permiso para administrar totalmente una instancia del servidor de informes.
 
 Antes de poder administrar una instancia del servidor de informes en un equipo local que ejecuta Windows Vista o Windows Server 2008, son necesarios algunos pasos de configuración adicionales. Para más información, vea [Configuración de un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).
  
## <a name="how-permissions-are-stored"></a>Cómo se almacenan los permisos
 Las asignaciones y las definiciones de roles se almacenan en la base de datos del servidor de informes. Si usa varias herramientas cliente o interfaces de programación, todo el acceso estará sujeto a los permisos que se definan para la instancia del servidor de informes en conjunto. Si configura varios servidores de informes en una implementación escalada, las asignaciones de roles que defina en una instancia se almacenan en una base de datos compartida y las usan todas las demás instancias de la misma implementación escalada. Dado que las asignaciones de roles se almacenan junto con los elementos a los que protegen, se puede mover la base de datos a otra instancia del servidor de informes sin perder los permisos definidos.
  
## <a name="tasks-and-tools-for-managing-permissions"></a>Tareas y herramientas para administrar permisos
 Use las herramientas siguientes para administrar definiciones y asignaciones de roles.
  
|Herramienta|Tareas|  
|----------|-----------|  
|Management Studio: se usa para ver, modificar, crear y eliminar definiciones de roles|[Creación, eliminación o modificación de un rol &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)|  
|El portal web: se usa para asignar usuarios y grupos a roles|[Concesión a un usuario de acceso a un servidor de informes](../../reporting-services/security/grant-user-access-to-a-report-server.md)<br /><br /> [Modificación o eliminación de una asignación de roles](../../reporting-services/security/role-assignments-modify-or-delete.md)|  
  
## <a name="see-also"></a>Consulte también
 - [Roles predefinidos](../../reporting-services/security/role-definitions-predefined-roles.md)  
 - [Concesión de permisos sobre elementos del servidor de informes en un sitio de SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 - [Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md)  
 - [Creación y administración de asignaciones de roles](../../reporting-services/security/create-and-manage-role-assignments.md)  
 - [Seguridad y protección de Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md)  
 - [Administración de contenido del servidor de informes &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
