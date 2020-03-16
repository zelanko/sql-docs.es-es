---
title: Uso de Azure Active Directory con el controlador ODBC | Microsoft Docs para SQL Server
ms.custom: ''
ms.date: 11/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e32889ceafa78d6c6eac716fca213f17badc5cea
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79286429"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Uso de Azure Active Directory con el controlador ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Propósito

Microsoft ODBC Driver for SQL Server con la versión 13.1 o superior permite que las aplicaciones ODBC se conecten a una instancia de SQL Azure mediante una identidad federada en Azure Active Directory con un nombre de usuario y contraseña, un token de acceso de Azure Active Directory, una identidad de servicio administrada de Azure Active Directory o autenticación integrada de Windows (_solo controlador de Windows_). Para la versión 13.1 del controlador ODBC, la autenticación de token de acceso de Azure Active Directory es _solo Windows_. La versión 17 del controlador ODBC y versiones posteriores admiten esta autenticación en todas las plataformas (Windows, Linux y Mac). En la versión 17.1 del controlador ODBC para Windows se incluye una nueva autenticación interactiva de Azure Active Directory con el identificador de inicio de sesión. Se agregó un nuevo método de autenticación de identidad de servicio administrada de Azure Active Directory en la versión 17.3.1.1 del controlador ODBC para las identidades asignadas por el sistema y por el usuario. Todo esto se logra mediante el uso de nuevas palabras clave de cadena de conexión y DSN con atributos de conexión.

> [!NOTE]
> El controlador ODBC en Linux y macOS solo admite la autenticación de Azure Active Directory directamente en Azure Active Directory. Si va a usar la autenticación de nombre de usuario y contraseña de Azure Active Directory desde un cliente Linux o macOS, y la configuración de Active Directory requiere que el cliente se autentique sobre un punto de conexión de Servicios de federación de Active Directory, se puede producir un error en la autenticación.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>Palabras clave de cadena de conexión y DSN nuevas y/o modificadas

Se puede usar la palabra clave `Authentication` al conectarse con un DSN o una cadena de conexión para controlar el modo de autenticación. El valor definido en la cadena de conexión reemplaza al del DNS, si se proporciona. El _valor de atributo anterior_ del parámetro `Authentication` es el valor calculado a partir de la cadena de conexión y los valores de DSN.

|Nombre|Valores|Valor predeterminado|Descripción|
|-|-|-|-|
|`Authentication`|(sin establecer), (cadena vacía), `SqlPassword`, `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`, `ActiveDirectoryMsi` |(sin establecer)|Controla el modo de autenticación.<table><tr><th>Value<th>Descripción<tr><td>(sin establecer)<td>Modo de autenticación determinado por otras palabras clave (opciones de conexión heredadas existentes).<tr><td>(cadena vacía)<td>(Solo cadena de conexión) Invalide y anule un valor de `Authentication` establecido en el DSN.<tr><td>`SqlPassword`<td>Autentíquese directamente en una instancia de SQL Server mediante un nombre de usuario y una contraseña.<tr><td>`ActiveDirectoryPassword`<td>Autentíquese con una identidad de Azure Active Directory mediante un nombre de usuario y una contraseña.<tr><td>`ActiveDirectoryIntegrated`<td>_Solo controlador de Windows_. Autentíquese con una identidad de Azure Active Directory mediante la autenticación integrada.<tr><td>`ActiveDirectoryInteractive`<td>_Solo controlador de Windows_. Autentíquese con una identidad de Azure Active Directory mediante la autenticación interactiva.<tr><td>`ActiveDirectoryMsi`<td>Autentíquese con una identidad de Azure Active Directory mediante autenticación de Managed Service Identity. Para la identidad asignada por el usuario, el UID se establece en el identificador de objeto de la identidad del usuario.</table>|
|`Encrypt`|(sin establecer), `Yes`, `No`|(consulte la descripción)|Controla el cifrado de una conexión. Si el valor de atributo anterior del parámetro `Authentication` no es _ninguno_ en el DSN o en la cadena de conexión, el valor predeterminado es `Yes`. De lo contrario, el valor predeterminado es `No`. Si el atributo `SQL_COPT_SS_AUTHENTICATION` invalida el valor de atributo anterior de `Authentication`, establezca explícitamente el valor de Encryption en el DSN, la cadena de conexión o el atributo de conexión. El valor de atributo anterior de Encryption es `Yes` si el valor se establece en `Yes` en el DSN o en la cadena de conexión.|

