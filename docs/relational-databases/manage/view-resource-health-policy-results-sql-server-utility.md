---
title: Ver los resultados de la directiva de mantenimiento de recursos (Utilidad de SQL Server) | Microsoft Docs
description: Obtenga información sobre cómo usar SQL Server Management Studio para ver los resultados de la directiva de mantenimiento de recursos de la Utilidad de SQL Server para instancias de SQL Server y aplicaciones de capa de datos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a3ec26ba8988f36e3deac88373a932ef377f8d59
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810045"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>Ver los resultados de la directiva de mantenimiento de recursos (Utilidad de SQL Server)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use el panel de Utilidad de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ver los parámetros de recursos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y aplicaciones de capa de datos. Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  

##  <a name="SSMSProcedure"></a>

### <a name="view-sql-server-utility-resource-health-policy-results"></a>Ver los resultados de la directiva de mantenimiento de recursos de la Utilidad de SQL Server.  

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS), seleccione **Ver** y luego **Explorador de la utilidad** para ver el panel de navegación del Explorador de la utilidad. Para ver el panel de contenido, seleccione **Ver** y luego **Contenido del explorador de la utilidad**.  

2. En el panel de navegación, seleccione ![conectar con la utilidad](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")**Conectar con la utilidad**. Si no ha creado un punto de control de la utilidad (UCP) o si no ha inscrito instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o aplicaciones de capa de datos en la utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  

3. Seleccione el nodo UCP a fin de ver los datos de resumen para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las aplicaciones de capa de datos (haga clic con el botón derecho con el fin de actualizar). Los datos del panel se muestran en el panel de contenido.  

4. Seleccione el nodo **Instancias administradas** a fin de ver los datos de la vista de lista para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (haga clic con el botón derecho con el fin de actualizar). Los datos de la vista de lista se muestran en el panel de contenido.  

5. Seleccione el nodo **Aplicaciones de capa de datos implementadas** a fin de ver la vista de lista para las aplicaciones de capa de datos (haga clic con el botón derecho con el fin de actualizar). Los datos de la vista de lista se muestran en el panel de contenido.  

## <a name="see-also"></a>Consulte también

- [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)
- [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130))
- [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](./utility-explorer-f1-help.md)
- [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))