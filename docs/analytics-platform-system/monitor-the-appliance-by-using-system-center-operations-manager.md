---
title: Monitor con SCOM - Analytics Platform System | Microsoft Docs
description: Use System Center Operations Manager (SCOM) para supervisar la aplicación Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3c43734dbd7ef1a766f3f1258f97565ab82e175d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639851"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>Supervisión con System Center Operations Manager: Analytics Platform System
Use System Center Operations Manager (SCOM) para supervisar la aplicación Analytics Platform System (APS).
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Requisitos previos  
  
1.  System Center Operations Manager 2007 R2, 2012 o 2012 SP1 debe estar instalado y ejecutándose.  
  
2.  Debe tener instalado SQL Server 2008 R2 Native Client o SQL Server 2012 Native Client.  
  
3.  Los módulos de administración para supervisar SQL Server PDW deben ser instalados, importados y configurados. Utilice los siguientes artículos para obtener instrucciones para realizar estas tareas.  
  
    -   [Instalar los módulos de administración de SCOM &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)  
  
    -   [Importar el módulo de administración de SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configuración de SCOM para supervisar Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Para supervisar SQL Server PDW con SCOM  
Después de configurar los módulos de administración de SCOM, haga clic en el panel de supervisión de SCOM y profundice para **SQL Server Appliance** y, a continuación, **almacenamiento de datos paralelos de Microsoft SQL Server**. Debajo de Microsoft SQL Server Parallel Data Warehouse, hay cuatro opciones: Las alertas, dispositivos, diagrama de dispositivo y los nodos.  
  
### <a name="alerts"></a>Alertas  
Las alertas son donde puede encontrar las alertas actuales para administrar.  
  
![Alerts](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Dispositivos  
Los dispositivos son donde encontrará los dispositivos detectados y supervisados actualmente SQL Server PDW en su entorno. Si un dispositivo no se muestra aquí y que ha creado la conexión de ODBC para ella, a continuación, puede haber algún problema con su cuenta PDWWatcher. Si muestra como "Sin supervisión", puede haber algún problema con su cuenta PDWMonitor. Tenga paciencia, puesto que SCOM no realiza cambios en tiempo real, pero comprueba periódicamente nuevos dispositivos supervisar y envía periódicamente las consultas a dispositivos para la supervisión.  
  
![Appliances](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagrama de dispositivos  
La página de diagrama de dispositivos es donde puede obtener un vistazo el estado de su dispositivo con una vista de árbol:  
  
![Diagrama de dispositivos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nodos  
Por último, la vista de nodos permite ver el estado del dispositivo a través de cada nodo:  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Alertas de la consola de administración de conocimiento &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
