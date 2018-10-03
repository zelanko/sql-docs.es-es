---
title: Azure Active Directory | Microsoft Docs
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: 67f32c2c48188b3bcff50e22ca66bf2f563b1704
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814833"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Conectar mediante autenticación de Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) es una tecnología de administración de Id. de usuario central que funciona como una alternativa a [autenticación de SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). Azure AD permite las conexiones a Microsoft Azure SQL Database y SQL Data Warehouse con identidades federadas en Azure AD mediante un nombre de usuario y contraseña, autenticación integrada de Windows o un token de acceso de Azure AD; los controladores PHP para SQL Server ofrecen compatibilidad parcial con estas características.

Para usar Azure AD, use el **autenticación** palabra clave. Los valores que **autenticación** puede tardar en se explican en la tabla siguiente.

|Palabra clave|Valores|Descripción|
|-|-|-|
|**Autenticación**|No se establece (valor predeterminado)|Modo de autenticación determinado por otras palabras clave. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Autenticarse directamente en una instancia de SQL Server (que puede ser una instancia de Azure) con un nombre de usuario y contraseña. El nombre de usuario y la contraseña se deben pasar la cadena de conexión mediante el **UID** y **PWD** palabras clave. |
||`ActiveDirectoryPassword`|Autenticar con una identidad de Azure Active Directory mediante un nombre de usuario y una contraseña. El nombre de usuario y la contraseña se deben pasar la cadena de conexión mediante el **UID** y **PWD** palabras clave. |

El **autenticación** palabra clave afecta a la configuración de seguridad de conexión. Si se establece en la cadena de conexión, a continuación, de forma predeterminada el **Encrypt** palabra clave está establecida en true, por lo que el cliente solicitará cifrado. Además, el certificado de servidor se validará con independencia de la configuración de cifrado a menos que **TrustServerCertificate** se establece en true. Esto se distingue de los antiguos y menos segura, método de inicio de sesión, en el que no se valida el certificado de servidor a menos que se le solicita específicamente el cifrado en la cadena de conexión.

Antes de usar Azure AD con los controladores PHP para SQL Server en Windows, asegúrese de que ha instalado el [Microsoft Online Services Sign-In Assistant](https://www.microsoft.com/download/details.aspx?id=41950) (no es necesario para Linux y MacOS).

#### <a name="limitations"></a>Limitaciones

En Windows, el controlador ODBC subyacente admite más de un valor para el **autenticación** palabra clave, **ActiveDirectoryIntegrated**, pero los controladores PHP no admiten este valor en cualquier plataforma y, por tanto, también no admiten la autenticación basada en token de Azure AD.

## <a name="example"></a>Ejemplo

El ejemplo siguiente muestra cómo conectarse mediante **SqlPassword** y **ActiveDirectoryPassword**.

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

El ejemplo siguiente funciona igual que anteriormente con el controlador PDO_SQLSRV.

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
## <a name="see-also"></a>Ver también  
[Uso de Azure Active Directory con el controlador ODBC](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)
