---
title: 'Controlador ODBC en Linux y macOS: alta disponibilidad y recuperación ante desastres | Microsoft Docs'
ms.custom: ''
ms.date: 04/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f53fc932ced3c5a4e002c9938a9af6a2b8d410e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798779"
---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>Compatibilidad del controlador ODBC en Linux y macOS para alta disponibilidad y recuperación ante desastres
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Compatibilidad de los controladores ODBC con Linux y macOS [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obtener más información acerca de [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], consulte:  
  
-   [Agentes de escucha del grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación (SQL Server)](https://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [Creación y configuración de grupos de disponibilidad (SQL Server)](https://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [Clúster de conmutación por error y grupos de disponibilidad de AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [Secundarias activas: réplicas secundarias legibles (grupos de disponibilidad AlwaysOn)](https://msdn.microsoft.com/library/ff878253.aspx)  
  
Puede especificar el agente de escucha del grupo de disponibilidad de un determinado grupo de disponibilidad en la cadena de conexión. Si una aplicación de ODBC en Linux o macOS se conecta a una base de datos de un grupo de disponibilidad que conmuta por error, la conexión original se interrumpe y la aplicación debe abrir una nueva conexión para continuar el trabajo después de la conmutación por error.

Los controladores ODBC en Linux y macOS iteran secuencialmente a través de todas las direcciones IP asociadas a un nombre de host de DNS si usted no se conecta a una escucha de grupo de disponibilidad y varias direcciones IP están asociadas con el nombre de host.

Si la primera dirección IP del servidor DNS que se devuelve no se puede conectar, estas iteraciones pueden llevar mucho tiempo. Al conectarse a una escucha de grupo de disponibilidad, el controlador trata de establecer conexiones con todas las direcciones IP en paralelo. Si un intento de conexión se realiza correctamente, el controlador descarta todos los intentos de conexión pendiente.

> [!NOTE]  
> Dado que se puede producir un error de conexión debido a la conmutación por error de un grupo de disponibilidad, se recomienda implementar la lógica de reintento de conexión y volver a intentar realizar una conexión que no se ha podido establecer hasta que vuelva a conectarse. El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de establecer una conexión con un grupo de disponibilidad.

## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover

Especifique siempre **MultiSubnetFailover=Yes** al conectarse a una escucha de grupo de disponibilidad de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] o a una instancia de clúster de conmutación por error de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. **MultiSubnetFailover** permite una conmutación por error más rápida en todos los grupos de disponibilidad y una instancia de clúster de conmutación por error de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. **MultiSubnetFailover** también reduce considerablemente el tiempo de conmutación por error en las topologías AlwaysOn de una y varias subredes. Durante una conmutación por error de varias subredes, el cliente intentará establecer conexiones en paralelo. Durante una conmutación por error de una subred, el controlador volverá a tratar de establecer la conexión TCP de manera drástica.

La propiedad de conexión **MultiSubnetFailover** indica que la aplicación se implementa en un grupo de disponibilidad o una instancia de clúster de conmutación por error. El controlador trata de conectarse a la base de datos de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] principal tratando de conectarse a todas las direcciones IP. Al conectarse con **MultiSubnetFailover=Yes**, el cliente reintenta la conexión TCP con más rapidez que los intervalos de retransmisión TCP predeterminados del sistema operativo. **MultiSubnetFailover=Yes** permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad o una instancia de clúster de conmutación por error de AlwaysOn. **MultiSubnetFailover=Yes** se aplica a instancias de clúster de conmutación por error y grupos de disponibilidad de una y varias subredes.  

Utilice **MultiSubnetFailover=Yes** al conectarse a una instancia de clúster de conmutación por error o una escucha de grupo de disponibilidad. De lo contrario, el rendimiento de la aplicación puede verse afectada adversamente.

Tenga en cuenta lo siguiente al conectarse a un servidor en un grupo de disponibilidad o una instancia de clúster de conmutación por error:
  
-   Especifique **MultiSubnetFailover=Yes** para mejorar el rendimiento cuando se conecte a un grupo de disponibilidad de una sola subred o varias subredes.

-   Especifique el agente de escucha del grupo de disponibilidad como el servidor en la cadena de conexión.
  
-   No se puede conectar a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurada con más de 64 direcciones IP.

-   Tanto la autenticación [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como la autenticación Kerberos se pueden usar con **MultiSubnetFailover=Yes** sin que el comportamiento de la aplicación se vea afectado.

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
  
Para más información sobre las palabras clave de cadena de conexión ODBC, vea la sección [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
Los atributos de conexión equivalentes son estos:
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
Para más información sobre los atributos de conexión de ODBC, vea [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
Una aplicación de ODBC que usa [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] puede utilizar una de las dos funciones para realizar la conexión:  
  
|Función|Descripción|  
|------------|---------------|  
|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect** admite **ApplicationIntent** y **MultiSubnetFailover** mediante un nombre de origen de datos (DSN) o un atributo de conexión.|  
|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect** admite **ApplicationIntent** y **MultiSubnetFailover** por medio de DNS, de una palabra clave de cadena de conexión o de un atributo de conexión.|
  
## <a name="see-also"></a>Consulte también  

[Palabras clave de cadena de conexión y nombres de orígenes de datos (DSN)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
