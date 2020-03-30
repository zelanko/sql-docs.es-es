---
title: Compatibilidad de SqlClient para la alta disponibilidad con recuperación de desastres
description: Describe la compatibilidad de SqlClient con grupos de disponibilidad de alta disponibilidad y recuperación ante desastres (Always On).
ms.date: 08/15/2019
ms.assetid: 61e0b396-09d7-4e13-9711-7dcbcbd103a0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: a7aa6a28a64e35c13c135e509b758a1636b3f896
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896287"
---
# <a name="sqlclient-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SqlClient para la alta disponibilidad con recuperación de desastres

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

En este tema se describe la compatibilidad del proveedor de datos SqlClient de Microsoft para SQL Server con los grupos de disponibilidad AlwaysOn de alta disponibilidad y recuperación ante desastres.  La característica Grupos de disponibilidad AlwaysOn se ha incorporado a SQL Server 2012. Para obtener más información sobre los grupos de disponibilidad AlwaysOn, vea los Libros en pantalla de SQL Server.  
  
Ahora puede especificar la escucha de grupo de disponibilidad de un grupo de disponibilidad (AG) (alta disponibilidad, recuperación ante desastres) o la instancia de clúster de conmutación por error de SQL Server 2012 en la propiedad de conexión. Si una aplicación SqlClient está conectada a una base de datos AlwaysOn que conmuta por error, se interrumpe la conexión original y la aplicación debe abrir una nueva para seguir trabajando tras la conmutación por error.  
  
Si no se está conectando a una escucha de grupo de disponibilidad o una instancia de clúster de conmutación por error de SQL Server 2012 y si hay varias direcciones IP asociadas a un nombre de host, SqlClient itera secuencialmente por todas las direcciones IP asociadas a la entrada de DNS. Esto puede llevar mucho tiempo si la primera dirección IP que devuelve el servidor DNS no está enlazada a una tarjeta (NIC) de interfaz de red. Al conectarse a una escucha de grupo de disponibilidad o a una instancia de clúster de conmutación por error de SQL Server 2012, SqlClient intenta establecer conexiones con todas las direcciones IP en paralelo y, si un intento de conexión se realiza correctamente, el controlador descarta cualquier intento de conexión pendiente.  
  
> [!NOTE]
>  El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de que una aplicación se conecte a un grupo de disponibilidad. Además, dado que una conexión puede producir un error debido a una conmutación por error, debe implementar lógica de reintento de conexión para que una conexión que no se ha podido establecer se reintente hasta que lo haga.  
  
Las siguientes propiedades de conexión se admiten en el proveedor de datos SqlClient de Microsoft para SQL Server:  
  
- `ApplicationIntent`  
  
- `MultiSubnetFailover`  
  
Puede modificar mediante programación estas palabras clave de cadena de conexión con:  
  
- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.ApplicationIntent%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A>  
  
## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover  
Especifique siempre `MultiSubnetFailover=True` al conectarse a un agente de escucha de grupo de disponibilidad de SQL Server 2012 o a una instancia de clúster de conmutación por error de SQL Server 2012. `MultiSubnetFailover` habilita una conmutación por error más rápida para todos los grupos de disponibilidad y la instancia del clúster de conmutación por error de SQL Server 2012 y reduce significativamente el tiempo de la conmutación por error en las topologías únicas y AlwaysOn de varias subredes. En un clúster de conmutación por error de varias subredes, el cliente intentará conexiones en paralelo. Durante una conmutación por error de subred, se sigue volviendo a intentar enérgicamente la conexión TCP.  
  
La propiedad de conexión `MultiSubnetFailover` indica que la aplicación se va a implementar en un grupo de disponibilidad o en una instancia de clúster de conmutación por error de SQL Server 2012 y que SqlClient intenta conectarse a la base de datos en la instancia primaria de SQL Server al intentar conectarse a todas las direcciones IP. Cuando se especifica `MultiSubnetFailover=True` para una conexión, el cliente reintenta la conexión TCP más deprisa que los intervalos de retransmisión TCP predeterminados del sistema operativo. Esto permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad AlwaysOn o una instancia de clúster de conmutación por error AlwaysOn, y es aplicable a instancias de clúster de conmutación por error y grupos de disponibilidad de una y varias subredes.  
  
Para obtener más información sobre las palabras clave de cadena de conexión de SqlClient, vea <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
La especificación de `MultiSubnetFailover=True` al conectarse con algo distinto a una escucha de grupo de disponibilidad o una instancia de clúster de conmutación por error de SQL Server 2012 puede tener un impacto negativo en el rendimiento y no se admite.  
  
Use las siguientes instrucciones para conectarse a un servidor de un grupo de disponibilidad o una instancia de clúster de conmutación por error de SQL Server 2012:  
  
- Utilice la propiedad de conexión `MultiSubnetFailover` al conectarse a una sola subred o a varias subredes. Así mejorará el rendimiento en ambas situaciones.  
  
- Para conectarse a un grupo de disponibilidad, especifique el agente de escucha del grupo de disponibilidad como el servidor en la cadena de conexión.  
  
- La conexión a una instancia de SQL Server configurada con más de 64 direcciones IP produce un error en la conexión.  
  
