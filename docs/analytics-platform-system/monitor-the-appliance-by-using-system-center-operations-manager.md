---
title: Dispositivo de monitor con System Center Operations Manager (APS)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de6cbf6e-f2e9-4877-94df-9c13b1182d56
caps.latest.revision: "14"
ms.openlocfilehash: 47a89b19a93d99bb3e63925b012bb53d169fdf0d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="monitor-the-appliance-by-using-system-center-operations-manager"></a>Supervisar el dispositivo mediante el uso de System Center Operations Manager
Describe cómo usar System Center Operations Manager para supervisar SQL Server PDW y HDInsight.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
### <a name="prerequisites"></a>Prerequisites  
  
1.  System Center Operations Manager 2007 R2, 2012 o 2012 SP1 debe estar instalado y ejecutándose.  
  
2.  Debe tener instalado SQL Server 2008 R2 Native Client o SQL Server 2012 Native Client.  
  
3.  Los módulos de administración para supervisar SQL Server PDW y HDInsight se deben instalar, importar y configurar. Utilice las siguientes instrucciones para realizar estas tareas.  
  
    -   [Instalar los módulos de administración de SCOM &#40; Sistema de la plataforma de análisis &#41;](install-the-scom-management-packs.md)  
  
    -   [Importar el módulo de administración de SCOM para PDW &#40; Sistema de la plataforma de análisis &#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configurar SCOM para supervisar el sistema de la plataforma de análisis &#40; Sistema de la plataforma de análisis &#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Para supervisar SQL Server PDW con SCOM  
Después de configurar los módulos de administración de SCOM, haga clic en el panel de supervisión de SCOM y profundizar en **SQL Server Appliance** y, a continuación, **Microsoft SQL Server Parallel Data Warehouse**. Debajo de Microsoft SQL Server Parallel Data Warehouse, hay cuatro opciones: alertas, dispositivos, diagrama de dispositivo y nodos.  
  
### <a name="alerts"></a>Trabajos  
Las alertas son dónde puede encontrar las alertas actuales para administrar.  
  
![Alertas](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Dispositivos  
Los dispositivos son donde encontrará los dispositivos detectados y supervisados actualmente SQL Server PDW en su entorno. Si un dispositivo no se muestra aquí y ha creado la conexión de ODBC que, a continuación, puede haber algún problema con su cuenta de PDWWatcher. Si aparecen como "No supervisado" puede haber algún problema con su cuenta de PDWMonitor. Tenga paciencia SCOM no realizar cambios en tiempo real, pero comprueba periódicamente si hay nuevos dispositivos supervisar y periódicamente envía consultas a los dispositivos para su supervisión.  
  
![Dispositivos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagrama de dispositivos  
La página de diagrama de dispositivos es donde puede obtener un vistazo el estado de su dispositivo con una vista de árbol:  
  
![Diagrama de dispositivos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nodos  
Por último, la nodos vista le permite ver el estado de su dispositivo a través de cada nodo:  
  
![Nodos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Conceptos básicos sobre alertas de consola de administración &#40; Sistema de la plataforma de análisis &#41;](understanding-admin-console-alerts.md)  
  
