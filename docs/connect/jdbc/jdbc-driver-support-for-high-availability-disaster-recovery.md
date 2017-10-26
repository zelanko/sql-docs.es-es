---
title: "Compatibilidad del controlador JDBC con alta disponibilidad y recuperación ante desastres | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27b51025180a1c9a2463c49401589ab459e7ecaf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>Compatibilidad del controlador JDBC con alta disponibilidad y recuperación ante desastres
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Este tema se describen [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite alta disponibilidad y recuperación ante desastres-- [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]. Para obtener más información acerca de [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vea los Libros en pantalla de [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] .  
  
 A partir de la versión 4.0 de la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], puede especificar el agente de escucha del grupo de disponibilidad de una (alta disponibilidad y recuperación ante desastres) grupo de disponibilidad (AG) en la propiedad de conexión. Si un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicación está conectada a una base de datos de AlwaysOn que conmuta por error, se pierde la conexión original y la aplicación debe abrir una conexión nueva para seguir trabajando después de la conmutación por error. El siguiente [propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) se agregaron en [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]:  
  
-   **multiSubnetFailover**  
  
-   **intención de aplicaciones**
 
Especifique multiSubnetFailover = true cuando se conecta a la escucha del grupo de disponibilidad de un grupo de disponibilidad o una instancia de clúster de conmutación por error. Tenga en cuenta que **multiSubnetFailover** es false de forma predeterminada. Use **applicationIntent** para declarar el tipo de carga de trabajo de la aplicación. Vea las secciones a continuación para obtener más detalles.
 
A partir de la versión 6.0 de Microsoft JDBC Driver para SQL Server, una nueva propiedad de conexión **transparentNetworkIPResolution** (TNIR) se agrega para conexiones transparentes a grupos de disponibilidad AlwaysOn o a un servidor que tiene varias direcciones IP asociadas. Cuando **transparentNetworkIPResolution** es true, el controlador intenta conectarse a la primera dirección IP disponible. Si se produce un error en el primer intento, el controlador intenta conectarse a todas las direcciones IP en paralelo hasta que expire el tiempo de espera, descartando todos los intentos de conexión pendiente cuando uno de ellos se realiza correctamente.   

Tenga en cuenta que:
* transparentNetworkIPResolution es true de forma predeterminada
* transparentNetworkIPResolution se omite si multiSubnetFailover es true
* transparentNetworkIPResolution se omite si se utiliza la creación de reflejo de base de datos
* transparentNetworkIPResolution se omite si no hay más de 64 direcciones IP
* Cuando transparentNetworkIPResolution es true, el primer intento de conexión utiliza un valor de tiempo de espera de 500 ms. Resto de los intentos de conexión siguen la misma lógica como en la característica de multiSubnetFailover. 

> [!NOTE]  
Si utiliza Microsoft JDBC Driver 4.2 (o inferior) para SQL Server y **multiSubnetFailover** es false, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] intenta conectarse a la primera dirección IP. Si el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no se puede establecer una conexión con la primera dirección IP, la conexión produce un error. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no intentará conectarse a ninguna dirección IP más asociada con el servidor. 

  
> [!NOTE]  
>  El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de que una aplicación se conecte a un grupo de disponibilidad. Además, dado que una conexión puede producir un error debido a la conmutación por error de un grupo de disponibilidad, es aconsejable implementar la lógica de reintento de conexión y hacer que una conexión que no se ha podido establecer se reintente hasta que vuelva a conectarse.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover  
 Especifique siempre **multiSubnetFailover = true** al conectarse a la escucha del grupo de disponibilidad de un [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] grupo de disponibilidad o una [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] instancia de clúster de conmutación por error. **multiSubnetFailover** permite más rápida conmutación por error para todos los grupos de disponibilidad y las instancias de clúster de conmutación por error en [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] y reducirá significativamente el tiempo de conmutación por error para las topologías de AlwaysOn y de varias subredes. En un clúster de conmutación por error de varias subredes, el cliente intentará conexiones en paralelo. Durante una conmutación por error de subred, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] seguirá Reintentando la conexión TCP.  
  
 El **multiSubnetFailover** propiedad de conexión indica que la aplicación se implementa en un grupo de disponibilidad o instancia de clúster de conmutación por error y que la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] intentará conectarse a la base de datos en el servidor principal [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] direcciones de la instancia intenta conectarse a todas las direcciones IP. Cuando **MultiSubnetFailover = true** se especifica para una conexión, el cliente lo reintenta intentos de conexión TCP más rápidamente que los intervalos de retransmisión TCP del sistema operativo de forma predeterminada. Esto permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad AlwaysOn o una instancia de clúster de conmutación por error AlwaysOn, y es aplicable a instancias de clúster de conmutación por error y grupos de disponibilidad de una y varias subredes.  
  
 Para obtener más información sobre las palabras clave de cadena de conexión en el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Especificar **multiSubnetFailover = true** al conectarse a algo distinto de un agente de escucha del grupo de disponibilidad o una instancia de clúster de conmutación por error puede producir un impacto negativo en el rendimiento y no se admite.  
  
 Si el administrador de seguridad no está instalado, la máquina virtual Java almacenará en memoria caché las direcciones IP virtuales (VIP) durante un período finito de tiempo, definido de manera predeterminada por la implementación de JDK y por las propiedades networkaddress.cache.ttl y networkaddress.cache.negative.ttl de Java. Si el administrador de seguridad de JDK está instalado, la máquina virtual Java almacenará en memoria caché las VIP y no actualizará la caché de forma predeterminada. Debe establecer el valor de "período de vida" (networkaddress.cache.ttl) en un día para la memoria caché de la máquina virtual Java. Si no cambia el valor predeterminado a un día (aproximadamente), el valor anterior no se purgará de la memoria caché de la máquina virtual Java cuando se agregue o se actualice una VIP. Para obtener más información sobre networkaddress.cache.ttl y networkaddress.cache.negative.ttl, vea [http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html](http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html).  
  
 Utilice las siguientes instrucciones para conectarse a un servidor en un grupo de disponibilidad o una instancia de clúster de conmutación por error:  
  