## <a name="new-andor-modified-connection-attributes"></a>Atributos de conexión nuevos o modificados

Se han incorporado o modificado los siguientes atributos de conexión anteriores a la conexión para admitir la autenticación de Azure Active Directory. Cuando un atributo de conexión tiene una cadena de conexión o una palabra clave de DSN correspondientes y se establece, el atributo de conexión tiene prioridad.

|Atributo|Tipo|Valores|Valor predeterminado|Descripción|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(sin establecer)|Consulte la descripción de la palabra clave `Authentication` anteriormente. `SQL_AU_NONE` se proporciona para reemplazar explícitamente un valor `Authentication` establecido en el DSN o la cadena de conexión, mientras `SQL_AU_RESET` desactiva el atributo si se estableció, lo que permite que el valor de la cadena de conexión o DSN tenga prioridad.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Puntero a `ACCESSTOKEN` o NULL|NULL|Si no es NULL, especifica el token de acceso de AzureAD que se va a usar. Es un error especificar un token de acceso y también las palabras clave de cadena de conexión `UID`, `PWD`, `Trusted_Connection` o `Authentication` o sus atributos equivalentes. <br> **NOTA:** La versión 13.1 del controlador ODBC solo lo admite en _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(consulte la descripción)|Controla el cifrado de una conexión. `SQL_EN_OFF` y `SQL_EN_ON` deshabilitan y habilitan el cifrado, respectivamente. Si el valor de atributo anterior del valor `Authentication` no es _ninguno_ o `SQL_COPT_SS_ACCESS_TOKEN` está establecido y `Encrypt` no se ha especificado en el DSN o en la cadena de conexión, el valor predeterminado es `SQL_EN_ON`. De lo contrario, el valor predeterminado es `SQL_EN_OFF`. Si el atributo de conexión `SQL_COPT_SS_AUTHENTICATION` se establece en no _ninguno_, establezca explícitamente `SQL_COPT_SS_ENCRYPT` en el valor deseado si no se ha especificado `Encrypt` en el DSN o la cadena de conexión. El valor efectivo de este atributo controla [si se utilizará el cifrado para la conexión.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|No se admite con Azure Active Directory, ya que los cambios de contraseña en las entidades de seguridad de AAD no se pueden realizar a través de una conexión ODBC. <br><br>La expiración de contraseñas para la autenticación de SQL Server se incorporó en SQL Server 2005. Se ha agregado el atributo `SQL_COPT_SS_OLDPWD` para permitir que el cliente especifique la contraseña antigua y la nueva contraseña para la conexión. Cuando se establezca esta propiedad, el proveedor no usará el grupo de conexiones para la primera conexión o para conexiones posteriores, puesto que la cadena de conexión contendrá la "contraseña antigua" que ahora ha cambiado.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_En desuso_; en su lugar, use `SQL_COPT_SS_AUTHENTICATION` establecido en `SQL_AU_AD_INTEGRATED`. <br><br>Fuerza el uso de la autenticación de Windows (Kerberos en Linux y macOS) para la validación de acceso en el inicio de sesión del servidor. Cuando se usa la autenticación de Windows, el controlador omite el identificador de usuario y los valores de contraseña proporcionados como parte del procesamiento de `SQLConnect`, `SQLDriverConnect` o `SQLBrowseConnect`.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Adiciones de interfaz de usuario para Azure Active Directory (solo controlador de Windows)

Las interfaces de conexión e instalación de DSN del controlador se han mejorado con las opciones adicionales necesarias para usar la autenticación con Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Creación y edición de nombres de orígenes de datos (DSN) en la interfaz de usuario

Es posible usar las nuevas opciones de autenticación de Azure AD al crear o editar un DSN existente mediante la interfaz de usuario de instalación del controlador:

`Authentication=ActiveDirectoryIntegrated` para la autenticación integrada de Azure Active Directory en SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` para la autenticación de nombre de usuario/contraseña de Azure Active Directory en SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` para la autenticación interactiva de Azure Active Directory en SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` para la autenticación de nombre de usuario/contraseña en SQL Server (Azure o de otro modo)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` en el caso de autenticación integrada SSPI para Windows

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

Las cinco opciones corresponden a `Trusted_Connection=Yes` (autenticación integrada existente solo con SSPI para Windows heredado) y `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, `ActiveDirectoryPassword` y `ActiveDirectoryInteractive`, respectivamente.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>Solicitud de SQLDriverConnect (solo controlador de Windows)

El cuadro de diálogo de solicitud que muestra SQLDriverConnect cuando solicita información necesaria para completar la conexión contiene tres nuevas opciones para la autenticación de Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Estas opciones se corresponden con las mismas cinco disponibles en la interfaz de usuario de instalación de DSN anterior.

### <a name="example-connection-strings"></a>Ejemplos de cadena de conexión
1. Autenticación de SQL Server: sintaxis heredada. No se valida el certificado de servidor y el cifrado solo se utiliza si el servidor lo exige. El nombre de usuario/contraseña se pasa en la cadena de conexión.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticación de SQL: nueva sintaxis. El cliente solicita el cifrado (el valor predeterminado de `Encrypt` es `true`) y se valida el certificado de servidor, independientemente de la configuración de cifrado (a menos que `TrustServerCertificate` se establezca en `true`). El nombre de usuario/contraseña se pasa en la cadena de conexión.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticación integrada de Windows (Kerberos en Linux y macOS) mediante SSPI (para una IaaS de SQL Server o SQL): sintaxis actual. No se valida el certificado de servidor, a menos que se use el cifrado. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Solo controlador de Windows_). Autenticación integrada de Windows mediante SSPI (si la base de datos de destino se encuentra en una IaaS de SQL Server o SQL): nueva sintaxis. El cliente solicita el cifrado (el valor predeterminado de `Encrypt` es `true`) y se valida el certificado de servidor, independientemente de la configuración de cifrado (a menos que `TrustServerCertificate` se establezca en `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticación de nombre de usuario/contraseña de AAD (si la base de datos de destino está en Azure SQL DB). Se valida el certificado de servidor, independientemente de la configuración de cifrado (a menos que `TrustServerCertificate` se establezca en `true`). El nombre de usuario/contraseña se pasa en la cadena de conexión. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Solo controlador de Windows_). Autenticación integrada de Windows mediante ADAL, que implica el canje de credenciales de cuenta de Windows para un token de acceso emitido por AAD, suponiendo que la base de datos de destino esté en Azure SQL Database. Se valida el certificado de servidor, independientemente de la configuración de cifrado (a menos que `TrustServerCertificate` se establezca en `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Solo controlador de Windows_). La autenticación interactiva de AAD usa tecnología de Azure Multi-Factor Authentication para configurar la conexión. En este modo, al proporcionar el identificador de inicio de sesión, se desencadena un cuadro de diálogo de autenticación de Azure que permite al usuario escribir la contraseña para completar la conexión. El nombre de usuario se pasa en la cadena de conexión.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. La autenticación de Managed Service Identity de AAD usa una identidad asignada por el sistema o asignada por el usuario para la autenticación con el fin de configurar la conexión. Para la identidad asignada por el usuario, el UID se establece en el identificador de objeto de la identidad del usuario.<br>
Para la identidad asignada por el sistema,<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
Para la identidad asignada por el usuario cuyo identificador de objeto es igual a myObjectId,<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- Al usar las nuevas opciones de Active Directory con el controlador ODBC de Windows, asegúrese de que se ha instalado la [Biblioteca de autenticación de Active Directory para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072). Al usar los controladores de Linux y macOS, asegúrese de que se ha instalado `libcurl`. En el caso de la versión de controlador 17.2 y versiones posteriores, esta no es una dependencia explícita, ya que no es necesaria para los otros métodos de autenticación u operaciones de ODBC.
>- Para conectarse con un nombre de usuario y una contraseña de la cuenta de SQL Server, ahora puede usar la nueva opción `SqlPassword`, que se recomienda especialmente para SQL Azure ya que esta opción habilita los valores predeterminados de conexión más seguros.
>- Para conectarse con un nombre de usuario y una contraseña de la cuenta de Azure Active Directory, especifique `Authentication=ActiveDirectoryPassword` en la cadena de conexión y las palabras clave `UID` y `PWD` con el nombre de usuario y la contraseña, respectivamente.
>- Para conectarse con autenticación integrada de Windows o de Active Directory (solo controlador de Windows), especifique `Authentication=ActiveDirectoryIntegrated` en la cadena de conexión. El controlador elegirá automáticamente el modo de autenticación correcto. No se debe especificar `UID` y `PWD`.
>- Para conectarse con autenticación interactiva de Active Directory (solo controlador de Windows), se debe especificar `UID`.

## <a name="authenticating-with-an-access-token"></a>Autenticación con token de acceso

El atributo anterior a la conexión `SQL_COPT_SS_ACCESS_TOKEN` permite el uso de un token de acceso obtenido de Azure AD para la autenticación en lugar de un nombre de usuario y una contraseña, y también omite la negociación y la obtención de un token de acceso por parte del controlador. Para usar un token de acceso, establezca el atributo de conexión `SQL_COPT_SS_ACCESS_TOKEN` en un puntero a una estructura `ACCESSTOKEN`:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN` es una estructura de longitud variable formada por un elemento _length_ de 4 bytes seguido de _length_ bytes de datos opacos que forman el token de acceso. Debido a cómo SQL Server controla los tokens de acceso, uno obtenido a través de una respuesta JSON de [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) debe expandirse para que cada byte vaya seguido de un byte 0 de relleno, similar a una cadena UCS-2 que solo contiene caracteres ASCII; sin embargo, el token es un valor opaco y la longitud especificada, en bytes, no debe incluir ningún terminador NULL. Dadas sus considerables restricciones de longitud y formato, este método de autenticación solo está disponible mediante programación a través del atributo de conexión `SQL_COPT_SS_ACCESS_TOKEN`; no hay ninguna palabra clave de cadena de conexión o DSN correspondiente. La cadena de conexión no debe contener las palabras clave `UID`, `PWD`, `Authentication` o `Trusted_Connection`.

> [!NOTE]
> La versión 13.1 del controlador ODBC solo admite esta autenticación en _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Código de ejemplo de autenticación de Azure Active Directory

En el ejemplo siguiente se muestra el código necesario para conectarse a SQL Server mediante Azure Active Directory con palabras clave de conexión. Tenga en cuenta que no es necesario cambiar el propio código de aplicación; la cadena de conexión, o el DSN si se usa uno, es la única modificación necesaria para usar AAD para la autenticación:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
En el ejemplo siguiente se muestra el código necesario para conectarse a SQL Server mediante Azure Active Directory con autenticación de token de acceso. En este caso, es necesario modificar el código de aplicación para procesar el token de acceso y establecer el atributo de conexión asociado.
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);      
    ...
    free(pAccToken);
~~~
A continuación se muestra una cadena de conexión de ejemplo para su uso con la autenticación interactiva de Azure Active Directory. Tenga en cuenta que no contiene el campo PWD, ya que la contraseña se escribiría con la pantalla de autenticación de Azure.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
A continuación se muestra una cadena de conexión de ejemplo para su uso con la autenticación de Managed Service Identity de Azure Active Directory. Tenga en cuenta que el UID se establece en el identificador de objeto de la identidad del usuario para la identidad asignada por el usuario.
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>Consulte también
[Compatibilidad de la autenticación basada en tokens con Azure SQL DB mediante la autenticación de Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

