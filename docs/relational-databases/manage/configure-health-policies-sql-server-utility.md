---
title: Configurar las directivas de mantenimiento (utilidad de SQL Server) | Microsoft Docs
description: Descubra cómo configurar directivas de mantenimiento que impliquen el uso del procesador y el espacio de archivo para las aplicaciones de capa de datos y las instancias administradas de SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 75b2f80a8f2d8aeed3bb5858c8de7dd07ef1419c
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868693"
---
# <a name="configure-health-policies-sql-server-utility"></a>Configurar las directivas de mantenimiento (utilidad de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use el panel de Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ver los parámetros de recursos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y aplicaciones de capa de datos. Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Para ver los resultados de la directiva de mantenimiento de la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , conéctese a un punto de control de la utilidad desde [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obtener más información, vea [Utilizar el explorador de Utilidad para administrar la utilidad de SQL Server](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Las directivas de mantenimiento de la utilidad se pueden configurar para las aplicaciones de capa de datos y las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las directivas de mantenimiento se pueden definir globalmente para todas las aplicaciones de capa de datos y las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o bien se pueden definir individualmente para cada aplicación de capa de datos y para cada instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="monitoring-policies-for-data-tier-applications"></a>Directivas de supervisión para aplicaciones de capa de datos  
 Las directivas de sobreutilización e infrautilización para las aplicaciones de capa de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son como sigue:  
  
-   Uso del procesador en la aplicaciones de capa de datos.  
  
-   Espacio de archivo de aplicación de capa de datos para los archivos de base de datos.  
  
-   Espacio de archivo de aplicación de capa de datos para los volúmenes de almacenamiento.  
  
-   Uso del procesador del sistema informático.  
  
> [!NOTE]  
>  El uso de los volúmenes de almacenamiento y del procesador son directivas de solo lectura para las aplicaciones de capa de datos.  
  
 Para obtener más información sobre la visualización o modificación de directivas de supervisión globales para las aplicaciones de capa de datos, vea [Administración de utilidades &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130)).  
  
 Para obtener más información sobre la visualización o modificación de directivas de supervisión para aplicaciones individuales de capa de datos, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130)).  
  
## <a name="monitoring-policies-for-managed-instances-of-sql-server"></a>Directivas de supervisión para instancias administradas de SQL Server  
 Las directivas de sobreutilización e infrautilización para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son como sigue:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para archivos de base de datos.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para volúmenes de almacenamiento.  
  
-   Uso del procesador del sistema informático.  
  
 Para obtener más información sobre la visualización o modificación de directivas de supervisión globales para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Administración de utilidades &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130)).  
  
 Para obtener más información sobre la visualización o modificación de directivas de supervisión para instancias individuales administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](./utility-explorer-f1-help.md).  
  
## <a name="see-also"></a>Consulte también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
