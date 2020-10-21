---
title: 'Procedimientos: Conexión con la autenticación de Windows'
description: Obtenga información sobre lo que significa conectarse con la autenticación integrada de Windows mediante los controladores para PHP para SQL Server.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62334a277bc169350af4db1c2961595178e733a6
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081764"
---
# <a name="how-to-connect-using-windows-authentication"></a>Procedimientos: Conexión con la autenticación de Windows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

De forma predeterminada, los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] utilizan la autenticación de Windows para conectarse a SQL Server. Es importante tener en cuenta que, en la mayoría de los escenarios, esto significa que se utiliza la identidad del proceso o subproceso del servidor web (si este está usando el modo de suplantación) para conectarse al servidor, no la identidad de un usuario final.  
  
Deben tener en cuenta los siguientes puntos al utilizar la autenticación de Windows para conectarse a SQL Server:  
  
-   Las credenciales con las que se ejecuta el proceso (o subproceso) del servidor web deben asignarse a un inicio de sesión de SQL Server válido con el fin de establecer una conexión.  
  
-   Si SQL Server y el servidor web se encuentran en equipos diferentes, SQL Server debe configurarse para habilitar conexiones remotas.  
  
> [!NOTE]  
> Se pueden definir atributos de conexión como *Database* y *ConnectionPooling* al establecer una conexión. Para obtener una lista completa de los atributos de conexión admitidos, consulte [Connection Options](connection-options.md).  
  
Debe utilizarse la autenticación de Windows para conectarse a SQL Server siempre que sea posible por los siguientes motivos:  
  
-   Durante la autenticación no se transmiten credenciales por la red; los nombres de usuario y las contraseñas no se incrustan en la cadena de conexión de base de datos. Es decir, los atacantes o usuarios malintencionados no pueden obtener las credenciales supervisando la red o consultando las cadenas de conexión de los archivos de configuración.  
  
-   Los usuarios tienen que pasar por un proceso de administración de cuentas centralizada; se aplican directivas de seguridad (por ejemplo, periodos de expiración de contraseñas, longitudes mínimas de contraseñas y bloqueo de cuentas) después de varias solicitudes de inicio de sesión no válidas.  
  
Si no considera la autenticación de Windows una opción práctica, consulte [Procedimientos: Conexión mediante la autenticación de SQL Server](how-to-connect-using-sql-server-authentication.md).  
  
## <a name="sqlsrv-example"></a>Ejemplo de SQLSRV  
Mediante el uso del controlador SQLSRV de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], en el ejemplo siguiente se utiliza la autenticación de Windows para conectarse a una instancia local de SQL Server. Cuando se establece la conexión, en el servidor se realiza una consulta del inicio de sesión del usuario que está accediendo a la base de datos.  
  
En el ejemplo se da por hecho que SQL Server y la base de datos [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) están instalados en el equipo local. Los resultados se agregan al explorador cuando se ejecuta el ejemplo en el explorador.  
  
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
  
## <a name="pdo_sqlsrv-example"></a>Ejemplo de PDO_SQLSRV  
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
  
## <a name="see-also"></a>Consulte también  
[Cómo: Conexión mediante la autenticación de SQL Server](how-to-connect-using-sql-server-authentication.md)

[Guía de programación para los controladores de Microsoft para PHP para SQL Server](programming-guide-for-php-sql-driver.md)

[Sobre los ejemplos de código de la documentación](about-code-examples-in-the-documentation.md)

[Cómo: Creación de un inicio de sesión de SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)

[Cómo: Creación de un usuario de base de datos](../../relational-databases/security/authentication-access/create-a-database-user.md)

[Administrar usuarios, roles e inicios de sesión](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Separación de esquemas de usuario](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Permisos de objeto Grant (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
