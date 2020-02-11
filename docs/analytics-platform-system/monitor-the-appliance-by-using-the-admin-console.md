---
title: Supervisión con la consola de administración
description: En Analytics Platform System, la consola de administración es una aplicación web que muestra la información sobre el estado, el estado y el rendimiento del dispositivo. Los usuarios se conectan a la consola de administración a través de un explorador de Internet.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 977e38016fbb58356d22ccfc5f783539e5f852d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400943"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>Supervisar el dispositivo con la consola de administración-Analytics Platform System
La consola de administración es una PDW de SQL Server aplicación web que muestra la información sobre el estado, el estado y el rendimiento del dispositivo. Los usuarios se conectan a la consola de administración a través de Internet Explorer.  
  
## <a name="About"></a>Acerca de la consola de administración  
![Inicio de la consola del dispositivo](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Producto**  
Inicio  
Proporciona un resumen rápido del estado del dispositivo.  
  
Health  
Muestra la topología del dispositivo con indicadores que muestran el estado de cada componente supervisado dentro de cada nodo. Permite ver el estado actual de los nodos y propiedades individuales de los componentes de nodo.  
  
Muestra alertas de hardware y software.  
  
Monitor de rendimiento  
Muestra gráficos del monitor de rendimiento.  
  
**Almacenamiento de datos paralelos**  
Inicio  
Proporciona un resumen rápido del estado de PDW.  
  
Sesiones  
Muestra las sesiones de usuario de PDW activas. Esto puede ayudar a supervisar la contención de recursos.  
  
Consultas  
Muestra una lista de las consultas en ejecución y las consultas completadas recientemente. Muestra errores relacionados, si los hay. También proporciona la capacidad de ver los detalles del plan de ejecución de consultas y la información de ejecución de los nodos.  
  
Cargas  
Muestra los planes de carga, el estado actual de las cargas de PDW y los errores relacionados, si los hay.  
  
Copias de seguridad y restauraciones  
Muestra un registro de las operaciones de restauración y copia de seguridad de PDW.  
  
Health  
Muestra la topología de PDW con indicadores que muestran el estado de cada componente supervisado dentro de cada nodo. Permite ver el estado actual de los nodos y propiedades individuales de los componentes de nodo.  
  
Muestra alertas de hardware y software.  
  
Recursos  
Muestra una lista de bloqueos de recursos de PDW y su estado actual.  
  
Storage  
Resume el uso del almacenamiento de PDW.  
  
Monitor de rendimiento  
Muestra gráficos del monitor de rendimiento de PDW.  
 
> [!NOTE]  
> La consola de administración tiene una resolución de pantalla de 1024 x 768. La consola de administración se muestra mejor con una resolución de pantalla de 1280 X 1024 o superior.  
  
## <a name="Connect"></a>Conectar con la consola de administración  
Para conectarse a la consola de administración, requiere:  
  
-   Al menos Internet Explorer versión 10.  
  
-   Permisos para tener acceso a la consola de administración. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Dirección IP del clúster de nodo de control.  Obtenerlo del administrador de PDW de SQL Server.  
  
Para conectarse a la consola de administración, use Internet Explorer y https para ir a la dirección IP del clúster de nodo de control. Por ejemplo, si la dirección IP del clúster de nodo de control `10.192.63.102`es, `https://10.192.63.102` escriba en la barra de direcciones del explorador. La primera pantalla solicitará el **Inicio de sesión** y la **contraseña**. Proporcione un inicio de sesión de autenticación de SQL Server y una contraseña, o un inicio de sesión de autenticación de Windows y una contraseña de Windows. Si usa un inicio de sesión de autenticación de Windows, la consola de administración utilizará la suplantación.  
  
## <a name="RelatedTasks"></a>Tareas de la consola de administración  
La consola de administración de proporciona la capacidad de supervisar lo siguiente:  
  
|||  
|-|-|  
|**Tipo de información**|**Cómo obtener acceso en la consola de administración**|  
|Estado general del dispositivo|Haga clic en **Estado del dispositivo** en el menú superior o en **Inicio**.|  
|Alertas|Haga clic en **Alertas**. Para obtener más información, consulte Descripción de las alertas de la [consola de administración &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md).|  
|Componentes del dispositivo y su estado|Haga clic en **Estado del dispositivo** en el menú superior o en **Inicio**.|  
|Supervisión de solicitudes (incluidas las consultas, las cargas, las copias de seguridad y las restauraciones)|Haga clic en **sesiones** para ver las sesiones actuales o recientes.<br /><br />Haga clic en **consultas** para ver las consultas actualmente activas o recientes. La información que se muestra para las consultas incluye cargas, copias de seguridad y restauraciones.<br /><br />Haga clic en **bloqueos** para ver los bloqueos activos.|  
|Supervise la información adicional para las cargas, copias de seguridad y restauraciones.|Haga clic en **cargas** o **copias de seguridad/restauraciones**.|  
|Información de rendimiento|Haga clic en **monitor de rendimiento**.|  
  
## <a name="see-also"></a>Consulte también  
[Supervisión de dispositivos &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
