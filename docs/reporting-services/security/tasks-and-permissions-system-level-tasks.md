---
description: 'Tareas y permisos: tareas de nivel de sistema'
title: Tareas de nivel de sistema | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- system-level tasks [Reporting Services]
ms.assetid: 7023b388-40b2-4590-b227-115cf380a1e7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 817c695a88cd40e761e5da807856d03658e05022
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497981"
---
# <a name="tasks-and-permissions---system-level-tasks"></a>Tareas y permisos: tareas de nivel de sistema
  Una tarea de nivel de sistema es una colección de permisos relativos a las operaciones correspondientes al sitio del servidor de informes en general. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] también incluye tareas de nivel de elemento que corresponden a elementos específicos. Para obtener más información, vea [Tareas de nivel de elemento](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md). Para obtener más información acerca de tareas y permisos en general, vea [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md).  
  
> [!NOTE]  
>  Si trabaja con estas tareas mediante programación, debe utilizar métodos que admitan tareas de nivel de sistema. Para obtener más información, vea <xref:ReportService2010.ReportingService2010.ListTasks%2A> y <xref:ReportService2010.ReportingService2010.ListRoles%2A>.  
  
## <a name="permissions-in-system-level-tasks"></a>Permisos en tareas de nivel de sistema  
 La siguiente tabla identifica la colección de permisos para cada tarea del sistema. Los permisos se incluyen con fin informativo únicamente, para proporcionar una descripción más exacta de la funcionalidad disponible con cada tarea.  
  
|Tarea|Permisos|  
|----------|-----------------|  
|Ejecutar definiciones de informe|Ejecutar definiciones de informe (el nombre del permiso y la tarea es el mismo)|  
|Generación de eventos|Generar eventos|  
|Trabajos de administración|Leer propiedades del sistema<br /><br /> Actualizar propiedades del sistema|  
|Administrar propiedades del servidor de informes|Leer propiedades del sistema<br /><br /> Actualizar propiedades del sistema|  
|Administrar roles|Crear roles<br /><br /> Eliminar roles<br /><br /> Leer propiedades de roles<br /><br /> Actualizar propiedades de roles|  
|Administrar programaciones compartidas|Crear programaciones|  
|Administrar la seguridad del servidor de informes|Leer directivas de seguridad del sistema<br /><br /> Actualizar directivas de seguridad del sistema|  
|Ver propiedades del servidor de informes|Leer propiedades del sistema|  
|Ver programaciones compartidas|Leer programaciones|  
  
## <a name="see-also"></a>Consulte también  
 [Concesión de permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
