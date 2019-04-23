---
title: Conceda al usuario el acceso a un servidor de informes (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- permissions [Reporting Services], granting report server access
- roles [Reporting Services], assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ebb42ac44d26e9ad8a091795eb3f8ab7283f6bcb
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59935861"
---
# <a name="grant-user-access-to-a-report-server-report-manager"></a>Conceder a un usuario acceso a un servidor de informes (Administrador de informes)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa la seguridad basada en roles para conceder a un usuario acceso a un servidor de informes. En una nueva instalación del servidor de informes, solo los usuarios que son miembros del grupo local de administradores tienen los permisos para acceder a las operaciones y al contenido del servidor de informes. Para hacer que el servidor de informes esté disponible para otros usuarios, debe crear asignaciones de roles que asignen cuentas de usuario o de grupo a un rol predefinido que especifique una recopilación de tareas.  
  
 **Servidores de informes de modo de SharePoint:** Para un servidor de informes está configurado para modo integrado de SharePoint, configurar acceso desde un sitio de SharePoint mediante los permisos de SharePoint. Los niveles de permisos del sitio de SharePoint determinan el acceso a las operaciones y el contenido del servidor de informes. Debe ser un administrador de sitio para conceder permisos en un sitio de SharePoint. Para obtener más información, vea [Conceder permisos sobre elementos del servidor de informes en un sitio de SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md).  
  
 **Servidores de informes de modo nativo:** En este tema se centra en un servidor de informes está configurado para modo nativo y el uso del Administrador de informes para asignar a usuarios a un rol. Hay dos tipos de roles:  
  
-   Los roles de nivel de elemento se usan para ver, agregar y administrar el contenido del servidor de informes, las suscripciones, el procesamiento de informes y el historial de informes. Las asignaciones de roles de nivel de elemento se definen en el nodo raíz (la carpeta Inicio) o en carpetas o elementos específicos en un nivel inferior de la jerarquía.  
  
-   Los roles de nivel de sistema permiten el acceso a las operaciones de todo el sitio que no se enlazan a ningún elemento específico. Los ejemplos incluyen el uso del Generador de informes y el uso de las programaciones compartidas.  
  
     Los dos tipos de roles se complementan entre sí y deben usarse juntos. Por esta razón, agregar un usuario a un servidor de informes es una operación con dos partes implicadas. Si asigna un usuario a un rol de nivel de elemento, también deberá asignarlo a un rol de nivel de sistema. Al asignar un usuario a un rol, debe seleccionar un rol que ya esté definido. Para crear, modificar o eliminar roles, use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para más información, consulte [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md).  
  
## <a name="before-you-start"></a>Antes de empezar  
 Revise la lista siguiente antes de agregar usuarios a un servidor de informes en modo nativo.  
  
-   Debe ser miembro del grupo local de administradores en el equipo del servidor de informes. Si implementa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] o Windows Server 2008, se requiere la configuración adicional antes de poder administrar localmente un servidor de informes. Para obtener más información, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
-   Para delegar esta tarea en otros usuarios, cree asignaciones de roles que asignen cuentas de usuario a los roles de administrador de contenido y de sistema. Los usuarios con permisos de administrador de contenido y de sistema pueden agregar usuarios a un servidor de informes.  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], vea los roles predefinidos para Roles del sistema y Roles del usuario para familiarizarse con los tipos de tareas de cada rol. Las descripciones de la tarea no están visibles en el Administrador de informes, de modo que si desea  familiarizarse con los roles agregue los usuarios antes de empezar.  
  
-   Si lo desea, personalice los roles o defina roles adicionales para incluir la recopilación de tareas que necesita. Por ejemplo, si piensa usar la configuración de seguridad personalizada para los elementos individuales, quizá desee crear una nueva definición de roles que permita el acceso a la vista de carpetas.  
  
### <a name="to-add-a-user-or-group-to-a-system-role"></a>Para agregar un usuario o un grupo al rol del sistema.  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  Haga clic en **Seguridad**.  
  
4.  Haga clic en **Nueva asignación de roles**.  
  
5.  En **nombre de usuario o grupo**, escriba un usuario de dominio de Windows o grupo cuenta con este formato: \<dominio >\\< cuenta\>. Si utiliza la autenticación de formularios o la seguridad personalizada, especifique la cuenta de grupo o de usuario en el formato correcto para su implementación.  
  
6.  Seleccione un rol del sistema y, a continuación, haga clic en **Aceptar**.  
  
     Los roles son acumulativos, de modo que si selecciona Administrador del sistema y Usuario del sistema, un usuario o grupo podrá realizar las tareas en ambos roles.  
  
7.  Repita el proceso para crear asignaciones para usuarios o grupos adicionales.  
  
### <a name="to-add-a-user-or-group-to-an-item-role"></a>Para agregar un usuario o grupo al rol del elemento  
  
1.  Inicie **Administrador de informes** y busque el elemento de informe para el que desea agregar un usuario o un grupo.  
  
2.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Seguridad**.  
  
4.  Haga clic en **Nueva asignación de roles**.  
  
    > [!NOTE]  
    >  Si un elemento hereda la seguridad de un elemento primario, en la barra de herramientas, haga clic en **Editar seguridad del elemento** para cambiar la configuración de seguridad. A continuación, haga clic en **Nuevo rol de funciones**.  
  
5.  En **nombre de usuario o grupo**, escriba un usuario de dominio de Windows o grupo cuenta con este formato: \<dominio >\\< cuenta\>. Si utiliza la autenticación de formularios o la seguridad personalizada, especifique la cuenta de grupo o de usuario en el formato correcto para su implementación.  
  
6.  Seleccione una o varias definiciones de roles que describan la manera en que el usuario o el grupo va a tener acceso al elemento y, a continuación, haga clic en **Aceptar**.  
  
7.  Repita el proceso para crear asignaciones para usuarios o grupos adicionales.  
  
## <a name="see-also"></a>Vea también  
 (crear-y-administrar-rol-assignments.md)   
 [Nueva asignación de roles: Editar página de asignación de rol &#40;el Administrador de informes&#41;](../new-role-assignment-edit-role-assignment-page-report-manager.md)   
 [Página de propiedades de seguridad, elementos &#40;Administrador de informes&#41;](../security-properties-page-items-report-manager.md)   
 [Asignaciones de roles](role-assignments.md)   
 [Definiciones de roles](role-definitions.md)  
  
  
