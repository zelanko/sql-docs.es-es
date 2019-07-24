---
title: Azure Active Directory | Microsoft Docs
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: david-puglielli
ms.author: v-dapugl
manager: v-mabarw
ms.openlocfilehash: 8712681a244e969d230b0b7099acd4aa56334f11
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265177"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Conectar mediante autenticación de Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) es una tecnología de administración de ID. de usuario central que funciona como alternativa a la [autenticación de SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). Azure AD permite conexiones a Microsoft Azure SQL Database y SQL Data Warehouse con identidades federadas en Azure AD mediante un nombre de usuario y una contraseña, la autenticación integrada de Windows o un token de acceso Azure AD. Los controladores PHP para SQL Server ofrecen compatibilidad parcial con estas características.

Para usar Azure AD, use las palabras clave **Authentication** o **AccessToken** (son mutuamente excluyentes), tal y como se muestra en la tabla siguiente. Para obtener más información técnica, consulte [uso de Azure Active Directory con el controlador ODBC](../../connect/odbc/using-azure-active-directory.md).

|Palabra clave|Valores|Descripción|
|-|-|-|
|**AccessToken**|No establecido (valor predeterminado)|Modo de autenticación determinado por otras palabras clave. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md). |
||Una cadena de bytes|El token de acceso Azure AD extraído de una respuesta JSON de OAuth. La cadena de conexión no debe contener el ID. de usuario, la contraseña o la palabra clave de autenticación (requiere la versión 17 del controlador ODBC o posterior en Linux o macOS). |
|**Autenticación**|No establecido (valor predeterminado)|Modo de autenticación determinado por otras palabras clave. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Autentique directamente en una instancia de SQL Server (que puede ser una instancia de Azure) mediante un nombre de usuario y una contraseña. El nombre de usuario y la contraseña se deben pasar a la cadena de conexión mediante las palabras clave **UID** y **pwd** . |
||`ActiveDirectoryPassword`|Autenticarse con una identidad de Azure Active Directory mediante un nombre de usuario y una contraseña. El nombre de usuario y la contraseña se deben pasar a la cadena de conexión mediante las palabras clave **UID** y **pwd** . |
||`ActiveDirectoryMsi`|Realice la autenticación mediante una identidad administrada asignada por el sistema o una identidad administrada asignada por el usuario (requiere la versión de controlador ODBC 17.3.1.1 o posterior). Para obtener información general y tutoriales, consulte [¿Qué son las identidades administradas para los recursos de Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)|

La palabra clave **Authentication** afecta a la configuración de seguridad de la conexión. Si se establece en la cadena de conexión, de forma predeterminada, la palabra clave **Encrypt** se establece en true, lo que significa que el cliente solicitará el cifrado. Además, el certificado de servidor se validará independientemente de la configuración de cifrado a menos que **TrustServerCertificate** se establezca en true (de forma predeterminada,**false** ). Esta característica se distingue del método de inicio de sesión antiguo y menos seguro, en el que el certificado de servidor solo se valida cuando el cifrado se solicita específicamente en la cadena de conexión.

Al usar Azure AD con los controladores PHP para SQL Server en Windows, es posible que se le pida que instale el ayudante para el [Inicio de sesión de Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=41950) (no es necesario para ODBC 17 +).

#### <a name="limitations"></a>Limitaciones

En Windows, el controlador ODBC subyacente admite un valor más para la palabra clave **Authentication** , **ActiveDirectoryIntegrated**, pero los controladores php no admiten este valor en ninguna plataforma.

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>Ejemplo: conexión mediante SqlPassword y ActiveDirectoryPassword

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = array("UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword');

$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=SqlPassword.\n";
    sqlsrv_close($conn);
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = array("Database"=>$azureDatabase,
                        "UID"=>$azureUsername,
                        "PWD"=>$azurePassword,
                        "Authentication"=>'ActiveDirectoryPassword');

$conn = sqlsrv_connect($azureServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    sqlsrv_close($conn);
}

?>
```

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>Ejemplo: conectar con el controlador PDO_SQLSRV

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

try {
    $conn = new PDO("sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword);
    echo "Connected successfully with Authentication=SqlPassword.\n";
    $conn = null;
} catch (PDOException $e) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword);
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-azure-ad-access-token"></a>Ejemplo: conexión mediante el token de acceso Azure AD

### <a name="sqlsrv-driver"></a>Controlador SQLSRV

```php
<?php
// Using an access token to connect: do not use UID or PWD connection options
// Assume $accToken is the valid byte string extracted from an OAuth JSON response
$connectionInfo = array("Database"=>$azureAdDatabase, "AccessToken"=>$accToken);
$conn = sqlsrv_connect($azureAdServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Azure AD Access Token.\n";
    sqlsrv_close($conn);
}
?>
```

### <a name="pdosqlsrv-driver"></a>Controlador PDO_SQLSRV

```php
<?php
try {
    // Using an access token to connect: do not pass in $uid or $pwd
    // Assume $accToken is the valid byte string extracted from an OAuth JSON response
    $connectionInfo = "Database = $azureAdDatabase; AccessToken = $accToken;";
    $conn = new PDO("sqlsrv:server = $azureAdServer; $connectionInfo");
    echo "Connected successfully with Azure AD Access Token\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>Ejemplo: conexión mediante identidades administradas para recursos de Azure

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>Uso de la identidad administrada asignada por el sistema con el controlador SQLSRV

Al conectarse mediante la identidad administrada asignada por el sistema, no use las opciones UID ni PWD.

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$connectionInfo = array('Database'=>$azureDatabase,
                        'Authentication'=>'ActiveDirectoryMsi');
$conn = sqlsrv_connect($azureServer, $connectionInfo);

if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    $stmt = sqlsrv_query($conn, $tsql);
    if ($stmt === false) {
        echo "Failed to run the simple query (system-assigned).\n";
        print_r(sqlsrv_errors());
    } else {
        while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
            echo $row['SQL_VERSION'] . PHP_EOL;
        }

        sqlsrv_free_stmt($stmt);
    }
    
    sqlsrv_close($conn);
}
?>
```

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>Usar la identidad administrada asignada por el usuario con el controlador PDO_SQLSRV

Una identidad administrada asignada por el usuario se crea como un recurso independiente de Azure. Azure crea una identidad en el inquilino de Azure AD que es de confianza para la suscripción en uso. Una vez creada la identidad, la identidad se puede asignar a una o varias instancias de servicio de Azure. Copie el `Object ID` de esta identidad y establézcalo como el nombre de usuario en la cadena de conexión. 

Por lo tanto, al conectarse mediante la identidad administrada asignada por el usuario, proporcione el identificador de objeto como nombre de usuario, pero omita la contraseña.

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$azureUser = '2d68f56e-9547-4dae-aee8-f3g28ab9674x';    // Object ID of the identity
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryMsi;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer; $connectionInfo", $azureUser);
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    
    try {
        $stmt = $conn->query($tsql);
        $result = $stmt->fetchall(PDO::FETCH_ASSOC);
        print_r($result);

        unset($stmt);
    } catch (PDOException $e) {
        echo "Failed to run the simple query (user-assigned).\n";
    }
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="see-also"></a>Consulte también
[Uso de Azure Active Directory con el controlador ODBC](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)

[¿Qué son las identidades administradas para los recursos de Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
