---
title: Con Azure Active Directory con el controlador ODBC | Documentos de Microsoft para SQL Server
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78c4e00a640da21079aebf0c4247b68f3237c25
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Con Azure Active Directory con el controlador ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Finalidad

Microsoft ODBC Driver for SQL Server con la versión 13.1 o una versión posterior permite a las aplicaciones de ODBC para conectarse a una instancia de SQL Azure con una identidad federada en Azure Active Directory con un nombre de usuario y una contraseña, un token de acceso de Azure Active Directory o Windows La autenticación integrada (_sólo el controlador Windows_). Para el controlador ODBC versión 13.1, el acceso de Azure Active Directory es la autenticación de token _sólo Windows_. La versión 17 y 17.1 Cuervo de ODBC admiten esta autenticación en todas las plataformas (Windows, Linux y Mac). Se introdujo una nueva autenticación interactiva de Azure Active Directory con el Id. de inicio de sesión en el controlador ODBC versión 17.1 para Windows. Todos ellos se llevan a cabo mediante el uso de nuevo DSN y palabras clave de cadena de conexión y atributos de conexión.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>DSN nuevo o modificado y palabras clave de cadena de conexión

El `Authentication` palabra clave puede utilizarse cuando se conecta con una cadena de conexión o DSN para controlar el modo de autenticación. El valor establecido en la cadena de conexión invalidaciones en el DSN, si se proporciona. El _previamente el valor de atributo_ de la `Authentication` configuración es el valor que se calcula a partir de la cadena de conexión y valores DSN.

|Nombre|Valores|Predeterminado|Description|
|-|-|-|-|
|`Authentication`|(no establecido), (cadena vacía), `SqlPassword`, `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`|(sin establecer)|Controla el modo de autenticación.<table><tr><th>Value<th>Description<tr><td>(sin establecer)<td>Modo de autenticación determinado por otras palabras clave (opciones de conexión antiguos existentes).<tr><td>(cadena vacía)<td>(Solo la cadena de conexión.) Invalidar y sin establecer un `Authentication` valor establecido en el DSN.<tr><td>`SqlPassword`<td>Autenticar directamente a una instancia de SQL Server mediante un nombre de usuario y una contraseña.<tr><td>`ActiveDirectoryPassword`<td>Autenticar con una identidad de Azure Active Directory con un nombre de usuario y contraseña.<tr><td>`ActiveDirectoryIntegrated`<td>_Sólo el controlador Windows_. Autenticar con una identidad de Azure Active Directory mediante la autenticación integrada.<tr><td>`ActiveDirectoryInteractive`<td>_Sólo el controlador Windows_. Autenticar con una identidad de Azure Active Directory mediante la autenticación interactiva.</table>|
|`Encrypt`|(no establecido), `Yes`, `No`|(vea la descripción)|Controla el cifrado de una conexión. Si el valor del atributo anterior de la `Authentication` configuración no está _ninguno_, el valor predeterminado es `Yes`. En caso contrario, el valor predeterminado es `No`. El valor del atributo preliminar de cifrado es `Yes` si el valor se establece en `Yes` en la cadena de conexión o DSN.|

## <a name="new-andor-modified-connection-attributes"></a>Atributos de conexión nueva o modificada

Lo siguiente antes de conectar conexión atributos se han introducido o modificado para admitir la autenticación de Azure Active Directory. Cuando un atributo de conexión tiene una cadena de conexión correspondiente o la palabra clave DSN y se establece, el atributo de conexión tiene prioridad.

