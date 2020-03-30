---
title: Crear, eliminar o modificar un rol (Management Studio) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f079b7b16f485b92c60952d082281a1dba52d024
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "65570543"
---
# <a name="role-definitions---create-delete-or-modify"></a>Definiciones de roles: creación, eliminación o modificación

Reporting Services proporciona roles predefinidos que definen los niveles de acceso al servidor de informes. A cada usuario o grupo que necesita obtener acceso al servidor de informes se le asigna un rol que define las tareas permitidas. Los roles se definen para el servidor de informes como un conjunto. Debe ser coherente en cómo se define un rol y cómo se utiliza en todas las áreas del servidor de informes.

Para crear, modificar o eliminar roles, puede usar [!INCLUDE[SQL Server Management Studio](../../includes/ssmanstudiofull-md.md)]. Solo puede eliminar los roles que no se usan.

 Para asignar usuarios y grupos a los roles que crea, use portal web de SSRS. Para más información, vea [Conceder acceso de usuario a un servidor de informes](../../reporting-services/security/grant-user-access-to-a-report-server.md).

> [!NOTE]  
>Si el servidor de informes se configura para el modo integrado de SharePoint, y se conectó al sitio de SharePoint con el que se integra el servidor de informes, puede ver y modificar los niveles de permisos que controlan el acceso a las operaciones y el contenido del servidor de informes.

## <a name="to-create-a-role-definition"></a>Para crear una definición de roles

1. En el Explorador de objetos, expanda un nodo de servidor de informes.

2. Expanda la carpeta Seguridad.

3. Si va a crear una definición de roles de nivel de elemento, haga clic con el botón derecho en **Roles** > **Nuevo rol**.

    O bien, si va a crear una definición de roles del sistema, haga clic con el botón derecho en **Roles del sistema** > **Nuevo rol del sistema**.

4. Escriba un nombre único para el rol. El nombre debe incluir al menos un carácter. También puede incluir espacios y determinados símbolos, pero no los caracteres siguientes `[; : \ / @ & = + , $ / * < > | "]`.

5. Si lo desea, escriba una descripción. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], esta descripción solo resulta visible en esta página. Los usuarios que ven este elemento en el portal web pueden ver esta descripción en esa herramienta.

6. Seleccione las tareas que pueden realizar los miembros de este rol.

7. Seleccione **Aceptar**.

### <a name="to-delete-or-modify-a-role-definition"></a>Para eliminar o modificar una definición de roles  

1. En el Explorador de objetos, expanda un nodo de servidor de informes.

2. Expanda la carpeta Seguridad.

3. Para eliminar o modificar una definición de roles de nivel de elemento, expanda la carpeta Roles y, después, realice alguna de las siguientes acciones:

    1. Para eliminar una definición de roles, haga clic con el botón derecho en el elemento > **Eliminar**. Aparece el cuadro de diálogo **Eliminar elementos del catálogo**. Seleccione **Aceptar** para eliminar el rol.
  
    2. Para modificar una definición de roles, haga clic con el botón derecho en el elemento > **Propiedades**. De este modo se muestra la página General del cuadro de diálogo **Propiedades de rol de usuario** .

         Seleccione las tareas que pueden realizar los miembros de este rol y después seleccione **Aceptar**.
  
4. Para eliminar o modificar una definición de roles de nivel de sistema, expanda la carpeta **Roles del sistema** . Realice alguna de las siguientes acciones:

- Para eliminar una definición de roles del sistema, haga clic con el botón derecho en el elemento y seleccione **Eliminar**. Aparece el cuadro de diálogo **Eliminar elementos del catálogo**. Seleccione **Aceptar** para eliminar el rol.

- Para modificar una definición de roles del sistema, haga clic con el botón derecho en el elemento y seleccione **Propiedades**. De este modo se muestra la página General del cuadro de diálogo **Propiedades de rol del sistema** . Seleccione las tareas que pueden realizar los miembros de este rol y seleccione **Aceptar** para aplicar los cambios.

## <a name="see-also"></a>Consulte también

 [Conexión con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
 [Crear y administrar asignaciones de roles](../../reporting-services/security/create-and-manage-role-assignments.md)  
 [Reporting Services en SQL Server Management Studio &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
