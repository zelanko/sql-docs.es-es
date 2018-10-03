---
title: Compatibilidad con alta disponibilidad, recuperación ante desastres para los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f81353dcf7dc3af6b8cdcccba287b425d2139af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838243"
---
# <a name="support-for-high-availability-disaster-recovery"></a>Compatibilidad con recuperación ante desastres de alta disponibilidad
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se describe la compatibilidad de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], agregada en la versión 3.0, con alta disponibilidad y recuperación ante desastres: [!INCLUDE[ssHADR](../../includes/sshadr_md.md)].  Se agregó compatibilidad para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Para obtener más información acerca de [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
En la versión 3.0 de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] puede especificar el agente de escucha de un grupo de disponibilidad (alta disponibilidad, recuperación ante desastres) en la propiedad de conexión. Si una aplicación [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] está conectada a una base de datos Always On que conmuta por error, se interrumpirá la conexión original y la aplicación deberá abrir una nueva para seguir trabajando tras la conmutación por error.  
  
Si no va a conectarse a un agente de escucha de grupo de disponibilidad y varias direcciones IP están asociadas a un nombre de host, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] iterará secuencialmente a través de todas las direcciones IP asociadas a la entrada DNS. Esto puede llevar mucho tiempo si la primera dirección IP que devuelve el servidor DNS no está enlazada a una tarjeta (NIC) de interfaz de red. Al conectarse a un agente de escucha de grupo de disponibilidad, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] intentará establecer conexiones con todas las direcciones IP en paralelo y, si un intento de conexión se realiza correctamente, el controlador descartará los intentos pendientes.  
  
> [!NOTE]  
> El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de que una aplicación se conecte a un grupo de disponibilidad. Además, dado que una conexión puede producir un error debido a la conmutación por error de un grupo de disponibilidad, es aconsejable implementar la lógica de reintento de conexión y hacer que una conexión que no se ha podido establecer se reintente hasta que vuelva a conectarse.  
  
## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover  
La propiedad de conexión **MultiSubnetFailover** indica que la aplicación se está implementando en un grupo de disponibilidad o una instancia de clúster de conmutación por error y que [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] intentará conectarse a la base de datos en la instancia principal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un intento de conexión a todas las direcciones IP. Si **MultiSubnetFailover=true** se especifica para una conexión, el cliente reintentará la conexión TCP más deprisa que los intervalos de retransmisión TCP predeterminados del sistema operativo. Esto permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad AlwaysOn o una instancia de clúster de conmutación por error AlwaysOn, y es aplicable a instancias de clúster de conmutación por error y grupos de disponibilidad de una y varias subredes.  
  
Al conectarse a un agente de escucha de grupo de disponibilidad de SQL Server 2012 o una instancia de clúster de conmutación por error de SQL Server 2012, especifique siempre **MultiSubnetFailover=True**. **MultiSubnetFailover** habilita una conmutación por error más rápida para todos los grupos de disponibilidad y la instancia del clúster de conmutación por error en SQL Server 2012 y reduce significativamente el tiempo de la conmutación por error en las topologías Always On únicas y de varias subredes. En un clúster de conmutación por error de varias subredes, el cliente intentará conexiones en paralelo. Durante una conmutación por error de subred, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] reintentará agresivamente la conexión TCP.  
  
Para obtener más información sobre las palabras clave de cadena de conexión en [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], consulte [opciones de conexión](../../connect/php/connection-options.md).  
  
Si se especifica **MultiSubnetFailover=true** al conectarse a algo que no sea un agente de escucha de grupo de disponibilidad o una instancia de clúster de conmutación por error, el rendimiento puede verse afectado negativamente, de modo que no se permite.  
  
Utilice las siguientes instrucciones para conectarse a un servidor de un grupo de disponibilidad :  
  
-   Use la propiedad de conexión **MultiSubnetFailover** cuando se conecte a una única subred o a varias subredes, ya que mejorará el rendimiento en ambos casos.  
  
-   Para conectarse a un grupo de disponibilidad, especifique el agente de escucha del grupo de disponibilidad como el servidor en la cadena de conexión.  
  
-   La conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada con más de 64 direcciones IP producirá un error en la conexión.  
  
