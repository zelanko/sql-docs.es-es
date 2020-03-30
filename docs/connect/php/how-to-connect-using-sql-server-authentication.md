---
title: Conexión mediante la autenticación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, SQL Server Authentication
ms.assetid: 8d298830-3186-47e7-aef6-586b457901c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7d894b48fc6ec82450c42599f13725f0cd8ee1a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993550"
---
# <a name="how-to-connect-using-sql-server-authentication"></a>Cómo conectarse mediante la autenticación de SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] son compatibles con la autenticación de SQL Server para conectarse a dicho sistema.  
  
La autenticación de SQL Server solo debe usarse cuando no sea posible utilizar la autenticación de Windows. Para obtener información sobre cómo conectarse con la autenticación de Windows, consulte [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Se deben tener en cuenta los siguientes puntos al usar la autenticación de SQL Server para conectarse a ese sistema:  
  
-   El modo mixto de autenticación de SQL Server debe estar habilitado en el servidor.  
  
-   El identificador de usuario y la contraseña (atributos de conexión *UID* y *PWD* en el controlador SQLSRV) deben definirse al intentar establecer una conexión. El id. de usuario y la contraseña se deben asignar a un usuario y una contraseña válidos de SQL Server.  
  
> [!NOTE]  
> A las contraseñas que contienen una llave de cierre (}) se les debe aplicar una segunda llave de cierre como carácter de escape. Por ejemplo, si la contraseña de SQL Server es "contra}seña", el valor del atributo de conexión *PWD* debe establecerse como "contra}}seña".  
  
Se deben tener en cuenta las siguientes precauciones al usar la autenticación de SQL Server para conectarse ese sistema:  
  
-   Proteja (cifre) las credenciales que se transmiten por la red del servidor web a la base de datos. Las credenciales se cifran de manera predeterminada desde la versión SQL Server 2005. Para lograr una mayor seguridad, establezca el atributo de conexión Encrypt como "on" para cifrar todos los datos enviados al servidor.  
  
> [!NOTE]  
> Establecer el atributo de conexión Encrypt como "on" puede ralentizar el rendimiento, ya que el cifrado de datos puede suponer una tarea que requiera un elevado volumen de cálculos.  
  
-   No incluya valores para los atributos de conexión *UID* y *PWD* en texto sin formato de scripts PHP. Estos valores se deben almacenar en un directorio específico de la aplicación con los permisos restringidos adecuados.  
  
-   Evite el uso de la cuenta *sa* . Asigne la aplicación a un usuario de la base de datos que tenga los privilegios que desee y use una contraseña segura.  
  
> [!NOTE]  
> Se pueden definir otros atributos de conexión aparte del id. de usuario y la contraseña al establecer una conexión. Para obtener una lista completa de los atributos de conexión admitidos, consulte [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se usa el controlador SQLSRV con la autenticación de SQL Server para conectarse a una instancia local de SQL Server. Los valores para los atributos de conexión necesarios *UID* y *PWD* se extraen de los archivos de texto específicos de la aplicación *uid.txt* y *pwd.txt*, en el directorio *C:\AppData*. Una vez establecida la conexión, se consulta al servidor para comprobar el inicio de sesión de usuario.  
  
En el ejemplo se da por hecho que SQL Server y la base de datos [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) están instalados en el equipo local. Los resultados se agregan al explorador cuando se ejecuta el ejemplo en el explorador.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
  
/* Get UID and PWD from application-specific files.  */  
$uid = file_get_contents("C:\AppData\uid.txt");  
$pwd = file_get_contents("C:\AppData\pwd.txt");  
$connectionInfo = array( "UID"=>$uid,  
                         "PWD"=>$pwd,  
                         "Database"=>"AdventureWorks");  
  
/* Connect using SQL Server Authentication. */  
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
En este ejemplo se usa el controlador PDO_SQLSRV para demostrar cómo conectarse con la autenticación de SQL Server.  
  
```  
<?php  
   $serverName = "(local)";   
   $database = "AdventureWorks";  
  
   // Get UID and PWD from application-specific files.   
   $uid = file_get_contents("C:\AppData\uid.txt");  
   $pwd = file_get_contents("C:\AppData\pwd.txt");  
  
   try {  
      $conn = new PDO( "sqlsrv:server=$serverName;Database = $database", $uid, $pwd);   
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
  
   // Free statement and connection resources.   
   $stmt = null;   
   $conn = null;   
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Conexión mediante la autenticación de SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[Guía de programación para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)

[SUSER_SNAME (Transact-SQL)](../../t-sql/functions/suser-sname-transact-sql.md)

[Creación de un inicio de sesión de SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)

[Creación de un usuario de base de datos](../../relational-databases/security/authentication-access/create-a-database-user.md)

[Administrar usuarios, roles e inicios de sesión](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Separación de esquemas de usuario](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Permisos de objeto Grant (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
