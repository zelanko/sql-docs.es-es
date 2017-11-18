---
title: "Opciones de conexión | Documentos de Microsoft"
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aadb44954096cbbcb520850a54d4cc2c41911f08
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="connection-options"></a>Opciones de conexión
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se enumera las opciones que se permiten en la matriz asociativa (al usar [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) en el controlador SQLSRV) o las palabras clave que se permiten en el nombre de origen de datos (dsn) (cuando se usa [PDO:: __construct ](../../connect/php/pdo-construct.md) en el controlador PDO_SQLSRV).  

|Key|Valor|Descripción|Valor de DB-Library|  
|-------|---------|---------------|-----------|  
|APP|String|Especifica el nombre de aplicación que se utiliza en el seguimiento.|No hay ningún valor establecido.|  
|Intención de aplicaciones|String|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son ReadOnly y ReadWrite.<br /><br />Para obtener más información sobre el soporte de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vea [Controlador PHP para el soporte de SQL Server para la alta disponibilidad con recuperación ante desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|ReadWrite|  
|AttachDBFileName|String|Especifica qué archivo de base de datos debe asociar el servidor.|No hay ningún valor establecido.|  
|Autenticación|Una de las siguientes cadenas:<br /><br />'SqlPassword'<br /><br />'ActiveDirectoryPassword'|Especifica el modo de autenticación.|No se ha establecido.|  
|CharacterSet<br /><br />(no compatible con el controlador PDO_SQLSRV)|String|Especifica el juego de caracteres que se utiliza para enviar datos al servidor.<br /><br />Los valores posibles son SQLSRV_ENC_CHAR y UTF-8. Para obtener más información, consulte [How to: Send and Retrieve UTF-8 Data Using Built-In UTF-8 Support](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|SQLSRV_ENC_CHAR|  
|ConnectionPooling|1 o **True** para activar la agrupación de conexiones.<br /><br />0 o **False** para desactivar la agrupación de conexiones.|Especifica si la conexión se asigna desde una agrupación de conexiones (1 o **true**) o no (0 o **false**).<sup> 1</sup>|**True** (1)|  
|Base de datos|String|Especifica el nombre de la base de datos en uso para la conexión que se va a establecer<sup>2</sup>.|La base de datos predeterminada del inicio de sesión que se va a utilizar.|  
|Cifrar|1 o **True** activar el cifrado.<br /><br />0 o **False** para desactivar el cifrado desactivado.|Especifica si se cifra la comunicación con SQL Server (1 o **true**) o sin cifrar (0 o **false**)<sup>3</sup>.|**false** (0)|  
|Failover_Partner|String|Especifica el servidor y la instancia del reflejo de la base de datos (si está habilitada y configurada) que se usará cuando el servidor principal no esté disponible.<br /><br />Existen restricciones en el uso de Failover_Partner con MultiSubnetFailover. Para obtener más información, vea [Controlador PHP para el soporte de SQL Server para la alta disponibilidad con recuperación ante desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|No hay ningún valor establecido.|  
|LoginTimeout|Integer (controlador SQLSRV)<br /><br />String (controlador PDO_SQLSRV)|Especifica el número de segundos que se espera antes de que se produzca un error en el intento de conexión.|Sin tiempo de espera.|  
|MultipleActiveResultSets|1 o **True** para utilizar conjuntos de resultados activos múltiples.<br /><br />0 o **False** para deshabilitar conjuntos de resultados activos múltiples.|Deshabilita o habilita explícitamente la compatibilidad con conjuntos de resultados activos múltiples (MARS).<br /><br />Para obtener más información, vea [Cómo: deshabilitar activos múltiples &#40; MARS &#41; ](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md).|True (1)|  
|MultiSubnetFailover|String|Especifique siempre **multiSubnetFailover = yes** al conectarse a la escucha del grupo de disponibilidad de un [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] grupo de disponibilidad o una [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] instancia de clúster de conmutación por error. **multiSubnetFailover = yes** configura [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para proporcionar una detección más rápida y conexión con el servidor (actualmente) activo. Los valores posibles Yes y No.<br /><br />Para obtener más información sobre el soporte de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vea [Controlador PHP para el soporte de SQL Server para la alta disponibilidad con recuperación ante desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|No|  
|PWD<br /><br />(no compatible con el controlador PDO_SQLSRV)|String|Especifica la contraseña asociada con el identificador de usuario que se utilizará al conectarse con la autenticación de SQL Server<sup>4</sup>.|No hay ningún valor establecido.|  
|QuotedId|1 o **true** para usar las reglas de SQL-92.<br /><br />0 o **False** para usar las reglas heredadas.|Especifica si se debe usar las reglas de SQL-92 para identificadores entrecomillados (1 o **true**) o para usar las reglas heredadas de Transact-SQL (0 o **false**).|**True** (1)|  
|ReturnDatesAsStrings<br /><br />(no compatible con el controlador PDO_SQLSRV)|1 o **True** para devolver tipos de fecha y hora como cadenas.<br /><br />0 o **False** para devolver tipos de fecha y hora como tipos de datos PHP **DateTime** .|Recupera tipos de fecha y hora (datetime, date, time, datetime2 y datetimeoffset) como cadenas o como tipos de datos PHP. Cuando se utiliza el controlador PDO_SQLSRV, las fechas se devuelven como cadenas. El controlador PDO_SQLSRV no tiene ningún **datetime** tipo.<br /><br />Para obtener más información, vea [Cómo recuperar el tipo de fecha y hora como cadenas con el controlador SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).|**False**|  
|De desplazamiento|String|"en búfer" indica que desea que un cursor de cliente (en búfer), que permite almacenar en caché un conjunto de resultados en memoria completo. Para obtener más información, vea [tipos de Cursor &#40; Controlador SQLSRV &#41; ](../../connect/php/cursor-types-sqlsrv-driver.md).|Cursor de solo avance|  
|Server<br /><br />(no compatible con el controlador SQLSRV)|String|El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a la que se conectará.<br /><br />También puede especificar un nombre de red virtual para conectarse a un grupo de disponibilidad AlwaysOn. Para obtener más información sobre el soporte de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vea [Controlador PHP para el soporte de SQL Server para la alta disponibilidad con recuperación ante desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|Server es una palabra clave obligatoria (aunque no tiene que ser la primera palabra clave de la cadena de conexión). Si no se pasa un nombre de servidor a la palabra clave, se realiza un intento para conectarse a la instancia local.<br /><br />El valor transmitido al servidor puede ser el nombre de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o la dirección IP de la instancia. También puede especificar un número de puerto (por ejemplo, `sqlsrv:server=(local),1033`).<br /><br />A partir de la versión 3.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] , también puede especificar una instancia de LocalDB con `server=(localdb)\instancename`. Para obtener más información, consulte [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).|  
|TraceFile|String|Especifica la ruta de acceso del archivo utilizado para los datos de seguimiento.|No hay ningún valor establecido.|  
|TraceOn|1 o **True** para habilitar el seguimiento.<br /><br />0 o **False** para deshabilitar el seguimiento.|Especifica si está habilitado el seguimiento de ODBC (1 o **true**) o deshabilitado (0 o **false**) para la conexión que se va a establecer.|**false** (0)|  
|TransactionIsolation|El controlador SQLSRV utiliza los siguientes valores:<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />El controlador PDO_SQLSRV utiliza los siguientes valores:<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|Especifica el nivel de aislamiento de la transacción.<br /><br />Para obtener más información sobre el aislamiento de transacciones, consulte [SET TRANSACTION ISOLATION LEVEL](http://go.microsoft.com/fwlink/?LinkID=191497) en la documentación de SQL Server.|SQLSRV_TXN_READ_COMMITTED<br /><br />o bien<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|TransparentNetworkIPResolution|**Habilitado** o **deshabilitado**|Afecta a la secuencia de conexión cuando la primera resuelve la dirección IP del nombre de host no responde y hay varias direcciones IP asociadas con el nombre de host.<br /><br />Interactúa con MultiSubnetFailover para proporcionar secuencias de una conexión distinta. Para obtener más información, consulte [utilizando resolución de IP de red transparente](https://docs.microsoft.com/en-us/sql/connect/odbc/using-transparent-network-ip-resolution).|Habilitado|
|TrustServerCertificate|1 o **True** para confiar en certificado.<br /><br />0 o **False** para no confiar en el certificado.|Especifica si el cliente debe confiar (1 o **true**) o rechazar (0 o **false**) un certificado de servidor autofirmado.|**false** (0)|  
|UID<br /><br />(no compatible con el controlador PDO_SQLSRV)|String|Especifica el identificador de usuario que se utilizará al conectar con la autenticación de SQL Server<sup>4</sup>.|No hay ningún valor establecido.|  
|WSID|String|Especifica el nombre del equipo del que se realizará el seguimiento.|No hay ningún valor establecido.|  

1. El `ConnectionPooling` atributo no puede utilizarse para habilitar o deshabilitar la agrupación de conexiones en Linux y Mac. Vea [agrupación de conexiones (controladores de Microsoft para PHP para SQL Server)](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).

2. Todas las consultas ejecutadas en la conexión establecida se realizan en la base de datos especificada por el *base de datos* atributo. Sin embargo, si el usuario tiene los permisos adecuados, en otras bases de datos pueden tener acceso a datos mediante un nombre completo. Por ejemplo, si la *maestro* base de datos se establece con el *base de datos* el atributo de conexión, todavía es posible ejecutar una consulta de Transact-SQL que tiene acceso a la  *AdventureWorks.HumanResources.Employee* tabla utilizando el nombre completo.  

3. Si se habilita *Encryption* , puede afectar al rendimiento de algunas aplicaciones debido a la sobrecarga computacional que se precisa para cifrar los datos.  

4. El nombre de la instancia de *UID* y *PWD* al realizar la conexión con la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  

Muchas de las claves admitidas son atributos de cadena de conexión ODBC. Para obtener información sobre las cadenas de conexión ODBC, consulte [Usar palabras clave de cadena de conexión con SQL Server Native Client](http://go.microsoft.com/fwlink/?LinkId=105504).  

## <a name="see-also"></a>Vea también  
[Conexión al servidor](../../connect/php/connecting-to-the-server.md)  

