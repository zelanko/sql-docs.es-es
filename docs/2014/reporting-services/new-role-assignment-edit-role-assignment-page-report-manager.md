---
title: 'Nueva asignación de roles: página Editar asignación de roles (Administrador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 3319ced0-4b86-42af-b18d-da41a625113c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a9480b0729e7c08117ba5633c6934eca1903a61b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108157"
---
# <a name="new-role-assignment-edit-role-assignment-page-report-manager"></a>Nueva asignación de roles y Editar asignación de roles (páginas del Administrador de informes)
  Utilice la página Nueva Asignación de roles o Editar asignación de roles para conceder permisos a operaciones y elementos del servidor de informes. Cada usuario que requiere acceso a un servidor de informes debe poseer una asignación de roles que define el nivel de acceso. Puede crear las asignaciones de roles en el nodo raíz o en un determinado informe, modelo, carpeta, recurso u origen de datos compartido. La seguridad de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se establece a través de asignaciones de roles que se aplican a elementos. Una asignación de roles asocia grupos o usuarios a una definición de roles; cada definición de roles identifica las tareas que los grupos o usuarios pueden realizar respecto a un elemento específico.  
  
 Las asignaciones de roles de nivel de elemento pueden tener un gran impacto. Aunque se asocien a un solo informe o a una sola carpeta, si se definen en un nivel alto de la jerarquía de carpetas, las carpetas y los elementos inferiores en el árbol las heredarán. Para obtener más información, vea [conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](security/grant-user-access-to-a-report-server.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-new-role-assignment-or-edit-role-assignment-page"></a>Para abrir la página Nueva asignación de roles o Editar asignación de roles  
  
1.  Abra el Administrador de informes y busque un elemento para el que desea agregar una nueva asignación de roles o modificar una asignación de roles.  
  
2.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Seguridad**. Se abrirá la página de propiedades Seguridad para el elemento.  
  
4.  Si desea agregar una nueva asignación de roles, en la barra de herramientas, haga clic en **Nueva asignación de roles**. Si desea editar una asignación de roles, haga clic en **Editar** junto al nombre de usuario o grupo que desee editar.  
  
    > [!NOTE]  
    >  Si un elemento hereda la seguridad de un elemento primario, en la barra de herramientas, haga clic en **Editar seguridad del elemento** para cambiar la configuración de seguridad.  
  
## <a name="options"></a>Opciones  
 **Nombre de usuario o grupo**  
 Escriba el nombre de una cuenta de usuario o de grupo para la que se va a crear la asignación de roles. El nombre de grupo o de usuario debe ser una cuenta de dominio de Windows. Escriba la cuenta con este formato: \<>\\ de dominio<\>cuenta.  
  
> [!NOTE]  
>  Este cuadro solo está disponible en la página Nueva asignación de roles.  
  
 **Role**  
 Muestra todos los roles definidos en el servidor de informes que se pueden utilizar para definir la seguridad de los elementos. Cuando cree o cambie una asignación de roles para un informe o una carpeta, seleccione uno o varios roles hasta que el conjunto combinado de tareas describa las acciones que el usuario debería poder realizar. Para ver el conjunto de tareas que admite cada rol, use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. No puede ver, crear, modificar ni eliminar roles en el Administrador de informes. Para obtener instrucciones, vea [crear, eliminar o modificar un rol &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md).  
  
 **Descripción**  
 Muestra información adicional sobre el rol. En el caso de los roles predefinidos, como **Explorador** o **Administrador de contenido**, la descripción es un resumen de las tareas que admite cada rol.  
  
 **Eliminar asignación de roles**  
 Haga clic para eliminar una asignación de roles existente correspondiente a un usuario o a un grupo. Una asignación de roles no se puede eliminar si es la única que queda, ya que cada elemento debe tener, como mínimo, una asignación de roles.  
  
> [!NOTE]  
>  Este botón solo está disponible en la página Editar asignación de roles.  
  
## <a name="see-also"></a>Consulte también  
 [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)   
 [Conceder permisos en un servidor de informes en modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Administrador de informes la ayuda F1](../../2014/reporting-services/report-manager-f1-help.md)   
 [Asignaciones de roles](security/role-assignments.md)   
 [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](security/grant-user-access-to-a-report-server.md)  
  
  