|Atributo|Tipo|Valores|Predeterminado|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_RESET`|(sin establecer)|Consulte la descripción de `Authentication` palabra clave anterior. `SQL_AU_NONE` se proporciona con el fin de reemplazar explícitamente un conjunto `Authentication` valor en la cadena de conexión o de DSN, mientras que `SQL_AU_RESET` unsets el atributo si ya se ha establecido, permitiendo que el valor de cadena de conexión o DSN tendrá prioridad.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Puntero a `ACCESSTOKEN` o NULL|NULL|Si no es null, especifica el Token de acceso de la organización a usar. Es un error especificar un token de acceso y también `UID`, `PWD`, `Trusted_Connection`, o `Authentication` palabras clave de cadena de conexión o sus atributos equivalente. <br> **Nota:** ODBC Driver 13.1 versión solo se admite esto en _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(vea la descripción)|Controla el cifrado de una conexión. `SQL_EN_OFF` y `SQL_EN_ON` deshabilitar y habilitar el cifrado, respectivamente. Si el valor del atributo anterior de la `Authentication` configuración no está _ninguno_ o `SQL_COPT_SS_ACCESS_TOKEN` está establecida, y `Encrypt` no se especificó en la cadena de la conexión o de DSN, el valor predeterminado es `SQL_EN_ON`. En caso contrario, el valor predeterminado es `SQL_EN_OFF`. El valor efectivo de este atributo controla [si se usará el cifrado para la conexión.](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|No se admite con Azure Active Directory, puesto que los cambios de contraseña a entidades de seguridad AAD no se puede lograr a través de una conexión ODBC. <br><br>Expiración de contraseña para la autenticación de SQL Server se introdujo en SQL Server 2005. El `SQL_COPT_SS_OLDPWD` atributo se agregó para permitir que el cliente proporcionar la antigua y la nueva contraseña para la conexión. Cuando se establezca esta propiedad, el proveedor no usará el grupo de conexiones para la primera conexión o para conexiones posteriores, puesto que la cadena de conexión contendrá la "contraseña antigua" que ahora ha cambiado.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_En desuso_; use `SQL_COPT_SS_AUTHENTICATION` establecido en `SQL_AU_AD_INTEGRATED` en su lugar. <br><br>Fuerza el uso de autenticación de Windows (Kerberos en Linux y Mac OS) para la validación de acceso de inicio de sesión de servidor. Cuando se usa la autenticación de Windows, el controlador omite los valores de identificador y la contraseña de usuario proporcionados como parte de `SQLConnect`, `SQLDriverConnect`, o `SQLBrowseConnect` de procesamiento.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Adiciones de interfaz de usuario para Azure Active Directory (solo controladores de Windows)

La conexión de interfaces de usuario del controlador y el programa de instalación DSN se han mejorado con las opciones adicionales necesarias para usar la autenticación con Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Creación y edición de DSN en la interfaz de usuario

Es posible usar el nuevo Azure AD de opciones de autenticación al crear o editar un DSN existente mediante el programa de instalación del controlador en la interfaz de usuario:

`Authentication=ActiveDirectoryIntegrated` para la autenticación de Azure Active Directory integrado en SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` para la autenticación de usuario y la contraseña de Azure Active Directory para SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` para la autenticación interactiva de Azure Active Directory para SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` para la autenticación de usuario y la contraseña para SQL Server (de Azure o de otra manera)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` para Windows SSPI heredado autenticación integrada

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

Las cinco opciones corresponden a `Trusted_Connection=Yes` (heredado de Windows existentes solo SSPI la autenticación integrada) y `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, `ActiveDirectoryPassword`, y `ActiveDirectoryInteractive`, respectivamente.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>Símbolo del sistema de SQLDriverConnect (sólo controladores de Windows)

El cuadro de diálogo muestra SQLDriverConnect cuando solicita la información necesaria para completar la conexión contiene tres nuevas opciones para la autenticación de Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Estas opciones corresponden a los mismos cinco disponibles en la configuración DSN anterior de la interfaz de usuario.

### <a name="example-connection-strings"></a>Ejemplos de cadena de conexión
1. Autenticación de SQL Server: sintaxis heredada. No se valida el certificado de servidor y se usa el cifrado solo si el servidor lo aplica. El nombre de usuario y la contraseña se pasa en la cadena de conexión.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticación de SQL: nueva sintaxis. El cliente solicita cifrado (el valor predeterminado de `Encrypt` es `true`) y el certificado de servidor obtiene validado, independientemente de la configuración de cifrado (a menos que `TrustServerCertificate` está establecido en `true`). El nombre de usuario y la contraseña se pasa en la cadena de conexión.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticación integrada de Windows (Kerberos en Linux y Mac OS) utilizando SSPI (para SQL Server o SQL IaaS) sintaxis actual. No se valida el certificado de servidor, a menos que se usa el cifrado. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Sólo el controlador Windows_.) Autenticación integrada de Windows utilizando SSPI (si la base de datos de destino está en SQL Server o SQL IaaS) – nueva sintaxis. El cliente solicita cifrado (el valor predeterminado de `Encrypt` es `true`) y el certificado de servidor obtiene validado, independientemente de la configuración de cifrado (a menos que `TrustServerCertificate` está establecido en `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticación de usuario y la contraseña de AAD (si la base de datos de destino está en la base de datos de SQL Azure). Se valida el certificado de servidor, independientemente de la configuración de cifrado (a menos que `TrustServerCertificate` está establecido en `true`). El nombre de usuario y la contraseña se pasa en la cadena de conexión. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Sólo el controlador Windows_.) Autenticación integrada de Windows usa ADAL, lo que implica canjeando credenciales de la cuenta de Windows para un token de acceso de AAD emitido, suponiendo que la base de datos de destino está en la base de datos de SQL Azure. Se valida el certificado de servidor, independientemente de la configuración de cifrado (a menos que `TrustServerCertificate` está establecido en `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Sólo el controlador Windows_.) Autenticación de AAD interactiva usa tecnología de autenticación multifactor de Azure para configurar una conexión. En este modo, proporcionando el identificador de inicio de sesión, un cuadro de diálogo de autenticación de Windows Azure se activa y permite al usuario que escriba la contraseña para completar la conexión. El nombre de usuario se pasa en la cadena de conexión.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