- El comportamiento de una aplicación que usa la propiedad de conexión `MultiSubnetFailover` no se ve afectado por el tipo de autenticación: de SQL Server, Kerberos o Windows.  
  
- Incremente el valor de `Connect Timeout` para dar tiempo a la conmutación por error y reducir los reintentos de conexión de la aplicación.  
  
- No se admiten las transacciones distribuidas.  
  
 Si no está activado el enrutamiento de solo lectura, no se puede conectar a una ubicación de réplica secundaria en las siguientes situaciones:  
  
- Si la ubicación de réplica secundaria no está configurada para aceptar conexiones.  
  
- Si una aplicación utiliza `ApplicationIntent=ReadWrite` (se explica a continuación) y la ubicación de réplica secundaria está configurada para el acceso de solo lectura.  
  
<xref:Microsoft.Data.SqlClient.SqlDependency> no se admite en las réplicas secundarias de solo lectura.  
  
Una conexión producirá un error si una réplica principal está configurada para rechazar las cargas de trabajo de solo lectura y la cadena de conexión contiene `ApplicationIntent=ReadOnly`.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Actualización para usar clústeres de varias subredes a partir de la creación de reflejo de la base de datos  
Se producirá un error de conexión (<xref:System.ArgumentException>) si las palabras clave de conexión `MultiSubnetFailover` y `Failover Partner` están presentes en la cadena de conexión, o si se usa `MultiSubnetFailover=True` y un protocolo distinto de TCP. También se produce un error (<xref:Microsoft.Data.SqlClient.SqlException>) si se usa `MultiSubnetFailover` y SQL Server devuelve una respuesta del asociado de conmutación por error que indica que forma parte de un par de creación de reflejo de la base de datos.  
  
Si actualiza una aplicación SqlClient que usa actualmente la creación de reflejo de la base de datos para un escenario de varias subredes, debe quitar la propiedad de conexión `Failover Partner` y reemplazarla por `MultiSubnetFailover` establecida en `True` y reemplazar el nombre de servidor en la cadena de conexión por una escucha de grupo de disponibilidad. Si una cadena de conexión utiliza `Failover Partner` y `MultiSubnetFailover=True`, el controlador generará un error. Sin embargo, si una cadena de conexión utiliza `Failover Partner` y `MultiSubnetFailover=False` (o `ApplicationIntent=ReadWrite`), la aplicación utilizará la creación de reflejo de la base de datos.  
  
El controlador devuelve un error si la creación de reflejo de la base de datos se usa en la base de datos principal del grupo de disponibilidad y si se usa `MultiSubnetFailover=True` en la cadena de conexión que conecta a una base de datos principal en lugar de a una escucha de grupo de disponibilidad.  
  
## <a name="specifying-application-intent"></a>Especificación de intención de aplicaciones  
Cuando `ApplicationIntent=ReadOnly`, el cliente solicita una carga de trabajo de lectura al conectarse a una base de datos habilitada para AlwaysOn. El servidor aplicará el intento en el momento de la conexión y durante una instrucción de base de datos USE pero solo en una base de datos con habilitada para AlwaysOn.  
  
La palabra clave `ApplicationIntent` no funciona con bases de datos de solo lectura heredadas.  
  
Una base de datos puede permitir o denegar la lectura de las cargas de trabajo en la base de datos de destino AlwaysOn. (Esto se hace con la cláusula `ALLOW_CONNECTIONS` de las instrucciones Transact-SQL de `PRIMARY_ROLE` y `SECONDARY_ROLE`).  
  
La palabra clave `ApplicationIntent` se utiliza para habilitar el enrutamiento de solo lectura.  
  
## <a name="read-only-routing"></a>Enrutamiento de solo lectura  
El enrutamiento de solo lectura es una característica que puede garantizar la disponibilidad de una réplica de solo lectura de una base de datos. Para habilitar el enrutamiento de solo lectura:  
  
- Debe conectarse siempre a un agente de escucha de grupo de disponibilidad Always On.  
  
- La palabra clave de la cadena de conexión `ApplicationIntent` debe establecerse en `ReadOnly`.  
  
- El administrador de bases de datos debe configurar el grupo de disponibilidad para habilitar el enrutamiento de solo lectura.  
  
Es posible que varias conexiones con enrutamiento de solo lectura no se conecten todas a la misma réplica de solo lectura. Los cambios en la sincronización de la base de datos o los cambios en la configuración de enrutamiento del servidor pueden producir conexiones de cliente para réplicas de solo lectura diferentes. Para asegurarse de que todas las solicitudes de solo lectura se conectan a la misma réplica de solo lectura, no pase un agente de escucha de grupo de disponibilidad a la palabra clave de cadena de conexión `Data Source`. En su lugar, especifique el nombre de la instancia de solo lectura.  
  
El enrutamiento de solo lectura puede tardar más en conectarse al servidor principal porque el enrutamiento de solo lectura se conecta primero al servidor principal y luego busca el mejor secundario legible disponible. Por ello, debe aumentar el tiempo de espera de inicio de sesión.  
  
## <a name="next-steps"></a>Pasos siguientes
- [Características de SQL Server y ADO.NET](sql-server-features-adonet.md)
