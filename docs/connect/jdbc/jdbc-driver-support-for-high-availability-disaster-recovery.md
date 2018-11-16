---
title: Compatibilidad del controlador JDBC con la alta disponibilidad y la recuperación ante desastres | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b101070aaaef8a0e287bf02d943359d9fca8de67
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605485"
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>Compatibilidad del controlador JDBC con alta disponibilidad y recuperación ante desastres
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En este tema se describe la compatibilidad de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para la alta disponibilidad y la recuperación ante desastres: [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]. Para obtener más información sobre [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vea los Libros en pantalla de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 A partir de la versión 4.0 de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], puede especificar el agente de escucha de un grupo de disponibilidad (alta disponibilidad, recuperación ante desastres) en la propiedad de conexión. Si una aplicación [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] está conectada a una base de datos Always On que conmuta por error, se interrumpirá la conexión original y la aplicación deberá abrir una nueva para seguir trabajando tras la conmutación por error. En [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] se han agregado las siguientes [propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md):  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
Especifique multiSubnetFailover=true al conectarse a la escucha de grupo de disponibilidad de un grupo de disponibilidad o de una instancia de clúster de conmutación por error. Tenga en cuenta que **multiSubnetFailover** es false de forma predeterminada. Use **applicationIntent** para declarar el tipo de carga de trabajo de aplicación. Consulte las secciones siguientes para obtener más detalles.
 
A partir de la versión 6.0 de Microsoft JDBC Driver para SQL Server, una nueva propiedad de conexión **transparentNetworkIPResolution** (TNIR) se agrega para conexiones transparentes a grupos de disponibilidad Always On o en un servidor que tiene varias direcciones IP asociadas. Cuando **transparentNetworkIPResolution** es true, el controlador intenta conectarse a la primera dirección IP disponible. Si se produce un error en el primer intento, el controlador intenta conectarse a todas las direcciones IP en paralelo hasta que expire el tiempo de espera, descartando cualquier intento de conexión pendiente cuando uno de ellos se realiza correctamente.   

Tenga en cuenta:
* transparentNetworkIPResolution es true de forma predeterminada
* transparentNetworkIPResolution se omite si multiSubnetFailover es true
* transparentNetworkIPResolution se omite si se usa la creación de reflejo de base de datos
* transparentNetworkIPResolution se omite si hay más de 64 direcciones IP
* Cuando transparentNetworkIPResolution es true, el primer intento de conexión utiliza un valor de tiempo de espera de 500 ms. Resto de los intentos de conexión siguen la misma lógica como se muestra en la característica de multiSubnetFailover. 

> [!NOTE]  
Si está utilizando Microsoft JDBC Driver 4.2 (o reducir) para SQL Server y si **multiSubnetFailover** es false, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] intenta conectarse a la primera dirección IP. Si el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no puede establecer una conexión con la primera dirección IP, se producirá un error en la conexión. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] no intentará conectarse a ninguna dirección IP más asociada al servidor. 

  
> [!NOTE]  
>  El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de que una aplicación se conecte a un grupo de disponibilidad. Además, dado que una conexión puede producir un error debido a la conmutación por error de un grupo de disponibilidad, es aconsejable implementar la lógica de reintento de conexión y hacer que una conexión que no se ha podido establecer se reintente hasta que vuelva a conectarse.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover  
 Especifique siempre **multiSubnetFailover=true** al conectarse a la escucha de grupo de disponibilidad de un grupo de disponibilidad de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o a una instancia de clúster de conmutación por error de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. **multiSubnetFailover** habilita una conmutación por error más rápida en todos los grupos de disponibilidad y las instancias del clúster de conmutación por error en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], y reducirá significativamente el tiempo de conmutación por error en las topologías únicas y AlwaysOn de varias subredes. En un clúster de conmutación por error de varias subredes, el cliente intentará conexiones en paralelo. Durante una conmutación por error de subred, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] reintentará agresivamente la conexión TCP.  
  
 La propiedad de conexión **multiSubnetFailover** indica que la aplicación se está implementando en un grupo de disponibilidad o una instancia de clúster de conmutación por error y que [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] intentará conectarse a la base de datos en la instancia principal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un intento de conexión a todas las direcciones IP. Si **MultiSubnetFailover=true** se especifica para una conexión, el cliente reintentará la conexión TCP más deprisa que los intervalos de retransmisión TCP predeterminados del sistema operativo. Esto permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad AlwaysOn o una instancia de clúster de conmutación por error AlwaysOn, y es aplicable a instancias de clúster de conmutación por error y grupos de disponibilidad de una y varias subredes.  
  
 Para obtener más información sobre las palabras clave de cadena de conexión en el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Si se especifica **multiSubnetFailover=true** al conectarse a algo que no sea una escucha de grupo de disponibilidad o una instancia de clúster de conmutación por error, el rendimiento puede verse afectado negativamente, de modo que no se permite.  
  
 Si el administrador de seguridad no está instalado, la máquina virtual Java almacenará en memoria caché las direcciones IP virtuales (VIP) durante un período finito de tiempo, definido de manera predeterminada por la implementación de JDK y por las propiedades networkaddress.cache.ttl y networkaddress.cache.negative.ttl de Java. Si el administrador de seguridad de JDK está instalado, la máquina virtual Java almacenará en memoria caché las VIP y no actualizará la caché de forma predeterminada. Debe establecer el valor de "período de vida" (networkaddress.cache.ttl) en un día para la memoria caché de la máquina virtual Java. Si no cambia el valor predeterminado a un día (aproximadamente), el valor anterior no se purgará de la memoria caché de la máquina virtual Java cuando se agregue o se actualice una VIP. Para obtener más información sobre networkaddress.cache.ttl y networkaddress.cache.negative.ttl, vea [ https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html ](https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html).  
  
 Utilice las siguientes instrucciones para conectarse a un servidor en un grupo de disponibilidad o una instancia de clúster de conmutación por error:  
  
