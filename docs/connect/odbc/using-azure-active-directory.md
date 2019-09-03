---
title: Usar Azure Active Directory con el controlador ODBC | Microsoft Docs para SQL Server
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
ms.openlocfilehash: c0f9d73dace4e17d87e1c93da703786fc920b2fb
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176171"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Uso de Azure Active Directory con el controlador ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Finalidad

La Microsoft ODBC Driver for SQL Server con la versión 13,1 o posterior permite que las aplicaciones ODBC se conecten a una instancia de SQL Azure mediante una identidad federada en Azure Active Directory con un nombre de usuario y contraseña, un token de acceso Azure Active Directory, un Azure Active Identidad de servicio administrada de directorios o autenticación integrada de Windows (_solo para controladores de Windows_). Para la versión 13,1 del controlador ODBC, la autenticación Azure Active Directory token de acceso es _solo Windows_. La versión 17 del controlador ODBC y versiones posteriores admiten esta autenticación en todas las plataformas (Windows, Linux y Mac). En la versión 17,1 del controlador ODBC para Windows se incluye una nueva autenticación interactiva de Azure Active Directory con ID. de inicio de sesión. Se agregó un nuevo Azure Active Directory método de autenticación de identidad de servicio administrada en la versión 17.3.1.1 del controlador ODBC para las identidades asignadas por el sistema y por el usuario. Todo esto se logra mediante el uso de nuevas palabras clave de cadena de conexión y DSN, y atributos de conexión.

> [!NOTE]
> El controlador ODBC en Linux y macOS no es compatible con Servicios de federación de Active Directory (AD FS). Si usa Azure Active Directory la autenticación de nombre de usuario/contraseña desde un cliente Linux o macOS y la configuración de Active Directory incluye servicios federados, puede producirse un error de autenticación.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>Palabras clave de cadena de conexión y DSN nuevas y/o modificadas

La `Authentication` palabra clave se puede usar al conectarse con un DSN o una cadena de conexión para controlar el modo de autenticación. El valor establecido en la cadena de conexión invalida que en el DSN, si se proporciona. El _valor de atributo anterior_ de la `Authentication` configuración es el valor calculado a partir de la cadena de conexión y los valores de DSN.

|Nombre|Valores|Valor predeterminado|Descripción|
|-|-|-|-|
|`Authentication`|(sin establecer), (cadena vacía), `SqlPassword` `ActiveDirectoryPassword`,, `ActiveDirectoryIntegrated` `ActiveDirectoryInteractive`,,`ActiveDirectoryMsi` |(sin establecer)|Controla el modo de autenticación.<table><tr><th>Valor<th>Descripción<tr><td>(sin establecer)<td>Modo de autenticación determinado por otras palabras clave (opciones de conexión heredadas existentes).<tr><td>(cadena vacía)<td>Ayuda con las cadenas de conexión Invalide y `Authentication` anule la definición de un valor establecido en el DSN.<tr><td>`SqlPassword`<td>Autentique directamente en una instancia de SQL Server mediante un nombre de usuario y una contraseña.<tr><td>`ActiveDirectoryPassword`<td>Autenticarse con una identidad de Azure Active Directory mediante un nombre de usuario y una contraseña.<tr><td>`ActiveDirectoryIntegrated`<td>_Solo Windows Driver_. Autenticarse con una identidad de Azure Active Directory mediante la autenticación integrada.<tr><td>`ActiveDirectoryInteractive`<td>_Solo Windows Driver_. Autenticarse con una identidad de Azure Active Directory mediante la autenticación interactiva.<tr><td>`ActiveDirectoryMsi`<td>Autentique con Azure Active Directory identidad mediante la autenticación de identidad de servicio administrada. Para la identidad asignada por el usuario, el UID se establece en el identificador de objeto de la identidad del usuario.</table>|
|`Encrypt`|(sin establecer), `Yes`, `No`|(consulte la descripción)|Controla el cifrado de una conexión. Si el valor de atributo anterior de la `Authentication` configuración no es _ninguno_ en el DSN o la cadena de conexión, el `Yes`valor predeterminado es. De lo contrario, el valor predeterminado es `No`. Si el atributo `SQL_COPT_SS_AUTHENTICATION` invalida el valor de atributo anterior de `Authentication`, establezca explícitamente el valor de Encryption en el DSN o la cadena de conexión o el atributo de conexión. El valor de atributo anterior del cifrado `Yes` es si el valor se `Yes` establece en en el DSN o en la cadena de conexión.|

