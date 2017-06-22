---
title: Propiedades de rol de sistema (Management Studio) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68038228fd6fb7b2af8dd6f1bb5ae50b7f63daac
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="system-role-properties-management-studio"></a>Propiedades de rol del sistema (Management Studio)
  Use la página Roles del sistema para ver las definiciones de roles del sistema actualmente definidas para el servidor de informes. Una definición de roles del sistema contiene una colección con nombre de tareas que se realizan en relación con el sitio completo, en lugar de un elemento individual. Las definiciones de roles se asignan a un usuario o grupos para crear una asignación de roles. Las tareas de la definición de roles especifican lo que puede hacer el usuario o grupo.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tiene dos definiciones de roles del sistema predefinidos: **Administrador del sistema** y **Usuario del sistema**. Las definiciones de estos roles se pueden modificar cambiando la lista de tareas, o bien, se puede crear un nuevo rol del sistema que admita una combinación distinta de tareas. Al editar una definición de roles, todas las asignaciones de roles que la incluyan se verán afectadas.  
  
> [!NOTE]  
>  Las asignaciones de roles del sistema solamente se usan en un servidor de informes que se ejecuta en modo nativo. Si el servidor de informes está configurado para la integración con SharePoint, esta página no está disponible.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Especifica el nombre de la definición de roles del sistema.  
  
 **Description**  
 Muestra una descripción de la definición de roles del sistema. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], esta descripción solo resulta visible en esta página. Los usuarios que ven este elemento a través del Administrador de informes pueden ver esta descripción al examinar la jerarquía de carpetas.  
  
 **Tarea**  
 Muestra todas las tareas del nivel de sistema que se pueden seleccionar para esta definición de roles. Puede agregar o quitar elementos de la lista de tareas predefinidas para definir el modo en que los usuarios tienen acceso a un elemento dado a través de ese rol. No puede crear nuevas tareas y no puede modificar tareas existentes.  
  
 **Description**  
 Proporciona información sobre cada tarea. No puede modificar descripciones de tareas.  
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Tareas de nivel de sistema](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)   
 [Tareas y permisos](../../reporting-services/security/tasks-and-permissions.md)   
 [Roles predefinidos](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
