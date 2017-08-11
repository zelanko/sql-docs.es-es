---
title: Crear, eliminar o modificar un rol (Management Studio) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 42f66d05b179ee5f00c3322a2eb2943439936bcb
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="role-definitions---create-delete-or-modify"></a>Las definiciones de roles - crear, eliminar o modificar
  Reporting Services proporciona roles predefinidos que definen un nivel de acceso a un servidor de informes. Cada usuario o grupo que requiere acceso al servidor de informes lo hace a través de un rol que describe las tareas que se pueden realizar. Los roles se definen para el servidor de informes como un conjunto. No puede variar una definición de roles para partes concretas del servidor de informes ni especificar que se use un rol de manera diferente dependiendo de las circunstancias.  
  
 Para crear, modificar o eliminar roles, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Solo puede eliminar roles que no se usan.  
  
 Para asignar usuarios y grupos a los roles que crea, use el Administrador de informes. Para obtener más información, vea [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md).  
  
> [!NOTE]  
>  Si el servidor de informes se configura para el modo integrado de SharePoint, y se conectó al sitio de SharePoint con el que se integra el servidor de informes, puede ver y modificar los niveles de permisos que controlan el acceso a las operaciones y el contenido del servidor de informes.  
  
### <a name="to-create-a-role-definition"></a>Para crear una definición de roles  
  
1.  En el Explorador de objetos, expanda un nodo de servidor de informes.  
  
2.  Expanda la carpeta Seguridad.  
  
3.  Si está creando una definición de roles de nivel de elemento, haga clic con el botón derecho en **Roles**y seleccione **Nuevo rol**.  
  
     O bien, si está creando una definición de roles de nivel de sistema, haga clic con el botón derecho en **Roles del sistema**y seleccione **Nuevo rol del sistema**.  
  
4.  Escriba un nombre único para el rol. El nombre debe incluir al menos un carácter. También puede incluir espacios y determinados símbolos, pero no los caracteres ; ? : @ & = + , $ / * < > | " o /.  
  
5.  Si lo desea, escriba una descripción. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , esta descripción solo resulta visible en esta página. Los usuarios que ven este elemento a través del Administrador de informes pueden ver esta descripción en esa herramienta.  
  
6.  Seleccione las tareas que pueden realizar los miembros de este rol.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-or-modify-a-role-definition"></a>Para eliminar o modificar una definición de roles  
  
1.  En el Explorador de objetos, expanda un nodo de servidor de informes.  
  
2.  Expanda la carpeta Seguridad.  
  
3.  Para eliminar o modificar una definición de roles de nivel de elemento, expanda la carpeta Roles. Realice una de las siguientes acciones:  
  
    1.  Para eliminar una definición de roles, haga clic con el botón derecho en el elemento y haga clic en **Eliminar**. Aparece el cuadro de diálogo **Eliminar objeto** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  Para modificar una definición de roles, haga clic con el botón derecho en el elemento y haga clic en **Propiedades**. De este modo se muestra la página General del cuadro de diálogo **Propiedades de rol de usuario** .  
  
         Seleccione las tareas que pueden realizar los miembros de este rol y haga clic en **Aceptar**.  
  
4.  Para eliminar o modificar una definición de roles de nivel de sistema, expanda la carpeta **Roles del sistema** . Realice una de las siguientes acciones:  
  
    1.  Para eliminar una definición de roles de sistema, haga clic con el botón derecho en el elemento y haga clic en **Eliminar**. Aparece el cuadro de diálogo **Eliminar objeto** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  Para modificar una definición de rol de sistema, haga clic con el botón derecho en el elemento y haga clic en **Propiedades**. De este modo se muestra la página General del cuadro de diálogo **Propiedades de rol del sistema** .  
  
         Seleccione las tareas que pueden realizar los miembros de este rol y haga clic en **Aceptar** para aplicar los cambios.  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Crear y administrar las asignaciones de roles](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Reporting Services en SQL Server Management Studio &#40; SSRS &#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  

