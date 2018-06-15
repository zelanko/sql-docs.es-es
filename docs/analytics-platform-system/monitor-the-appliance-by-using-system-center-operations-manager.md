---
title: Monitor con SCOM - sistema de la plataforma de análisis | Documentos de Microsoft
description: Use System Center Operations Manager (SCOM) para supervisar el dispositivo Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2b26462ab37cf7d63960ff7db6e20c57e8290bb
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538985"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>Monitor con System Center Operations Manager - sistema de la plataforma de análisis
Use System Center Operations Manager (SCOM) para supervisar el dispositivo Analytics Platform System (APS).
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
### <a name="prerequisites"></a>Requisitos previos  
  
1.  System Center Operations Manager 2007 R2, 2012 o 2012 SP1 debe estar instalado y ejecutándose.  
  
2.  Debe tener instalado SQL Server 2008 R2 Native Client o SQL Server 2012 Native Client.  
  
3.  Los módulos de administración para supervisar SQL Server PDW y HDInsight se deben instalar, importar y configurar. Utilice los siguientes artículos para obtener instrucciones para realizar estas tareas.  
  
    -   [Instalar los módulos de administración de SCOM &#40;sistema de la plataforma de análisis&#41;](install-the-scom-management-packs.md)  
  
    -   [Importar el módulo de administración de SCOM para PDW &#40;sistema de la plataforma de análisis&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configurar SCOM para supervisar el sistema de la plataforma de análisis &#40;sistema de la plataforma de análisis&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Para supervisar SQL Server PDW con SCOM  
Después de configurar los módulos de administración de SCOM, haga clic en el panel de supervisión de SCOM y profundizar en **SQL Server Appliance** y, a continuación, **Microsoft SQL Server Parallel Data Warehouse**. Debajo de Microsoft SQL Server Parallel Data Warehouse, hay cuatro opciones: alertas, dispositivos, diagrama de dispositivo y nodos.  
  
### <a name="alerts"></a>Alertas  
Las alertas son dónde puede encontrar las alertas actuales para administrar.  
  
![Alertas](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Dispositivos  
Los dispositivos son donde encontrará los dispositivos detectados y supervisados actualmente SQL Server PDW en su entorno. Si un dispositivo no se muestra aquí y ha creado la conexión de ODBC que, a continuación, puede haber algún problema con su cuenta de PDWWatcher. Si muestra como "No supervisado", puede haber algún problema con su cuenta de PDWMonitor. Tenga paciencia ya que SCOM no realizar cambios en tiempo real, pero comprueba periódicamente si hay nuevos dispositivos supervisar y periódicamente envía consultas a los dispositivos para su supervisión.  
  
![Dispositivos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagrama de dispositivos  
La página de diagrama de dispositivos es donde puede obtener un vistazo el estado de su dispositivo con una vista de árbol:  
  
![Diagrama de dispositivos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nodos  
Por último, la nodos vista le permite ver el estado de su dispositivo a través de cada nodo:  
  
![Nodos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Las alertas de la consola de administración de conocimiento &#40;sistema de la plataforma de análisis&#41;](understanding-admin-console-alerts.md)  
  
