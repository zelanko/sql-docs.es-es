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
manager: mbarwin
ms.openlocfilehash: 30423cd7c15a920d99fad4c0ea08e074beaece0b
ms.sourcegitcommit: 8664c2452a650e1ce572651afeece2a4ab7ca4ca
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/26/2019
ms.locfileid: "56828055"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Conectar mediante autenticación de Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) es una tecnología de administración de Id. de usuario central que funciona como una alternativa a [autenticación de SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). Azure AD permite las conexiones a Microsoft Azure SQL Database y SQL Data Warehouse con identidades federadas en Azure AD mediante un nombre de usuario y contraseña, autenticación integrada de Windows o un token de acceso de Azure AD. Los controladores PHP para SQL Server ofrecen compatibilidad parcial con estas características.

Para usar Azure AD, use el **autenticación** o **AccessToken** palabras clave (que son mutuamente excluyentes), tal como se muestra en la tabla siguiente. Para obtener más información, consulte [mediante Azure Active Directory con el controlador ODBC](../../connect/odbc/using-azure-active-directory.md).

|Palabra clave|Valores|Descripción|
|-|-|-|
|**AccessToken**|No se establece (valor predeterminado)|Modo de autenticación determinado por otras palabras clave. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md). |
||Una cadena de bytes|Azure AD Access Token extraído de una respuesta de OAuth JSON. La cadena de conexión no debe contener la palabra clave de autenticación, la contraseña o Id. de usuario (requiere el controlador ODBC versión 17 o posterior en Linux o macOS). |
|**Autenticación**|No se establece (valor predeterminado)|Modo de autenticación determinado por otras palabras clave. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Autenticarse directamente en una instancia de SQL Server (que puede ser una instancia de Azure) con un nombre de usuario y contraseña. El nombre de usuario y la contraseña se deben pasar la cadena de conexión mediante el **UID** y **PWD** palabras clave. |
||`ActiveDirectoryPassword`|Autenticar con una identidad de Azure Active Directory mediante un nombre de usuario y una contraseña. El nombre de usuario y la contraseña se deben pasar la cadena de conexión mediante el **UID** y **PWD** palabras clave. |
||`ActiveDirectoryMsi`|Autenticarse con una identidad administrada asignado por el sistema o una identidad administrada asignada por el usuario (requiere el controlador ODBC versión 17.3.1.1 o superior). Para información general y tutoriales, consulte [What ' s identidades administradas para los recursos de Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).|

El **autenticación** palabra clave afecta a la configuración de seguridad de conexión. Si se establece en la cadena de conexión, a continuación, de forma predeterminada el **Encrypt** palabra clave está establecida en true, lo que significa que el cliente solicitará cifrado. Además, el certificado de servidor se validará con independencia de la configuración de cifrado a menos que **TrustServerCertificate** se establece en true (**false** de forma predeterminada). Esta característica se distingue de la antigua, menos el método de inicio de sesión seguro, en el que se valida el certificado de servidor solo cuando se le solicita específicamente el cifrado en la cadena de conexión.

Al usar Azure AD con los controladores PHP para SQL Server en Windows, se le pedirá que instale el [Microsoft Online Services Sign-In Assistant](https://www.microsoft.com/download/details.aspx?id=41950) (no se necesita para ODBC 17 +).

#### <a name="limitations"></a>Limitaciones

En Windows, el controlador ODBC subyacente admite más de un valor para el **autenticación** palabra clave, **ActiveDirectoryIntegrated**, pero los controladores PHP no admiten este valor en cualquier plataforma.

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>Ejemplo: conectar usando SqlPassword y ActiveDirectoryPassword

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

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>Por ejemplo, conectar con el controlador PDO_SQLSRV

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

## <a name="example---connect-using-azure-ad-access-token"></a>Por ejemplo, conectar con el Token de acceso de Azure AD

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

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>Por ejemplo, conectarse con identidades administradas para los recursos de Azure

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>Uso de la identidad administrada asignado por el sistema con el controlador SQLSRV

Cuando se conecta mediante el sistema asigna la identidad administrada, no use las opciones UID y PWD.

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

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>Uso de la identidad administrada asignada por el usuario con el controlador PDO_SQLSRV

Se crea una identidad administrada asignada por el usuario como un recurso de Azure independiente. Azure crea una identidad en el inquilino de Azure AD que confía la suscripción en uso. Después de crea la identidad, la identidad puede asignarse a una o varias instancias de servicio de Azure. Copia el `Object ID` de esta identidad y un conjunto como el usuario el nombre de la cadena de conexión. 

Por lo tanto, cuando se conecta mediante el asignada por el usuario administrado identidad, proporcione el identificador de objeto como el nombre de usuario y omite la contraseña.

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

[¿Qué es identidades administradas para los recursos de Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