-   El comportamiento de una aplicación que usa la propiedad de conexión **MultiSubnetFailover** no se ve afectado por el tipo de autenticación: autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], autenticación Kerberos o autenticación de Windows.  
  
-   Aumente el valor de **loginTimeout** para tener en cuenta el tiempo de conmutación por error y reducir los reintentos de conexión de la aplicación.  
  
-   No se admiten las transacciones distribuidas.  
  
Si no está activado el enrutamiento de solo lectura, no se podrá conectar a una ubicación de réplica secundaria en un grupo de disponibilidad en las siguientes situaciones:  
  
- Si la ubicación de réplica secundaria no está configurada para aceptar conexiones.  
  
- Si una aplicación usa **ApplicationIntent=ReadWrite** (se describe a continuación) y la ubicación de réplica secundaria está configurada para acceso de solo lectura.  
  
Una conexión producirá un error si una réplica principal está configurada para rechazar cargas de trabajo de solo lectura y la cadena de conexión contiene **ApplicationIntent=ReadOnly**.  

## <a name="transparent-network-ip-resolution-tnir"></a>Resolución de IP de red transparente (TNIR)

Resolución de IP de red transparente (TNIR) es una revisión de la característica de MultiSubnetFailover existente. Afecta a la secuencia de conexión del controlador cuando el primero resuelva IP del nombre de host no responde y hay varias direcciones IP asociada con el nombre de host. Junto con MultiSubnetFailover proporcionan las siguientes secuencias de cuatro conexiones: 

- Habilitado TNIR & MultiSubnetFailover deshabilitado: se ha intentado una dirección IP, seguida de todas las direcciones IP en paralelo
- Habilitado TNIR & MultiSubnetFailover habilitado: se ha intentado todas las direcciones IP en paralelo
- Desactivado TNIR & MultiSubnetFailover deshabilitado: todas las direcciones IP se ha intentado una tras otra
- Desactivado TNIR & MultiSubnetFailover habilitado: se ha intentado todas las direcciones IP en paralelo

TNIR está habilitado de forma predeterminada, y MultiSubnetFailover está deshabilitada de forma predeterminada.

Este es un ejemplo de la habilitación de TNIR y MultiSubnetFailover utilizando el controlador PDO_SQLSRV:

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$connectionString = "sqlsrv:Server=$serverName; TransparentNetworkIPResolution=Enabled; MultiSubnetFailover=yes";
try {
    $conn = new PDO($connectionString, $username, $password, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
    // your code 
    // more of your code
    // when done, close the connection
    unset($conn);
} catch(PDOException $e) {
    print_r($e->errorInfo);
}
?>
```

## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Actualizar para utilizar clústeres de varias subredes a partir de la creación de reflejo de la base de datos  
Se producirá un error de conexión si las palabras clave de conexión **MultiSubnetFailover** y **Failover_Partner** se encuentran en la cadena de conexión. También se producirá un error si se usa **MultiSubnetFailover** y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve una respuesta del asociado de conmutación por error que indica que forma parte de un par de creación de reflejo de la base de datos.  
  
Si actualiza una aplicación [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] que actualmente use la creación de reflejo de la base de datos en un escenario de varias subredes, debe quitar la propiedad de conexión **Failover_Partner** y reemplazarla por **MultiSubnetFailover** establecida en **Yes**, así como reemplazar el nombre del servidor en la cadena de conexión por un agente de escucha de grupo de disponibilidad. Si una cadena de conexión usa **Failover_Partner** y **MultiSubnetFailover=true**, el controlador generará un error. En cambio, si una cadena de conexión usa **Failover_Partner** y **MultiSubnetFailover=false** (o **ApplicationIntent=ReadWrite**), la aplicación usará la creación de reflejo de la base de datos.  
  
Si la creación de reflejo de la base de datos se usa en la base de datos principal del grupo de disponibilidad y **MultiSubnetFailover=true** se usa en la cadena de conexión que se conecta a una base de datos principal, en lugar de a un agente de escucha de grupo de disponibilidad, el controlador devolverá un error.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>Ver también  
[Conexión al servidor](../../connect/php/connecting-to-the-server.md)  
  
