---
title: Monitor de consola de administración - Analytics Platform System | Microsoft Docs
description: Para Analytics Platform System, la consola de administración es una aplicación web que presenta la información de estado, el estado y rendimiento del dispositivo. Los usuarios conectarse a la consola de administración a través de un explorador de internet.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d094f809052222238806e679e38c6578422fd9aa
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909855"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>Supervisar el dispositivo con la consola de administración - Analytics Platform System
La consola de administración es una aplicación web de PDW de SQL Server que presenta la información de estado, el estado y rendimiento del dispositivo. Los usuarios conectarse a la consola de administración a través de Internet Explorer.  
  
## <a name="About"></a>Acerca de la consola de administración  
![Inicio de la consola de dispositivo](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Dispositivo**  
Inicio  
Proporciona un resumen rápido del estado del dispositivo.  
  
Estado  
Muestra la topología del dispositivo con indicadores que muestra el estado de cada componente supervisado dentro de cada nodo. Permite ver el estado actual de los nodos individuales y las propiedades de los componentes del nodo.  
  
Muestra las alertas de hardware y software.  
  
Monitor de rendimiento  
Muestra los gráficos de monitor de rendimiento.  
  
**Almacenamiento de datos paralelos**  
Inicio  
Proporciona un resumen rápido del estado PDW.  
  
Sesiones  
Muestra las sesiones de usuario activas de PDW. Esto puede ayudar a para la supervisión de contención de recursos.  
  
Consultas  
Muestra una lista de consultas de ejecución y completados recientemente. Muestra los errores relacionados, si existe. También proporciona la capacidad para ver los detalles de la información de ejecución de plan y el nodo de ejecución de consulta.  
  
Cargas  
Muestra carga los planes, el estado actual de las cargas de PDW y errores relacionados, si existe.  
  
Las copias de seguridad/restauraciones  
Muestra un registro de PDW de copia de seguridad y las operaciones de restauración.  
  
Estado  
Muestra la topología PDW con indicadores que muestra el estado de cada componente supervisado dentro de cada nodo. Permite ver el estado actual de los nodos individuales y las propiedades de los componentes del nodo.  
  
Muestra las alertas de hardware y software.  
  
Recursos  
Muestra una lista de bloqueos de recursos PDW y su estado actual.  
  
Storage  
Resume el uso de almacenamiento PDW.  
  
Monitor de rendimiento  
Muestra los gráficos de monitor de rendimiento de PDW.  
 
> [!NOTE]  
> La consola de administración tiene una resolución de pantalla de 1024 x 768. La consola de administración muestra mejor con una resolución de pantalla de 1280 X 1024 o superior.  
  
## <a name="Connect"></a>Conectarse a la consola de administración  
Para conectarse a la consola de administración, necesita:  
  
-   Al menos Internet Explorer versión 10.  
  
-   Permisos de acceso a la consola de administración. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   La dirección IP del clúster de nodo de Control.  Obtenerlo desde el Administrador de SQL Server PDW.  
  
Para conectarse a la consola de administración, use Internet Explorer y https para ir a la dirección IP del clúster de nodo de Control. Por ejemplo, si la dirección IP del clúster de nodo de Control es `10.192.63.102`, escriba `https://10.192.63.102` en la barra de direcciones del explorador. La primera pantalla solicitará su **inicio de sesión** y **contraseña**. Proporcionar un inicio de sesión de autenticación de SQL Server y contraseña, o bien un inicio de sesión de autenticación de Windows y contraseña de Windows. Si usa un inicio de sesión de autenticación de Windows, la consola de administración utilizará la suplantación.  
  
## <a name="RelatedTasks"></a>Tareas de la consola de administrador  
La consola de administración proporciona la capacidad para supervisar lo siguiente:  
  
|||  
|-|-|  
|**Tipo de información**|**Cómo obtener acceso a en la consola de administración**|  
|Estado general del dispositivo|Haga clic en **estado de dispositivo** en el menú superior, o **inicio**.|  
|Trabajos|Haga clic en **alertas**. Para obtener más información, consulte [información sobre las alertas de la consola de administrador &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md).|  
|Componentes de dispositivo y su estado|Haga clic en **estado de dispositivo** en el menú superior, o **inicio**.|  
|Solicitudes de monitor (incluidas las consultas, las cargas, las copias de seguridad y restauraciones)|Haga clic en **sesiones** para ver sesiones actualmente activas o recientes.<br /><br />Haga clic en **consultas** para ver consultas actualmente activas o recientes. La información que aparece para las consultas incluye cargas, las copias de seguridad y restauraciones.<br /><br />Haga clic en **bloqueos** para ver los bloqueos activos.|  
|Supervisar la información adicional para las cargas, las copias de seguridad y restauraciones.|Haga clic en **cargas** o **copias de seguridad/restauraciones**.|  
|Información de rendimiento|Haga clic en **Monitor de rendimiento**.|  
  
## <a name="see-also"></a>Vea también  
[Supervisión del dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
