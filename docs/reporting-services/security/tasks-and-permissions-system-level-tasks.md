---
title: Tareas de nivel de sistema | Documentos de Microsoft
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
- system-level tasks [Reporting Services]
ms.assetid: 7023b388-40b2-4590-b227-115cf380a1e7
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8f8eac1d05b8bdd034879cb2eba1c4fc867fce66
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="tasks-and-permissions---system-level-tasks"></a>Tareas y permisos - tareas de nivel de sistema
  Una tarea de nivel de sistema es una colección de permisos relativos a las operaciones correspondientes al sitio del servidor de informes en general. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] también incluye tareas de nivel de elemento que corresponden a elementos específicos. Para obtener más información, vea [Tareas de nivel de elemento](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md). Para obtener más información acerca de tareas y permisos en general, vea [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md).  
  
> [!NOTE]  
>  Si trabaja con estas tareas mediante programación, debe utilizar métodos que admitan tareas de nivel de sistema. Para obtener más información, consulte <xref:ReportService2010.ReportingService2010.ListTasks%2A> y <xref:ReportService2010.ReportingService2010.ListRoles%2A>.  
  
## <a name="permissions-in-system-level-tasks"></a>Permisos en tareas de nivel de sistema  
 La siguiente tabla identifica la colección de permisos para cada tarea del sistema. Los permisos se incluyen con fin informativo únicamente, para proporcionar una descripción más exacta de la funcionalidad disponible con cada tarea.  
  
|Tarea|Permissions|  
|----------|-----------------|  
|Ejecutar definiciones de informe|Ejecutar definiciones de informe (el nombre del permiso y la tarea es el mismo)|  
|Generar eventos|Generar eventos|  
|Administrar trabajos|Leer propiedades del sistema<br /><br /> Actualizar propiedades del sistema|  
|Administrar propiedades del servidor de informes|Leer propiedades del sistema<br /><br /> Actualizar propiedades del sistema|  
|Administrar roles|Crear roles<br /><br /> Eliminar roles<br /><br /> Leer propiedades de roles<br /><br /> Actualizar propiedades de roles|  
|Administrar programaciones compartidas|Crear programaciones|  
|Administrar la seguridad del servidor de informes|Leer directivas de seguridad del sistema<br /><br /> Actualizar directivas de seguridad del sistema|  
|Ver propiedades del servidor de informes|Leer propiedades del sistema|  
|Ver programaciones compartidas|Leer programaciones|  
  
## <a name="see-also"></a>Vea también  
 [Conceder permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  

