---
title: Controlador ODBC en Linux y macOS - alta disponibilidad y recuperación ante desastres | Documentos de Microsoft
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e69df64ad4e5c5e5319719fe14f380c745b0aeba
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>Controlador ODBC en Linux y macOS compatibilidad con alta disponibilidad y recuperación ante desastres
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Los controladores ODBC para la compatibilidad con Linux y Mac OS [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obtener más información acerca de [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], consulte:  
  
-   [Agentes de escucha del grupo de disponibilidad, conectividad de cliente y conmutación por error de aplicación (SQL Server)](http://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [Creación y configuración de grupos de disponibilidad (SQL Server)](http://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [Agrupación en clústeres de conmutación por error y grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [Secundarias activas: Réplicas secundarias legibles (grupos de disponibilidad AlwaysOn)](http://msdn.microsoft.com/library/ff878253.aspx)  
  
Puede especificar el agente de escucha del grupo de disponibilidad de un determinado grupo de disponibilidad en la cadena de conexión. Si una aplicación ODBC en Linux o Mac OS está conectada a una base de datos en un grupo de disponibilidad que conmuta por error, se pierde la conexión original y la aplicación debe abrir una conexión nueva para seguir trabajando después de la conmutación por error.

Los controladores ODBC en Linux y macOS iteración secuencialmente todas las direcciones IP asociadas con un nombre de host DNS si no se está conectando a un agente de escucha del grupo de disponibilidad y hay varias direcciones IP asociadas con el nombre de host.

Si la primera dirección IP devuelta del servidor DNS no es conectable, estas iteraciones pueden llevar mucho tiempo. Al conectarse a un agente de escucha del grupo de disponibilidad, el controlador intenta establecer conexiones con todas las direcciones IP en paralelo. Si un intento de conexión se realiza correctamente, el controlador descarta todos los intentos de conexión pendiente.

> [!NOTE]  
> Dado que una conexión puede fallar debido a una conmutación por error del grupo de disponibilidad, implementar lógica de reintento de conexión; Vuelva a intentar una conexión con errores hasta que se vuelve a conectar. El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de establecer una conexión con un grupo de disponibilidad.

## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover

Especifique siempre **MultiSubnetFailover = Yes** (o **= True**) cuando se conecta a un [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] agente de escucha del grupo de disponibilidad o [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] instancia de clúster de conmutación por error. **MultiSubnetFailover** permite más rápida conmutación por error para todos los grupos de disponibilidad y una instancia de clúster de conmutación por error en [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]. **MultiSubnetFailover** también reduce considerablemente el tiempo de conmutación por error para las topologías de AlwaysOn y de varias subredes. Durante una conmutación por error de varias subredes, el cliente intentará establecer conexiones en paralelo. Durante una conmutación por error de subred, el controlador reintentará agresivamente la conexión de TCP.

La propiedad de conexión **MultiSubnetFailover** indica que la aplicación se implementa en un grupo de disponibilidad o una instancia de clúster de conmutación por error. El controlador intenta conectarse a la base de datos en el servidor principal [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] direcciones de la instancia intenta conectarse a todas las direcciones IP. Cuando se conecta con **MultiSubnetFailover = Yes**, el cliente lo reintenta intentos de conexión TCP más rápidamente que los intervalos de retransmisión TCP del sistema operativo de forma predeterminada. **MultiSubnetFailover=Yes** permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad o una instancia de clúster de conmutación por error de AlwaysOn. **MultiSubnetFailover = Yes** se aplica tanto único y múltiples subredes grupos de disponibilidad como instancias de clúster de conmutación por error.  

Utilice **MultiSubnetFailover=Yes** al conectarse a una instancia de clúster de conmutación por error o una escucha de grupo de disponibilidad. En caso contrario, puede verse afectado negativamente al rendimiento de su aplicación.

Cuando se conecta a un servidor en un grupo de disponibilidad o una instancia de clúster de conmutación por error, tenga en cuenta lo siguiente:
  
-   Especifique **MultiSubnetFailover = Yes** para mejorar el rendimiento cuando se conecta a una sola subred o el grupo de disponibilidad de múltiples subredes.

-   Especifique el agente de escucha del grupo de disponibilidad del grupo de disponibilidad como el servidor en la cadena de conexión.
  
-   No se puede conectar a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] una instancia configurada con más de 64 direcciones IP.

-   Ambos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticación o la autenticación Kerberos puede usarse con **MultiSubnetFailover = Yes** sin que ello afecte al comportamiento de la aplicación.

-   Puede aumentar el valor de **loginTimeout** para tener en cuenta el tiempo de conmutación por error y reducir los reintentos de conexión de la aplicación.

-   No se admiten las transacciones distribuidas.  
  
Si no está activado el enrutamiento de solo lectura, no se podrá conectar a una ubicación de réplica secundaria en un grupo de disponibilidad en las siguientes situaciones:  
  
1.  Si la ubicación de réplica secundaria no está configurada para aceptar conexiones.  
  
2.  Si una aplicación utiliza **ApplicationIntent=ReadWrite** y la ubicación de réplica secundaria está configurada para acceso de solo lectura.  
  
Una conexión producirá un error si una réplica principal está configurada para rechazar cargas de trabajo de solo lectura y la cadena de conexión contiene **ApplicationIntent=ReadOnly**.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc-syntax"></a>Sintaxis de ODBC

Dos palabras clave de cadena de conexión ODBC admiten [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
Para obtener más información sobre las palabras clave de cadena de conexión ODBC, consulte la sección [Usar palabras clave de cadena de conexión con SQL Server Native Client](http://msdn.microsoft.com/library/ms130822.aspx).  
  
Los atributos de conexión equivalentes son:
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
Para obtener más información acerca de los atributos de conexión ODBC, vea [SQLSetConnectAttr](http://msdn.microsoft.com/library/ms131709.aspx).  
  
Una aplicación ODBC que usa [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] puede usar uno de dos funciones para realizar la conexión:  
  
|Función|Description|  
|------------|---------------|  
|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect** admite tanto **ApplicationIntent** y **MultiSubnetFailover** a través de un nombre de origen de datos (DSN) o el atributo de conexión.|  
|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect** admite **ApplicationIntent** y **MultiSubnetFailover** a través del atributo de conexión, palabra clave de cadena de conexión o DSN.|
  
## <a name="see-also"></a>Vea también  

[Palabras clave de cadena de conexión y nombres de orígenes de datos (DSN)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)  