> [!NOTE] 
>- Al utilizar las nuevas opciones de Active Directory con el controlador ODBC de Windows, asegúrese de que el [biblioteca de autenticación de Active Directory para SQL Server](http://go.microsoft.com/fwlink/?LinkID=513072) se ha instalado. Los controladores de Linux y Mac OS no necesitan las dependencias adicionales para autenticar con Azure Active Directory.
>- Para conectarse mediante un nombre de usuario de cuenta de SQL Server y una contraseña, ahora puede usar el nuevo `SqlPassword` opción, que se recomienda especialmente para SQL Azure, ya que esta opción permite que los valores predeterminados de conexión más seguros.
>- Para conectarse con un nombre de usuario de cuenta de Azure Active Directory y la contraseña, especifique `Authentication=ActiveDirectoryPassword` en la cadena de conexión y la `UID` y `PWD` palabras clave con el nombre de usuario y contraseña, respectivamente.
>- Para conectarse utilizando la autenticación integrada en Active Directory (solo controladores de Windows) o integrada de Windows, especifique `Authentication=ActiveDirectoryIntegrated` en la cadena de conexión. El controlador elegirá el modo de autenticación correcto automáticamente. `UID` y `PWD` no se debe especificar.
>- Para conectarse mediante la autenticación de Active Directory interactiva (sólo controladores de Windows), `UID` debe especificarse.

## <a name="authenticating-with-an-access-token"></a>Autenticar con un Token de acceso

El `SQL_COPT_SS_ACCESS_TOKEN` atributo anterior a la conexión permite el uso de un token de acceso obtenido de Azure AD para la autenticación en lugar del nombre de usuario y contraseña y también omite la negociación y la obtención de un token de acceso con el controlador. Para usar un token de acceso, establezca el `SQL_COPT_SS_ACCESS_TOKEN` atributo de conexión a un puntero a un `ACCESSTOKEN` estructura:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

El `ACCESSTOKEN` es una estructura de longitud variable que se compone de 4 bytes _longitud_ seguido _longitud_ bytes de datos opacos que forman el token de acceso. Debido a cómo SQL Server trata los tokens de acceso, una obtenidas a través de un [OAuth 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios) respuesta JSON debe ampliarse para que cada byte va seguido de un byte, similar a una cadena de UCS-2 que contiene únicamente caracteres ASCII de relleno de 0; sin embargo, el token es un valor opaco y la longitud especificada, en bytes, no deben incluir cualquier carácter nulo de terminación. Debido a sus restricciones de longitud y el formato considerables, este método de autenticación sólo está disponible mediante programación a través de la `SQL_COPT_SS_ACCESS_TOKEN` coonnection atributo; no hay ningún DSN correspondiente o la palabra clave de cadena de conexión. No debe contener la cadena de conexión `UID`, `PWD`, `Authentication`, o `Trusted_Connection` palabras clave.

> [!NOTE]
> El controlador ODBC versión 13.1 solo se admite la autenticación en _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Código de ejemplo de autenticación de Azure Active Directory

El ejemplo siguiente muestra el código necesario para conectarse a SQL Server con Azure Active Directory con las palabras clave de conexión. Tenga en cuenta que no es necesario cambiar el código de la aplicación; la cadena de conexión o DSN si se usa alguno, es la única modificación necesarios cuando se usa de AAD para la autenticación:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
El ejemplo siguiente muestra el código necesario para conectarse a SQL Server con Azure Active Directory con la autenticación de token de acceso. En este caso, es necesario modificar el código de la aplicación para procesar el token de acceso y establezca el atributo de conexión asociada.
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
La siguiente es una cadena de conexión de ejemplo para su uso con autenticación interactiva de Azure Active Directory. Tenga en cuenta que no contiene campos PWD tal y como se insertaría la contraseña usando la autenticación de Windows Azure de la pantalla.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~

## <a name="see-also"></a>Vea también
[Compatibilidad con la autenticación basada en autorización token de base de datos de SQL de Azure con autenticación de Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

