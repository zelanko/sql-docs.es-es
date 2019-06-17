---
title: Supervisión de aplicaciones de capa de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring [SQL Server], data-tier applications
- monitoring server performance [SQL Server], DACs
- data-tier application [SQL Server], monitor
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8fe96b7d84a2e363166238c3e840cac383f443dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918147"
---
# <a name="monitor-data-tier-applications"></a>Supervisar aplicaciones de capa de datos
  Una aplicación de capa de datos (DAC) se puede supervisar desde el **Explorador de Utilidad** y el **Explorador de objetos** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS), junto con las vistas de sistema y las tablas. Además, todos los objetos de la base de datos contenida en la DAC se pueden supervisar usando las técnicas de supervisión de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y base de datos estándar.  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Si implementa una DAC en una instancia administrada del [!INCLUDE[ssDE](../../includes/ssde-md.md)], la información acerca de la DAC implementada se incorpora a la Utilidad de SQL Server la próxima vez que el conjunto de recopilación de utilidades se envíe desde la instancia al punto de control de la utilidad. Después puede ver la información básica de estado acerca de la DAC mediante el **Explorador de la utilidad** [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 El **Explorador de objetos** SSMS muestra información de configuración básica acerca de cada DAC implementada en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)], independientemente de si la instancia está administrada en la utilidad de SQL Server. Además, la base de datos asociada con la DAC implementada puede supervisarse con los mismos procedimientos usados para supervisar cualquier base de datos.  
  
## <a name="using-the-sql-server-utility"></a>Usar la utilidad de SQL Server  
 La página de detalles **Aplicaciones de capa de datos implementadas** del [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** displays a dashboard that reports the resource utilization of all DACs that have been deployed to managed instances of the [!INCLUDE[ssDE](../../includes/ssde-md.md)]. El panel superior de la página de detalles enumera cada DAC implementada con indicadores visuales que muestran si su utilización de los recursos de archivo y CPU está fuera de las directivas definidas para la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona una DAC en la vista de lista, los detalles adicionales se muestran en pestañas en la sección inferior de la página. Para obtener más información sobre la información presentada en la página de detalles, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md).  
  
 Después de usar la página de detalles **Aplicaciones de capa de datos implementadas** para identificar rápidamente las DAC que se infrautilizan o agotan su recurso de hardware, puede hacer planes para resolver los posibles problemas. Varias DAC que no usen totalmente sus recursos de hardware actuales podrían consolidarse en un único servidor, liberando algunos de los servidores para otros usos. Si una DAC está agotando los recursos en su servidor actual, se puede mover a un servidor más grande o se pueden agregar recursos adicionales al servidor actual.  
  
 Las directivas de supervisión de aplicaciones definidas en la página de detalles **Administración de la utilidad** define los límites mínimo y máximo para el uso de recursos. Los administradores de bases de datos pueden personalizar las directivas para que cumplan los límites establecidos por las organizaciones. Por ejemplo, una compañía podría establecer 75% como la utilización máxima de CPU para una DAC, mientras que otra compañía podría establecer en un 80% el máximo. Para obtener más información sobre cómo establecer las directivas de supervisión de aplicaciones, vea [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md).  
  
 Para ver la página de detalles **Aplicaciones de capa de datos implementadas**:  
  
1.  Seleccione el menú **Ver/Explorador de utilidades** .  
  
2.  Conecte el **Explorador de la utilidad** al punto de control de la utilidad (UCP).  
  
3.  Seleccione el menú **Ver/Detalles del Explorador de la utilidad** .  
  
4.  Seleccione el nodo **Aplicaciones de capa de datos implementadas** en el **Explorador de la utilidad**.  
  
 La información de la página de detalles **Aplicaciones de capa de datos implementadas** procede de los datas del almacén de administración de datos que, de forma predeterminada, recopila los datos cada 15 minutos. El intervalo también se puede personalizar usando la página de detalles **Administración de la utilidad** .  
  
## <a name="using-object-explorer"></a>Usar el Explorador de objetos  
 El **Explorador de objetos** de SSMS muestra la información de configuración básica sobre cada DAC implementada en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Se incluyen las dos instancias administradas inscritas en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e instancias independientes que no se pueden ver en el **Explorador de la utilidad**.  
  
 Para ver los detalles de una DAC implementada en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
1.  Seleccione el menú **Ver/Explorador de objetos** .  
  
2.  Conéctese a la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]desde el panel Explorador de objetos.  
  
3.  Seleccione el menú **Ver/Detalles del Explorador de objetos** .  
  
4.  Seleccione el nodo del servidor en **Explorador de objetos** que se asigna a la instancia y, después, navegue hasta el nodo **Administración\Aplicaciones de capa de datos** .  
  
5.  La vista de lista del panel superior de la página de detalles muestra cada DAC implementada en la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Seleccione una DAC para mostrar la información en el panel de detalles, en la parte inferior de la página.  
  
 El menú contextual del nodo **Aplicaciones de capa de datos** también sirve para implementar una nueva DAC o eliminar una existente.  
  
## <a name="using-the-dac-system-views-and-tables"></a>Usar las vistas y tablas de sistema de DAC  
 La tabla de sistema msdb.dbo.sysdac_history_internal registra el éxito o error de todas las acciones de administración de DAC realizadas en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. La tabla registra la hora en que se produjo cada acción y qué inicio de sesión la inició. Para obtener más información, vea [sysdac_history_internal &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/data-tier-application-tables-sysdac-history-internal).  
  
 Las vistas del sistema de DAC notifican información de catálogo básica. Para obtener más información, vea [Aplicación de capa de datos &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances).  
  
## <a name="monitoring-dac-databases"></a>Supervisar las bases de datos de DAC  
 Una vez implementada correctamente una DAC, la base de datos contenida en ella funciona igual que cualquier otra. Utilice técnicas y herramientas estándar de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para supervisar el rendimiento, el registro, los eventos y la utilización de recursos de la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de capa de datos](data-tier-applications.md)   
 [Implementar una aplicación de capa de datos](deploy-a-data-tier-application.md)  
  
  