-   El controlador generará un error si la **nombreDeInstancia** propiedad de conexión se usa en la misma cadena de conexión que el **multiSubnetFailover** propiedad de conexión. Esto refleja el hecho de que SQL Browser no se usa en un grupo de disponibilidad. Sin embargo, si la **portNumber** también se especifica la propiedad de conexión, el controlador omitirá **nombreDeInstancia** y usar **portNumber**.  
  
-   Use la **multiSubnetFailover** propiedad de conexión al conectarse a una sola subred o a varias subredes, mejorará el rendimiento de ambos.  
  
-   Para conectarse a un grupo de disponibilidad, especifique el agente de escucha del grupo de disponibilidad como el servidor en la cadena de conexión. Por ejemplo, jdbc:sqlserver://VNN1.  
  
-   La conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] configurada con más de 64 direcciones IP producirá un error en la conexión.  
  
-   Comportamiento de una aplicación que usa el **multiSubnetFailover** propiedad de conexión no se ve afectada por el tipo de autenticación: [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticación, la autenticación Kerberos o autenticación de Windows.  
  
-   Aumente el valor de **loginTimeout** para dar tiempo de conmutación por error y reducir los reintentos de conexión de aplicación.  
  
-   No se admiten las transacciones distribuidas.  
  
 Si no está activado el enrutamiento de solo lectura, no se podrá conectar a una ubicación de réplica secundaria en un grupo de disponibilidad en las siguientes situaciones:  
  
1.  Si la ubicación de réplica secundaria no está configurada para aceptar conexiones.  
  
2.  Si una aplicación usa **applicationIntent = ReadWrite** (descrito a continuación) y la ubicación de réplica secundaria está configurada para acceso de solo lectura.  
  
 Una conexión producirá un error si una réplica principal está configurada para rechazar cargas de trabajo de solo lectura y la cadena de conexión contiene **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Actualizar para utilizar clústeres de varias subredes a partir de la creación de reflejo de la base de datos  
 Si actualiza un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicación que emplea actualmente creación de reflejo de base de datos a un escenario de múltiples subredes, debe quitar la **failoverPartner** propiedad de conexión y reemplazarla con **multiSubnetFailover ** establecido en **true** y reemplace el nombre del servidor en la cadena de conexión con un agente de escucha del grupo de disponibilidad. Si usa una cadena de conexión **failoverPartner** y **multiSubnetFailover = true**, el controlador generará un error. Sin embargo, si usa una cadena de conexión **failoverPartner** y **multiSubnetFailover = false** (o **ApplicationIntent = ReadWrite**), la aplicación utilizará la base de datos creación de reflejo.  
  
 El controlador devolverá un error si la creación de reflejo de base de datos se utiliza en la base de datos principal en el AG y si **multiSubnetFailover = true** se utiliza en la cadena de conexión que se conecta a una base de datos principal en lugar de un grupo de disponibilidad agente de escucha.  
  
## <a name="specifying-application-intent"></a>Especificar el intento de la aplicación  
 Cuando **applicationIntent = ReadOnly**, el cliente solicita una carga de trabajo de solo lectura al conectarse a una base de datos de AlwaysOn habilitado. El servidor exigirá la intención en el momento de la conexión y durante una instrucción USE DATABASE, pero solo para una base de datos habilitada para AlwaysOn.  
  
 El **applicationIntent** palabra clave no funciona con bases de datos heredados, de solo lectura.  
  
 Una base de datos puede permitir o denegar la lectura de las cargas de trabajo en la base de datos de destino AlwaysOn. (Use la cláusula **ALLOW_CONNECTIONS** de las instrucciones **PRIMARY_ROLE** y **SECONDARY_ROLE**[!INCLUDE[tsql](../../includes/tsql_md.md)]).  
  
 El **applicationIntent** palabra clave se utiliza para habilitar el enrutamiento de solo lectura.  
  
## <a name="read-only-routing"></a>Enrutamiento de solo lectura  
 El enrutamiento de solo lectura es una característica que puede asegurar la disponibilidad de una réplica de solo lectura de una base de datos. Para habilitar el enrutamiento de solo lectura:  
  
1.  Debe conectarse a un agente de escucha de grupo de disponibilidad AlwaysOn.  
  
2.  El **applicationIntent** palabra clave de cadena de conexión debe establecerse en **ReadOnly**.  
  
3.  El administrador de bases de datos debe configurar el grupo de disponibilidad para habilitar el enrutamiento de solo lectura.  
  
 Es posible que varias conexiones con enrutamiento de solo lectura no se conecten todas a la misma réplica de solo lectura. Los cambios en la sincronización de la base de datos o los cambios en la configuración de enrutamiento del servidor pueden producir conexiones de cliente para réplicas de solo lectura diferentes. Para asegurarse de que todas las solicitudes de solo lectura se conectan a la misma réplica de solo lectura, no pase un agente de escucha del grupo de disponibilidad o la dirección IP virtual a la **serverName** palabra clave de cadena de conexión. En su lugar, especifique el nombre de la instancia de solo lectura.  
  
 El enrutamiento de solo lectura puede tardar más tiempo que la conexión a la réplica principal, ya que primero se conecta a la réplica principal y después busca la mejor réplica secundaria legible disponible. Por ello, debe aumentar el tiempo de espera de inicio de sesión.  
  
## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>Nuevos métodos que admiten multiSubnetFailover y applicationIntent  
 Los métodos siguientes ofrecen acceso mediante programación a la **multiSubnetFailover**, **applicationIntent** y **transparentNetworkIPResolution** cadena de conexión palabras clave:  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 El **getMultiSubnetFailover**, **setMultiSubnetFailover**, **getApplicationIntent**, **setApplicationIntent**, **getTransparentNetworkIPResolution** y **setTransparentNetworkIPResolution** métodos también se agregan a [clase SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [ Clase SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), y [clase SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
## <a name="ssl-certificate-validation"></a>Validación de certificados SSL  
 Un grupo de disponibilidad consta de varios servidores físicos. [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]Agrega compatibilidad con **nombre alternativo del sujeto** en los certificados SSL para varios hosts pueden asociarse con el mismo certificado. Para obtener más información sobre SSL, consulte [descripción de la compatibilidad SSL](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md)  
  
  