## <a name="new-andor-modified-connection-attributes"></a>Atributos de conexión nuevos o modificados

Los siguientes atributos de conexión anteriores a la conexión se han introducido o modificado para admitir la autenticación Azure Active Directory. Cuando un atributo de conexión tiene una cadena de conexión correspondiente o una palabra clave de DSN y se establece, el atributo de conexión tiene prioridad.

|Attribute|Tipo|Valores|Valor predeterminado|Descripción|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(sin establecer)|Vea la descripción `Authentication` de la palabra clave anterior. `SQL_AU_NONE`se proporciona para reemplazar explícitamente un valor establecido `Authentication` en el DSN o la cadena de conexión, mientras `SQL_AU_RESET` que desactiva el atributo si se estableció, lo que permite que el valor de la cadena de conexión o DSN tenga prioridad.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Puntero a `ACCESSTOKEN` o null|NULL|Si no es null, especifica el token de acceso de AzureAD que se va a usar. Es un error especificar un token de acceso `UID`y también `Trusted_Connection`, `PWD`, o `Authentication` palabras clave de cadena de conexión o sus atributos equivalentes. <br> **Nota:** La versión 13,1 del controlador ODBC solo es compatible con _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(consulte la descripción)|Controla el cifrado de una conexión. `SQL_EN_OFF`y `SQL_EN_ON` deshabilite y habilite el cifrado, respectivamente. Si el valor del atributo anterior de la `Authentication` configuración no es _ninguno_ o `SQL_COPT_SS_ACCESS_TOKEN` está establecido, y `Encrypt` no se especificó en el DSN o en la cadena de conexión, `SQL_EN_ON`el valor predeterminado es. De lo contrario, el valor predeterminado es `SQL_EN_OFF`. Si el atributo `SQL_COPT_SS_AUTHENTICATION` de conexión se establece en no _ninguno_, establézcalo `SQL_COPT_SS_ENCRYPT` explícitamente en el valor deseado si `Encrypt` no se especificó en el DSN o la cadena de conexión. El valor efectivo de este atributo controla [si se usará el cifrado para la conexión.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|No se admite con Azure Active Directory, ya que los cambios de contraseña en las entidades de seguridad de AAD no se pueden realizar a través de una conexión ODBC. <br><br>La expiración de contraseñas para la autenticación de SQL Server se incorporó en SQL Server 2005. El `SQL_COPT_SS_OLDPWD` atributo se agregó para permitir al cliente proporcionar la contraseña antigua y la nueva para la conexión. Cuando se establezca esta propiedad, el proveedor no usará el grupo de conexiones para la primera conexión o para conexiones posteriores, puesto que la cadena de conexión contendrá la "contraseña antigua" que ahora ha cambiado.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|En _desuso_; en `SQL_COPT_SS_AUTHENTICATION` su lugar `SQL_AU_AD_INTEGRATED` , use establecido en. <br><br>Fuerza el uso de la autenticación de Windows (Kerberos en Linux y macOS) para la validación de acceso en el inicio de sesión del servidor. Cuando se utiliza la autenticación de Windows, el controlador omite los valores de identificador de usuario y contraseña proporcionados `SQLDriverConnect`como parte `SQLBrowseConnect` del procesamiento de `SQLConnect`, o.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Adiciones de interfaz de usuario para Azure Active Directory (solo en el controlador de Windows)

La instalación de DSN y las IUs de conexión del controlador se han mejorado con las opciones adicionales necesarias para usar la autenticación con Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Crear y editar DSN en la interfaz de usuario

Es posible usar las nuevas opciones de autenticación de Azure AD al crear o editar un DSN existente mediante la interfaz de usuario del programa de instalación del controlador:

`Authentication=ActiveDirectoryIntegrated` para la autenticación integrada de Azure Active Directory en SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword`para Azure Active Directory la autenticación de nombre de usuario/contraseña en SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` para la autenticación interactiva de Azure Active Directory en SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword`para la autenticación de nombre de usuario/contraseña en SQL Server (Azure o de otro modo)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes`para la autenticación integrada SSPI heredada de Windows

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

Las cinco opciones corresponden a `Trusted_Connection=Yes` (autenticación integrada de Windows SSPI heredada existente) y `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword` `ActiveDirectoryPassword`, y `ActiveDirectoryInteractive`, respectivamente.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>Solicitud de SQLDriverConnect (solo para el controlador de Windows)

El cuadro de diálogo de solicitud que se muestra por SQLDriverConnect cuando solicita información necesaria para completar la conexión contiene tres nuevas opciones para la autenticación Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Estas opciones se corresponden con los cinco mismos disponibles en la interfaz de usuario de instalación de DSN anterior.

### <a name="example-connection-strings"></a>Ejemplos de cadena de conexión
1. Autenticación SQL Server: sintaxis heredada. No se valida el certificado de servidor y el cifrado solo se utiliza si el servidor lo exige. El nombre de usuario/contraseña se pasa en la cadena de conexión.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticación de SQL: nueva sintaxis. El cliente solicita el cifrado (el valor `Encrypt` predeterminado `true`es) y se valida el certificado de servidor, independientemente de la configuración de cifrado (a `true`menos `TrustServerCertificate` que se establezca en). El nombre de usuario/contraseña se pasa en la cadena de conexión.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticación integrada de Windows (Kerberos en Linux y macOS) mediante SSPI (para SQL Server o IaaS de SQL): sintaxis actual. No se valida el certificado de servidor, a menos que se use el cifrado. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Solo Windows Driver_). Autenticación integrada de Windows mediante SSPI (si la base de datos de destino está en SQL Server o IaaS de SQL), nueva sintaxis. El cliente solicita el cifrado (el valor `Encrypt` predeterminado `true`es) y se valida el certificado de servidor, independientemente de la configuración de cifrado (a `true`menos `TrustServerCertificate` que se establezca en). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticación de nombre de usuario/contraseña de AAD (si la base de datos de destino está en Azure SQL DB). Se valida el certificado de servidor, independientemente de la configuración de cifrado (a `true`menos que `TrustServerCertificate` se establezca en). El nombre de usuario/contraseña se pasa en la cadena de conexión. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Solo Windows Driver_). Autenticación integrada de Windows mediante ADAL, que implica el canje de credenciales de cuenta de Windows para un token de acceso emitido por AAD, suponiendo que la base de datos de destino está en Azure SQL Database. Se valida el certificado de servidor, independientemente de la configuración de cifrado (a `true`menos que `TrustServerCertificate` se establezca en). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Solo Windows Driver_). La autenticación interactiva de AAD usa tecnología de Azure multi-factor Authentication para configurar la conexión. En este modo, al proporcionar el identificador de inicio de sesión, se desencadena un cuadro de diálogo de autenticación de Azure que permite al usuario escribir la contraseña para completar la conexión. El nombre de usuario se pasa en la cadena de conexión.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. La autenticación de Managed Service Identity de AAD usa una identidad asignada por el sistema o asignada por el usuario para la autenticación con el fin de configurar la conexión. Para la identidad asignada por el usuario, el UID se establece en el identificador de objeto de la identidad del usuario.<br>
Para la identidad asignada por el sistema,<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
Para la identidad asignada por el usuario con el ID. de objeto igual a myObjectId,<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- Al usar las nuevas opciones de Active Directory con el controlador ODBC de Windows, asegúrese de que se ha instalado el [biblioteca de autenticación de Active Directory para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) . Al usar los controladores de Linux y MacOS, asegúrese `libcurl` de que se ha instalado. En el caso de la versión de controlador 17,2 y versiones posteriores, esta no es una dependencia explícita, ya que no es necesaria para los otros métodos de autenticación u operaciones de ODBC.
>- Para conectarse con un nombre de usuario y una contraseña de la cuenta de SQL Server, `SqlPassword` ahora puede usar la opción nueva, que se recomienda especialmente para SQL Azure ya que esta opción permite valores predeterminados de conexión más seguros.
>- Para conectarse con un nombre de usuario y una contraseña de `Authentication=ActiveDirectoryPassword` la cuenta de Azure Active Directory, especifique `UID` en `PWD` la cadena de conexión y las palabras clave y con el nombre de usuario y la contraseña, respectivamente.
>- Para conectarse con la autenticación de Windows integrada o Active Directory integrada (solo Windows Driver) `Authentication=ActiveDirectoryIntegrated` , especifique en la cadena de conexión. El controlador elegirá automáticamente el modo de autenticación correcto. `UID`y `PWD` no deben especificarse.
>- Para conectarse con Active Directory autenticación interactiva (solo con el controlador `UID` de Windows), debe especificarse.

