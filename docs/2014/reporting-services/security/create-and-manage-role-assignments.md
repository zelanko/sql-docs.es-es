---
title: Crear y administrar asignaciones de roles | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- security [Reporting Services], role assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 086d0987-b43c-4834-8372-e08fb4b432f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eed9b1a0deb7e88c85283ea3dc7cab9bf893937f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101996"
---
# <a name="create-and-manage-role-assignments"></a>Crear y administrar asignaciones de roles
  Una *asignación de roles* es una directiva de seguridad que determina si un usuario o un grupo pueden tener acceso a un elemento de servidor de informes específico o realizar una operación. Una asignación de roles consiste en un nombre de cuenta de usuario o de grupo y una o más definiciones de roles.  
  
 El ámbito de las asignaciones de roles es el *nivel de elemento* o el *nivel de sistema*.  
  
-   Una asignación de roles de nivel de elemento siempre se crea en el contexto de un elemento o rama específicos en la jerarquía de carpetas del servidor de informes. Navegue a una carpeta o un elemento específico para crear una asignación de roles para él.  
  
-   Las asignaciones de roles de nivel de sistema proporcionan a usuarios seleccionados la capacidad de realizar tareas que afectan en conjunto al sitio del servidor de informes. Estas tareas incluyen la creación de programaciones compartidas, la administración de trabajos, el procesamiento de informes en el Generador de informes y el establecimiento de propiedades. La seguridad de nivel de sistema no otorga acceso a elementos en la jerarquía de carpetas del servidor de informes.  
  
## <a name="creating-an-item-level-role-assignment"></a>Crear una asignación de roles de nivel de elemento  
 Para crear o administrar asignaciones de roles, utilice el Administrador de informes y abra las páginas de propiedades de Seguridad del elemento que desea proteger.  
  
 Debe crear una asignación de roles independiente para cada cuenta de grupo o de usuario que requiera acceso al servidor de informes. Si la cuenta se encuentra en un dominio diferente del que contiene el servidor de informes, incluya el nombre de dominio. Después de especificar una cuenta, puede elegir una o más definiciones de roles. Las definiciones de roles son aditivas. La asignación admite el conjunto combinado de todas las tareas de todas las definiciones, para un usuario o grupo en particular.  
  
 Para permitir un acceso amplio, debe elegir un elemento en una posición alta de la jerarquía de carpetas (por ejemplo, el nodo raíz Inicio). Después, puede crear las asignaciones de roles subsiguientes para restringir áreas específicas de la jerarquía de carpetas.  
  
 Debe ser miembro del grupo local Administradores del equipo del servidor de informes para crear una asignación de roles. Puede delegar esa responsabilidad asignando otros usuarios al rol **Administrador de contenido** .  
  
 Para obtener más información, vea [conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](grant-user-access-to-a-report-server.md).  
  
## <a name="creating-a-system-level-role-assignment"></a>Crear una asignación de roles de nivel de sistema  
 Para crear o administrar una asignación de roles de nivel de sistema, utilice el Administrador de informes y abra la página de Configuración del sitio.  
  
 Las asignaciones de roles de nivel de sistema y de nivel de elemento van juntas. Debe crear una asignación de roles de nivel de sistema para cada usuario o grupo que tenga una asignación de roles de nivel de elemento.  
  
 Las asignaciones de roles de nivel de sistema incluyen una amplia variedad de permisos, pero no incluyen los que forman parte de una asignación de roles de nivel de elemento. A diferencia de los permisos de sistema de un equipo, los roles de sistema en los servidores de informes no transfieren permisos determinantes que incluyan el conjunto completo de todas las operaciones posibles. En su lugar, las asignaciones de roles de nivel de sistema simplemente son un conjunto de tareas cuyo ámbito es el sitio del servidor de informes. Los permisos que se transfieren a través de las asignaciones de roles de nivel de sistema determinan si los usuarios pueden ver las propiedades de la aplicación (como la imagen o el título de la página Inicio), ver o administrar las programaciones compartidas, o usar el Generador de informes.  
  
 Para más información, vea [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](grant-user-access-to-a-report-server.md) y [Roles predefinidos](role-definitions-predefined-roles.md).  
  
## <a name="modifying-a-role-assignment"></a>Modificar una asignación de roles  
 Puede modificar las asignaciones de roles en cualquier momento. Los cambios surtirán efecto cuando guarde la asignación de roles. Las sesiones de usuarios no se ven afectadas por cambios en la asignación de roles. Si un usuario tiene un informe abierto y se modifica una asignación de roles para denegar el acceso, el usuario puede continuar usando el informe mientras la sesión esté activa.  
  
 Si se agrega una cuenta de usuario a un grupo que ya forme parte de una asignación de roles, habrá un retardo antes de que la cuenta de usuario pueda obtener acceso a los elementos a través de las directivas de la cuenta de grupo. Este retardo se debe a que Internet Information Services (IIS) de Microsoft almacena en caché los tokens de autenticación. También puede esperar a que se actualicen los tokens (por lo general, el período de espera es de quince minutos) o puede restablecer IIS para actualizar la caché de forma inmediata.  
  
 Solo puede modificar una asignación de roles cada vez. No puede llevar a cabo una operación de búsqueda y reemplazo global para cambiar nombres de definiciones de roles o configuraciones de asignaciones de roles, o bien para buscar todas las asignaciones de roles que incluyan un usuario o grupo específico.  
  
## <a name="deleting-a-role-assignment"></a>Eliminar una asignación de roles  
 Puede eliminar asignaciones de roles activando la casilla de cada asignación que desee eliminar y haciendo clic en **Eliminar**. También puede eliminarlas haciendo clic en **Volver a la seguridad del elemento primario**. Cuando haga clic en este botón, las asignaciones de roles existentes para el elemento se eliminarán y se usarán en su lugar las que se proporcionan a través de un elemento primario.  
  
## <a name="see-also"></a>Consulte también  
 [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](grant-user-access-to-a-report-server.md)   
 [Modificar o eliminar una asignación de roles &#40;Administrador de informes&#41;](role-assignments-modify-or-delete.md)   
 [Asignaciones de roles](role-assignments.md)   
 [Definiciones de roles](role-definitions.md)   
 [Roles predefinidos](role-definitions-predefined-roles.md)   
 [Concesión de permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  