-   El controlador generará un error si el **nombreDeInstancia** propiedad de conexión se usa en la misma cadena de conexión que el **multiSubnetFailover** propiedad de conexión. Esto refleja el hecho de que SQL Browser no se usa en un grupo de disponibilidad. Sin embargo, si la **portNumber** también se especifica la propiedad de conexión, el controlador omitirá **nombreDeInstancia** y usar **portNumber**.  
  
-   Use la propiedad de conexión **multiSubnetFailover** cuando se conecte a una única subred o a varias subredes, ya que mejorará el rendimiento en ambos casos.  
  
-   Para conectarse a un grupo de disponibilidad, especifique el agente de escucha del grupo de disponibilidad como el servidor en la cadena de conexión. Por ejemplo, jdbc:sqlserver://VNN1.  
  
-   La conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada con más de 64 direcciones IP producirá un error en la conexión.  
  
-   El comportamiento de una aplicación que usa la propiedad de conexión **multiSubnetFailover** no se ve afectado por el tipo de autenticación: autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], autenticación Kerberos o autenticación de Windows.  
  
-   Aumente el valor de **loginTimeout** para tener en cuenta el tiempo de conmutación por error y reducir los reintentos de conexión de la aplicación.  
  
-   No se admiten las transacciones distribuidas.  
  
 Si no está activado el enrutamiento de solo lectura, no se podrá conectar a una ubicación de réplica secundaria en un grupo de disponibilidad en las siguientes situaciones:  
  
1.  Si la ubicación de réplica secundaria no está configurada para aceptar conexiones.  
  
2.  Si una aplicación usa **applicationIntent=ReadWrite** (se describe a continuación) y la ubicación de réplica secundaria está configurada para acceso de solo lectura.  
  
 Una conexión producirá un error si una réplica principal está configurada para rechazar cargas de trabajo de solo lectura y la cadena de conexión contiene **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Actualizar para utilizar clústeres de varias subredes a partir de la creación de reflejo de la base de datos  
 Si actualiza una aplicación [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] que actualmente usa la creación de reflejo de la base de datos en un escenario de varias subredes, debe quitar la propiedad de conexión **failoverPartner** y reemplazarla por **multiSubnetFailover** establecida en **true**, así como reemplazar el nombre del servidor en la cadena de conexión por una escucha de grupo de disponibilidad. Si una cadena de conexión usa **failoverPartner** y **multiSubnetFailover=true**, el controlador generará un error. En cambio, si una cadena de conexión usa **failoverPartner** y **multiSubnetFailover=false** (o **ApplicationIntent=ReadWrite**), la aplicación usará la creación de reflejo de la base de datos.  
  
 Si la creación de reflejo de la base de datos se usa en la base de datos principal del grupo de disponibilidad y **multiSubnetFailover=true** se usa en la cadena de conexión que se conecta a una base de datos principal, en lugar de a una escucha de grupo de disponibilidad, el controlador devolverá un error.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


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
 Un grupo de disponibilidad consta de varios servidores físicos. [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] agregó compatibilidad con **nombres alternativos de sujeto** en los certificados SSL, por lo que es posible asociar varios hosts al mismo certificado. Para obtener más información sobre SSL, consulte [descripción de la compatibilidad SSL](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="see-also"></a>Ver también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
