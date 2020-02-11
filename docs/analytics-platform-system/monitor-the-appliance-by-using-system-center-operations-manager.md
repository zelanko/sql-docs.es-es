---
title: Supervisión con SCOM
description: Use System Center Operations Manager (SCOM) para supervisar el dispositivo de Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 0b244d85e601e46fe778298e723c0a7d01e669bb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400969"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>Supervisión con System Center Operations Manager-Analytics Platform System
Use System Center Operations Manager (SCOM) para supervisar el dispositivo de Analytics Platform System (APS).
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Prerequisites  
  
1.  System Center Operations Manager 2007 R2, 2012 o 2012 SP1 debe estar instalado y en ejecución.  
  
2.  SQL Server 2008 R2 Native Client o SQL Server 2012 Native Client deben estar instalados.  
  
3.  Los módulos de administración para supervisar PDW de SQL Server deben estar instalados, importados y configurados. Use los artículos siguientes para obtener instrucciones sobre cómo realizar estas tareas.  
  
    -   [Instale los módulos de administración de SCOM &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)  
  
    -   [Importe el módulo de administración de SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configure SCOM para supervisar Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Para supervisar PDW de SQL Server con SCOM  
Después de configurar los módulos de administración de SCOM, haga clic en el panel supervisión de SCOM y explore en profundidad hasta **SQL Server dispositivo** y, a continuación, **Microsoft SQL Server almacenamiento de datos paralelos**. Debajo Microsoft SQL Server almacenamiento de datos paralelos, hay cuatro opciones: alertas, dispositivos, diagrama de dispositivos y nodos.  
  
### <a name="alerts"></a>Alertas  
Las alertas son donde puede encontrar las alertas actuales para administrar.  
  
![Alertas](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Dota  
Los dispositivos son los lugares en los que encontrará los dispositivos PDW de SQL Server detectados y supervisados actualmente en su entorno. Si un dispositivo no aparece aquí y ha creado la conexión ODBC para él, puede haber algún problema con su cuenta de PDWWatcher. Si aparecen como "sin supervisión", puede haber algún problema con su cuenta de PDWMonitor. Sea paciente, ya que SCOM no realiza cambios en tiempo real, sino que comprueba periódicamente si hay nuevos dispositivos para supervisar y envía consultas periódicamente a los dispositivos para su supervisión.  
  
![Dota](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagrama de dispositivos  
En la página de diagramas de dispositivos puede ver el estado del dispositivo con una vista de árbol:  
  
![Diagrama de dispositivos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nodos  
Por último, la vista de nodos permite ver el estado del dispositivo a través de cada nodo:  
  
![Nodos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Consulte también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Descripción de las alertas de la consola de administración &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
