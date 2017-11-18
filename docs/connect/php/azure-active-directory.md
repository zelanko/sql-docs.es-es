---
title: Azure Active Directory | Documentos de Microsoft
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.suite: sql
ms.custom: 
ms.technology:
- drivers
ms.topic: article
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 01d921ebee152924b905fa7a9de8c6d46f41ca64
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="connect-using-azure-active-directory-authentication"></a>Conectarse mediante la autenticación de Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis) (Azure AD) es una tecnología de administración de Id. de usuario central que funciona como una alternativa a [autenticación de SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). Azure AD permite conexiones a la base de datos de SQL de Microsoft Azure y almacenamiento de datos de SQL con identidades federadas en Azure AD mediante un nombre de usuario y una contraseña, autenticación integrada de Windows o un token de acceso de Azure AD; los controladores PHP para SQL Server ofrecen una compatibilidad parcial para estas características.

Para usar Azure AD, use la **autenticación** palabra clave. Los valores que **autenticación** puede tardar en se explican en la tabla siguiente.

|Palabra clave|Valores|Description|
|-|-|-|
|**Autenticación**|No se establece (valor predeterminado)|Modo de autenticación determinado por otras palabras clave. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Autenticarse directamente en una instancia de SQL Server (que puede ser una instancia de Azure) utilizando un nombre de usuario y contraseña. El nombre de usuario y la contraseña se deben pasar a la cadena de conexión mediante el **UID** y **PWD** palabras clave. |
||`ActiveDirectoryPassword`|Autenticar con una identidad de Azure Active Directory con un nombre de usuario y contraseña. El nombre de usuario y la contraseña se deben pasar a la cadena de conexión mediante el **UID** y **PWD** palabras clave. |

El **autenticación** palabra clave afecta a la configuración de seguridad de conexión. Si se establece en la cadena de conexión, a continuación, de forma predeterminada el **Encrypt** palabra clave está establecida en true, por lo que el cliente solicitará el cifrado. Además, el certificado de servidor se validarán con independencia de la configuración de cifrado a menos que **TrustServerCertificate** se establece en true. Esto se diferencia de la antigua así como menos seguro, método de inicio de sesión, en el que no se valida el certificado de servidor a menos que se le solicita específicamente el cifrado en la cadena de conexión.

Antes de usar Azure AD con los controladores PHP para SQL Server en Windows, asegúrese de que ha instalado el [Microsoft Online Services Sign-In Assistant](https://www.microsoft.com/download/details.aspx?id=41950) (no se necesita para Linux y Mac OS).

#### <a name="limitations"></a>Limitaciones

En Windows, el controlador ODBC subyacente admite más de un valor para el **autenticación** palabra clave, **ActiveDirectoryIntegrated**, pero los controladores PHP no es compatible con este valor en cualquier plataforma y, por lo que también no se admite la autenticación basada en autorización token de Azure AD.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo conectarse mediante **SqlPassword** y **ActiveDirectoryPassword**.

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = array( "UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword' );

    $conn = sqlsrv_connect( $serverName, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=SqlPassword.\n";
        sqlsrv_close( $conn );
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = array( "Database"=>$azureDatabase, "UID"=>$azureUsername, "PWD"=>$azurePassword,
                             "Authentication"=>'ActiveDirectoryPassword' );

    $conn = sqlsrv_connect( $azureServer, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        sqlsrv_close( $conn );
    }

    ?>
```

En el ejemplo siguiente se hace lo mismo que anteriormente con el controlador PDO_SQLSRV.

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword );
        echo "Connected successfully with Authentication=SqlPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword );
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    ?>
```
## <a name="see-also"></a>Vea también  
[Con Azure Active Directory con el controlador ODBC](https://docs.microsoft.com/en-us/sql/connect/odbc/using-azure-active-directory)

