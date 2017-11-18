---
title: "Cómo: conectarse mediante la autenticación de Windows | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
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
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 669ea9f70127c383f1390930a842cfee70366dd9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-connect-using-windows-authentication"></a>Cómo conectarse mediante la autenticación de Windows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

De forma predeterminada, los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] utilizan la autenticación de Windows para conectarse a SQL Server. Es importante tener en cuenta que, en la mayoría de los escenarios, esto significa que se utiliza la identidad del proceso o subproceso del servidor web (si este está usando el modo de suplantación) para conectarse al servidor, no la identidad de un usuario final.  
  
Deben tener en cuenta los siguientes puntos al utilizar la autenticación de Windows para conectarse a SQL Server:  
  
-   Las credenciales con las que se ejecuta el proceso (o subproceso) del servidor web deben asignarse a un inicio de sesión de SQL Server válido con el fin de establecer una conexión.  
  
-   Si SQL Server y el servidor web se encuentran en equipos diferentes, SQL Server debe configurarse para habilitar conexiones remotas.  
  
> [!NOTE]  
> Se pueden definir atributos de conexión como *Database* y *ConnectionPooling* al establecer una conexión. Para obtener una lista completa de los atributos de conexión admitidos, consulte [Connection Options](../../connect/php/connection-options.md).  
  
Debe utilizarse la autenticación de Windows para conectarse a SQL Server siempre que sea posible por los siguientes motivos:  
  
-   Durante la autenticación no se transmiten credenciales por la red; los nombres de usuario y las contraseñas no se incrustan en la cadena de conexión de base de datos. Es decir, los atacantes o usuarios malintencionados no pueden obtener las credenciales supervisando la red o consultando las cadenas de conexión de los archivos de configuración.  
  
-   Los usuarios tienen que pasar por un proceso de administración de cuentas centralizada; se aplican directivas de seguridad (por ejemplo, periodos de expiración de contraseñas, longitudes mínimas de contraseñas y bloqueo de cuentas) después de varias solicitudes de inicio de sesión no válidas.  
  
Si no considera la autenticación de Windows una opción práctica, consulte [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Ejemplo  
Mediante el uso del controlador SQLSRV de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], en el ejemplo siguiente se utiliza la autenticación de Windows para conectarse a una instancia local de SQL Server. Cuando se establece la conexión, en el servidor se realiza una consulta del inicio de sesión del usuario que está accediendo a la base de datos.  
  
En el ejemplo se da por hecho que SQL Server y la base de datos de [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) están instalados en el equipo local. Los resultados se agregan al explorador cuando se ejecuta el ejemplo en el explorador.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se utiliza el controlador PDO_SQLSRV para realizar la misma tarea que en el ejemplo anterior.  
  
```  
<?php  
try {  
   $conn = new PDO( "sqlsrv:Server=(local);Database=AdventureWorks", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
echo "Connected to SQL Server\n";  
  
$query = 'select * from Person.ContactType';   
$stmt = $conn->query( $query );   
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
   print_r( $row );   
}  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
[Guía de programación para el controlador SQL para PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
[Cómo crear un inicio de sesión de SQL Server](http://go.microsoft.com/fwlink/?LinkId=106325)  
[Cómo crear un usuario de base de datos](http://go.microsoft.com/fwlink/?LinkId=106327)  
[Administrar usuarios, roles e inicios de sesión](http://go.microsoft.com/fwlink/?LinkId=106329)  
[Separación usuario-esquema](http://go.microsoft.com/fwlink/?LinkId=106330)  
[Permisos de objeto GRANT (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=106332)  
  

