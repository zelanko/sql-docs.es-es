---
title: "Supervisar el dispositivo mediante la consola de administración (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 294ba6ac-b1ff-46ea-ba32-d8b32cb4cdc2
caps.latest.revision: "26"
ms.openlocfilehash: c9a2d9e7191a1f362dfc998254f69a2a71e32aac
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-the-appliance-by-using-the-admin-console"></a>Supervisar el dispositivo mediante la consola de administración
La consola de administración es una aplicación web de SQL Server PDW que presenta la información de estado, el estado y el rendimiento del equipo. Los usuarios conectarse a la consola de administración a través de Internet Explorer.  
  
## <a name="About"></a>Acerca de la consola de administración  
![Inicio de la consola de dispositivo](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Dispositivo**  
Inicio  
Proporciona un rápido resumen del estado del dispositivo.  
  
Mantenimiento  
Muestra la topología de dispositivos con indicadores que muestran el estado de cada componente supervisado dentro de cada nodo. Le permite ver el estado actual de los nodos individuales y las propiedades de los componentes del nodo.  
  
Muestra las alertas de hardware y software.  
  
Monitor de rendimiento  
Muestra los gráficos del monitor de rendimiento.  
  
**Almacenamiento de datos paralelos**  
Inicio  
Proporciona un resumen rápido del estado PDW.  
  
Sesiones  
Muestra las sesiones de usuario activas de PDW. Esto puede ayudar a para la supervisión de contención de recursos.  
  
Consultas  
Muestra una lista de las consultas en ejecución y las consultas de completado recientemente. Muestra los errores relacionados, si lo hay. También proporciona la capacidad para ver los detalles de la información de ejecución de plan y el nodo de ejecución de consulta.  
  
Cargas  
Muestra carga planes, el estado actual de cargas PDW y errores relacionados, si lo hay.  
  
Las copias de seguridad/restauraciones  
Muestra un registro de PDW de copia de seguridad y las operaciones de restauración.  
  
Mantenimiento  
Muestra la topología PDW con indicadores que muestran el estado de cada componente supervisado dentro de cada nodo. Le permite ver el estado actual de los nodos individuales y las propiedades de los componentes del nodo.  
  
Muestra las alertas de hardware y software.  
  
Recursos  
Muestra una lista de bloqueos de recursos PDW y su estado actual.  
  
Almacenamiento  
Resume la utilización de almacenamiento PDW.  
  
Monitor de rendimiento  
Muestra los gráficos de monitor de rendimiento de PDW.  
  
**HDInsight**  
Inicio  
Proporciona un resumen rápido del estado de HDInsight.  
  
HDFS  
Resume el uso de espacio de HDInsight y enumera los principales consumidores de espacio de 10.  
  
Asignación/reducción  
Resume el estado de los trabajos de MapReduce.  
  
Mantenimiento  
Muestra la topología de HDInsight con indicadores que muestran el estado de cada componente supervisado dentro de cada nodo. Le permite ver el estado actual de los nodos individuales y las propiedades de los componentes del nodo.  
  
Muestra las alertas de hardware y software.  
  
Almacenamiento  
Resume la utilización de almacenamiento de HDInsight.  
  
Monitor de rendimiento  
Muestra los gráficos del monitor de rendimiento.  
  
> [!NOTE]  
> La consola de administración tiene una resolución de pantalla de 1024 x 768. La consola de administración muestra mejor con una resolución de pantalla de 1280 X 1024 o superior.  
  
## <a name="Connect"></a>Conectarse a la consola de administración  
Para conectarse a la consola de administración, necesita:  
  
-   Al menos Internet Explorer versión 10.  
  
-   Permisos para tener acceso a la consola de administración. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   La dirección IP del clúster de nodo de Control.  Obtener desde el Administrador de SQL Server PDW.  
  
Para conectarse a la consola de administración, use Internet Explorer y https para ir a la dirección IP del clúster de nodo de Control. Por ejemplo, si la dirección IP del clúster de nodo de Control es `10.192.63.102`, escriba `https://10.192.63.102` en la barra de direcciones del explorador. La primera pantalla, se solicitará la **inicio de sesión** y **contraseña**. Proporcionar un inicio de sesión de autenticación de SQL Server y contraseña, o bien un inicio de sesión de autenticación de Windows y contraseña de Windows. Si utiliza un inicio de sesión de autenticación de Windows, la consola de administración utilizará la suplantación.  
  
## <a name="RelatedTasks"></a>Tareas de la consola de administración  
La consola de administración proporciona la capacidad para supervisar los siguientes:  
  
|||  
|-|-|  
|**Tipo de información**|**Cómo obtener acceso a en la consola de administración**|  
|Estado general del dispositivo|Haga clic en **estado de dispositivo** en el menú superior, o **inicio**.|  
|Alertas|Haga clic en **alertas**. Para obtener más información, vea [conceptos básicos sobre alertas de consola de administración &#40; Sistema de la plataforma de análisis &#41; ](understanding-admin-console-alerts.md).|  
|Componentes de dispositivo y su estado|Haga clic en **estado de dispositivo** en el menú superior, o **inicio**.|  
|Solicitudes de monitor (incluidas las consultas, carga, las copias de seguridad y restauraciones)|Haga clic en **sesiones** para ver sesiones actualmente activas o recientes.<br /><br />Haga clic en **consultas** para ver consultas actualmente activas o recientes. La información mostrada para consultas incluye cargas, las copias de seguridad y restauraciones.<br /><br />Haga clic en **bloqueos** para ver los bloqueos activos.|  
|Supervisar la información adicional de carga, las copias de seguridad y restauraciones.|Haga clic en **cargas** o **copias de seguridad/restauraciones**.|  
|Información de rendimiento|Haga clic en **Monitor de rendimiento**.|  
  
## <a name="see-also"></a>Vea también  
[Supervisión de dispositivo &#40; Sistema de la plataforma de análisis &#41;](appliance-monitoring.md)  
  
