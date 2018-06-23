---
title: Propiedades de rol del sistema (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 1dce716a55830afa2d7e3bc38d87d9ea407ce95c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112160"
---
# <a name="system-role-properties-management-studio"></a>Propiedades de rol del sistema (Management Studio)
  Use la página Roles del sistema para ver las definiciones de roles del sistema actualmente definidas para el servidor de informes. Una definición de roles del sistema contiene una colección con nombre de tareas que se realizan en relación con el sitio completo, en lugar de un elemento individual. Las definiciones de roles se asignan a un usuario o grupos para crear una asignación de roles. Las tareas de la definición de roles especifican lo que puede hacer el usuario o grupo.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tiene dos definiciones de roles del sistema predefinidos: **Administrador del sistema** y **Usuario del sistema**. Las definiciones de estos roles se pueden modificar cambiando la lista de tareas, o bien, se puede crear un nuevo rol del sistema que admita una combinación distinta de tareas. Al editar una definición de roles, todas las asignaciones de roles que la incluyan se verán afectadas.  
  
> [!NOTE]  
>  Las asignaciones de roles del sistema solamente se usan en un servidor de informes que se ejecuta en modo nativo. Si el servidor de informes está configurado para la integración con SharePoint, esta página no está disponible.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Especifica el nombre de la definición de roles del sistema.  
  
 **Descripción**  
 Muestra una descripción de la definición de roles del sistema. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], esta descripción solo resulta visible en esta página. Los usuarios que ven este elemento a través del Administrador de informes pueden ver esta descripción al examinar la jerarquía de carpetas.  
  
 **Tarea**  
 Muestra todas las tareas del nivel de sistema que se pueden seleccionar para esta definición de roles. Puede agregar o quitar elementos de la lista de tareas predefinidas para definir el modo en que los usuarios tienen acceso a un elemento dado a través de ese rol. No puede crear nuevas tareas y no puede modificar tareas existentes.  
  
 **Descripción**  
 Proporciona información sobre cada tarea. No puede modificar descripciones de tareas.  
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)   
 [Tareas de nivel de sistema](../security/tasks-and-permissions-system-level-tasks.md)   
 [Tareas y permisos](../security/tasks-and-permissions.md)   
 [Roles predefinidos](../security/role-definitions-predefined-roles.md)  
  
  