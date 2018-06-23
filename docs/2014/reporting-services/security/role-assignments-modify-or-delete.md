---
title: Modificar o eliminar una asignación de roles (Administrador de informes) | Microsoft Docs
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
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
caps.latest.revision: 44
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 8c68d1b0375fb8fa565ec3b24c59f8a4eab1b066
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111944"
---
# <a name="modify-or-delete-a-role-assignment-report-manager"></a>Modificar o eliminar una asignación de roles (Administrador de informes)
  Una asignación de roles asigna un grupo o cuenta de usuario a una definición de roles predefinida que incluye tareas que se pueden realizar. Determina los tipos de operaciones que un usuario puede realizar con relación a una carpeta, informe, modelo u otro tipo de contenido. Para crear, modificar o eliminar asignaciones de roles, use el Administrador de informes. Después de crear una asignación de roles para un grupo o usuario concreto, puede modificarla posteriormente seleccionando un rol diferente. Si desea revocar los permisos a un servidor de informes, puede eliminar una asignación de roles del servidor de informes.  
  
 Dependiendo de su objetivo, los enfoques alternativos podrían ser más adecuados. Entre los ejemplos se incluyen la personalización o la creación de una nueva definición de roles, o la modificación de la pertenencia de una cuenta de grupo en Active Directory.  
  
 Por ejemplo, supongamos que tiene un grupo de usuarios que necesitan administrar su contenido totalmente, pero que no deberían tener el conjunto completo de permisos asociado al Administrador de contenido. En este caso, podría crear una nueva definición de roles denominada Administrador de contenido del departamento que incluye todas las tareas en Administrador de contenido excepto **Establecer directivas de seguridad para elementos**.  
  
 Del mismo modo, si es un administrador de red o del sistema, y es más sencillo para usted administrar las cuentas de grupo de Active Directory que las asignaciones de roles en el Administrador de informes, podría reducir la sobrecarga de administrar asignaciones de roles creando una asignación de roles única para una cuenta de grupo y ajustar a continuación la pertenencia a grupo cuando los usuarios ya no requieren el acceso a los informes.  
  
 Si determina que el mejor enfoque es la modificación o la eliminación de una asignación de roles, recuerde comprobar las asignaciones de roles del sistema y las asignaciones de roles del elemento. Cada tipo de asignación de roles se configura a través de páginas diferentes del Administrador de informes.  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>Para modificar o eliminar una asignación de roles del sistema  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  Haga clic en **Seguridad**. Todas las asignaciones de roles del nivel de sistema definidas actualmente para el servidor o la implementación escalada aparecen enumeradas por nombre de cuenta.  
  
4.  Busque la asignación de rol que desea modificar o eliminar.  
  
5.  Para agregar o quitar el rol para un usuario o grupo determinado, haga clic en **Editar**.  
  
6.  Para eliminar una asignación de rol, active la casilla situada junto al nombre de usuario o grupo y, a continuación, haga clic en **Eliminar**.  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>Para modificar o eliminar una asignación de roles de elemento  
  
1.  Inicie el **Administrador de informes** y busque el elemento para el que desea modificar o eliminar una asignación de roles.  
  
2.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Seguridad**.  
  
4.  Busque la asignación de rol que desea modificar o eliminar.  
  
5.  Para agregar o quitar el rol para un usuario o grupo determinado, haga clic en **Editar**.  
  
6.  Para eliminar una asignación de rol, active la casilla situada junto al nombre de usuario o grupo y, a continuación, haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Vea también  
 (crear-y-administrar-rol-assignments.md)   
 [Asignaciones de roles](role-assignments.md)   
 [Página Configuración del sitio &#40;Administrador de informes&#41;](../site-settings-page-report-manager.md)   
 [Nueva asignación de roles del sistema y Editar asignaciones de roles del sistema &#40;páginas del Administrador de informes&#41;](../new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)  
  
  