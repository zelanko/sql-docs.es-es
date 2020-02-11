---
title: Tareas y permisos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], tasks
- role-based security [Reporting Services], permissions
- security [Reporting Services], tasks
- security [Reporting Services], permissions
- role-based security [Reporting Services], tasks
- predefined tasks [Reporting Services]
- tasks [Reporting Services]
ms.assetid: d7ff90b5-b976-4270-b9ad-9d7b801d8263
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 01cbf00850c5dd57e7ca1575a1a0cb826c009714
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101457"
---
# <a name="tasks-and-permissions"></a>Tareas y permisos
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], *tareas* son las acciones que un usuario o administrador puede llevar a cabo. Las tareas están predefinidas. No se puede crear tareas personalizadas ni modificar las que se proporcionan ni mediante programación ni con una herramienta. En total, hay veinticinco tareas. Estas tareas comprenden todo el conjunto de operaciones que están disponibles en la seguridad basada en roles. Algunos ejemplos de tareas son "Ver informes", "Administrar informes" y "Administrar propiedades del servidor de informes".  
  
 Cada tarea se compone de un conjunto de permisos, también predefinidos. Por ejemplo, la tarea "Administrar carpetas" contiene los permisos necesarios para crear y eliminar carpetas, así como para ver y actualizar propiedades de carpetas. Los permisos de cada tarea están documentos para proporcionar una descripción más exacta de cada tarea. No es posible interactuar con permisos directamente ni especificarlos en las asignaciones de roles. Los permisos se conceden a los usuarios indirectamente mediante las tareas que se incluyen en las definiciones de rol.  
  
 Las tareas solo se pueden llevar a cabo si forman parte de un rol y dicho rol se incluye en una asignación de roles. Por lo tanto, si la tarea Ver modelos no está incluida en un rol, o ese rol no está incluido en una asignación de roles, los usuarios no podrán ver los modelos de informes. El siguiente diagrama muestra cómo los permisos se combinan para crear tareas y éstas se combinan para crear roles que se pueden utilizar para asignaciones de roles específicas.  
  
 ![Diagrama de tareas y permisos](../media/report-securityobjects.gif "Diagrama de tareas y permisos")  
Diagrama de tareas y permisos  
  
## <a name="system-and-item-level-tasks"></a>Tareas de nivel de sistema y de elemento  
 Las tareas se clasifican en dos categorías: nivel de sistema y nivel de elemento. Un rol puede incluir tareas solo de una categoría. La siguiente tabla describe cada categoría de tareas.  
  
|Category|Descripción|  
|--------------|-----------------|  
|[Tareas de nivel de elemento](tasks-and-permissions-item-level-tasks.md)|Acciones que se realizan con elementos administrados por un servidor de informes, como carpetas, informes, modelos de informe y recursos.<br /><br /> Las tareas de nivel de elemento se centran en el espacio de nombres de las carpetas del servidor de informes. Todos los elementos a los que tiene acceso mediante las carpetas en un servidor de informes o mediante una dirección URL están protegidos por las asignaciones de roles que incluyen tareas de nivel de elemento.|  
|[Tareas de nivel de sistema](tasks-and-permissions-system-level-tasks.md)|Acciones que se realizan en el nivel de sistema, como administrar trabajos o programaciones compartidas que se pueden utilizar con muchos elementos. Las tareas de nivel de sistema se centran fuera del espacio de nombres de carpetas del servidor de informes.|  
  
## <a name="see-also"></a>Consulte también  
 [Definiciones de roles](role-definitions.md)   
 [Roles predefinidos](role-definitions-predefined-roles.md)   
 [Concesión de permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  