## <a name="authenticating-with-an-access-token"></a>Autenticación con un token de acceso

El `SQL_COPT_SS_ACCESS_TOKEN` atributo anterior a la conexión permite el uso de un token de acceso Obtenido de Azure ad para la autenticación en lugar de un nombre de usuario y una contraseña, y también omite la negociación y la obtención de un token de acceso por el controlador. Para usar un token de acceso, establezca `SQL_COPT_SS_ACCESS_TOKEN` el atributo de conexión en un puntero `ACCESSTOKEN` a una estructura:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

Es una estructura de longitud variable que se compone de una _longitud_ de 4 bytes seguida de bytes de _longitud_ de datos opacos que forman el token de acceso. `ACCESSTOKEN` Debido a la forma en que SQL Server controla los tokens de acceso, se debe expandir uno obtenido a través de una respuesta JSON de [OAuth 2,0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) para que cada byte vaya seguido de un byte 0 de relleno, similar a una cadena UCS-2 que contiene solo caracteres ASCII; sin embargo, el token es un valor opaco y la longitud especificada, en bytes, no debe incluir ningún terminador null. Debido a sus considerables restricciones de longitud y formato, este método de autenticación solo está disponible mediante programación a través `SQL_COPT_SS_ACCESS_TOKEN` del atributo de conexión; no hay ninguna palabra clave de cadena de conexión o DSN correspondiente. La cadena de conexión no debe `UID`contener `PWD`palabras `Authentication`clave, `Trusted_Connection` , o.

> [!NOTE]
> La versión 13,1 del controlador ODBC solo admite esta autenticación en _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Código de ejemplo de autenticación de Azure Active Directory

En el ejemplo siguiente se muestra el código necesario para conectarse a SQL Server mediante Azure Active Directory con palabras clave de conexión. Tenga en cuenta que no es necesario cambiar el propio código de aplicación; la cadena de conexión, o DSN si se usa una, es la única modificación necesaria para usar AAD para la autenticación:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
En el ejemplo siguiente se muestra el código necesario para conectarse a SQL Server mediante Azure Active Directory con autenticación de token de acceso. En este caso, es necesario modificar el código de aplicación para procesar el token de acceso y establecer el atributo de conexión asociado.
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
A continuación se muestra una cadena de conexión de ejemplo para su uso con la autenticación de Azure Active Directory Managed Service Identity. Tenga en cuenta que el UID se establece en el identificador de objeto de la identidad del usuario para la identidad asignada por el usuario.
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>Consulte también
[Compatibilidad con la autenticación basada en tokens para Azure SQL DB mediante Azure AD auth](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

