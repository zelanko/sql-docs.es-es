---
title: Ver los resultados de la directiva de mantenimiento de recursos (Utilidad de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae549061481b0dde5dca884da8a9f686e54b73eb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>Ver los resultados de la directiva de mantenimiento de recursos (Utilidad de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use el panel de Utilidad de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ver los parámetros de recursos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y aplicaciones de capa de datos. Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>Ver los resultados de la directiva de mantenimiento de recursos de la Utilidad de SQL Server.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS), haga clic en **Ver**y, a continuación, haga clic en **Explorador de Utilidad** para ver el panel de navegación del Explorador de Utilidad. Para ver el panel de contenido, haga clic en **Ver**y, a continuación, haga clic en **Contenido del explorador de la utilidad**.  
  
2.  En el panel de navegación, haga clic en ![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")**Conectar con la utilidad**. Si no ha creado un punto de control de la utilidad (UCP) o si no ha inscrito instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o aplicaciones de capa de datos en la utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
3.  Haga clic en el nodo UCP para ver los datos de resumen para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las aplicaciones de capa de datos (haga clic con el botón derecho para actualizar). Los datos del panel se muestran en el panel de contenido.  
  
4.  Haga clic en el nodo **Instancias administradas** para ver los datos de la vista de lista para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (haga clic con el botón secundario para actualizar). Los datos de la vista de lista se muestran en el panel de contenido.  
  
5.  Haga clic en el nodo **Aplicaciones de capa de datos implementadas** para ver la vista de lista para las aplicaciones de capa de datos (haga clic con el botón derecho para actualizar). Los datos de la vista de lista se muestran en el panel de contenido.  
  
## <a name="see-also"></a>Ver también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)   
 [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)   
 [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)  
  
  
