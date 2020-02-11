---
title: Página de seguridad (Configuración del sitio. Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: acc9a905-90f8-4544-aec6-b2ab3a1b0015
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6c0b0cc68c73c66dabb237d859aba641fb234647
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102178"
---
# <a name="security-page-site-settings-report-manager"></a>Página de seguridad (Configuración del sitio. Administrador de informes)
  Use la página Seguridad para ver las asignaciones de roles del sistema que controlan el acceso al sitio del servidor de informes. Las asignaciones de roles del sistema existen fuera del ámbito del espacio de nombres o la jerarquía de carpetas del servidor de informes. Son globales y no pueden variar para elementos específicos. Las operaciones que se admiten a través de las asignaciones de roles del sistema incluyen la creación y el uso de las programaciones compartidas, el uso del Generador de informes y el establecimiento de valores predeterminados para algunas características del servidor.  
  
 Al instalar el servidor de informes, se crea una asignación de roles del sistema predeterminada. Esta asignación de roles del sistema concede a los administradores del sistema local permisos para administrar el entorno del servidor de informes. El administrador del sistema local siempre puede configurar la seguridad de un servidor de informes local, aunque se eliminen las asignaciones de roles del sistema.  
  
 Todos los demás usuarios que requieren acceso al Generador de informes o programaciones compartidas deben estar asignados a una asignación de roles del sistema.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-security-page-for-site-settings"></a>Para abrir la página Seguridad para Configuración del sitio  
  
1.  Abra el Administrador de informes.  
  
2.  En la parte superior de la página, haga clic en **Configuración del sitio**. Esto abre la página de propiedades General del sitio.  
  
3.  Selecciona la pestaña **Seguridad**.  
  
## <a name="options"></a>Opciones  
 **Eliminar**  
 Haga clic para eliminar una asignación de roles existente. Antes de hacer clic en **Eliminar**, active la casilla que aparece junto al nombre de grupo o usuario que desea quitar. No puede eliminar una asignación de roles si es la única que permanece. Si se elimina una asignación de roles, no se elimina la cuenta de usuario o grupo ni las definiciones de roles.  
  
 **Nueva asignación de roles**  
 Haga clic para abrir la página Nueva asignación de roles del sistema, que se utiliza para crear asignaciones de roles del sistema adicionales para el sitio del servidor de informes. Para obtener más información, vea [nuevas asignaciones de roles del sistema: página Editar asignaciones de roles del sistema &#40;Administrador de informes&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md).  
  
 **Edición**  
 Haga clic para abrir la página Editar asignaciones de roles del sistema, que se usa para editar las asignaciones de roles del sistema individuales para el sitio del servidor de informes. Para obtener más información, vea [nuevas asignaciones de roles del sistema: página Editar asignaciones de roles del sistema &#40;Administrador de informes&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md).  
  
 **Grupo o usuario**  
 Muestra los grupos y usuarios que forman parte de una asignación de roles existente. Se han definido las asignaciones de roles existentes para la carpeta actual de los grupos y usuarios que se muestran en esta columna. Haga clic en **Editar** junto a un nombre de usuario o grupo para ver o editar los detalles de las asignaciones de roles.  
  
 **Roles**  
 Muestra una o varias definiciones de roles que son parte de una asignación de roles existente. Si se asignan varios roles a una cuenta de usuario o grupo, ese usuario o grupo puede realizar todas las tareas de todos los roles. Para ver el conjunto de tareas que admite cada rol, use [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. No puede ver, crear, modificar ni eliminar roles en el Administrador de informes. Para obtener instrucciones, vea [crear, eliminar o modificar un rol &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md).  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de informes la ayuda F1](../../2014/reporting-services/report-manager-f1-help.md)   
 [Concesión de permisos en un servidor de informes en modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
