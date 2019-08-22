---
title: Conexión mediante autenticación de Azure Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b596936010fcdce4eb5c0701c5f0c6631cd9687e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028121"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conexión mediante autenticación de Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se proporciona información sobre cómo desarrollar aplicaciones de Java para usar la característica de autenticación de Azure Active Directory con Microsoft JDBC driver para SQL Server.

Puede usar la autenticación Azure Active Directory (AAD), que es un mecanismo de conexión a Azure SQL Database V12 mediante identidades en Azure Active Directory. Use la autenticación de Azure Active Directory para administrar identidades de usuarios de base de datos de forma centralizada y como alternativa a la autenticación de SQL Server. El controlador JDBC le permite especificar las credenciales de Azure Active Directory en la cadena de conexión de JDBC para conectarse a Azure SQL DB. Para obtener información sobre cómo configurar la autenticación de Azure Active Directory [, visite conexión a SQL Database mediante el uso de Azure Active Directory autenticación](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Las propiedades de conexión para admitir la autenticación Azure Active Directory en Microsoft JDBC driver for SQL Server son las siguientes:
*   **autenticación**: Use esta propiedad para indicar el método de autenticación de SQL que se va a utilizar para la conexión. Los valores posibles son: 
    * **ActiveDirectoryMSI**
        * Compatible desde la versión de controlador **v 7.2**, `authentication=ActiveDirectoryMSI` se puede usar para conectarse a un almacenamiento de datos de Azure SQL Database/desde dentro de un recurso de Azure con la compatibilidad de "identidad" habilitada. Opcionalmente, **msiClientId** también se puede especificar en las propiedades Connection/DataSource junto con este modo de autenticación, que debe contener el identificador de cliente de una Managed Service Identity que se usará para adquirir el **accessToken** para establecer la conexión.
    * **ActiveDirectoryIntegrated**
        * Compatible desde la versión de controlador **v 6.0**, `authentication=ActiveDirectoryIntegrated` se puede usar para conectarse a un almacenamiento de datos de Azure SQL Database/mediante la autenticación integrada. Para usar este modo de autenticación, debe federar el Servicios de federación de Active Directory (AD FS) local (ADFS) con Azure Active Directory en la nube. Una vez configurado, puede conectarse agregando la biblioteca nativa ' sqljdbc_auth. dll ' a la ruta de acceso de clase de aplicación en el sistema operativo Windows o configurando un vale de Kerberos para la compatibilidad con la autenticación multiplataforma. Podrá acceder a Azure SQL DB/DW sin que se le soliciten las credenciales cuando haya iniciado sesión en una máquina unida a un dominio.
    * **ActiveDirectoryPassword**
        * Compatible desde la versión de controlador **v 6.0**, `authentication=ActiveDirectoryPassword` se puede usar para conectarse a un almacenamiento de Azure SQL Database/datos con un nombre de entidad de seguridad Azure ad y una contraseña.
    * **SqlPassword**
        * Utilice `authentication=SqlPassword` para conectarse a un SQL Server mediante las propiedades de nombre de usuario y contraseña.
    * **NotSpecified**
        * Use `authentication=NotSpecified` o déjela como valor predeterminado cuando no se necesite ninguno de estos métodos de autenticación.

*   **accessToken**: Use esta propiedad de conexión para conectarse a un SQL Database mediante un token de acceso. accessToken solo se puede establecer mediante el parámetro Properties del método getConnection () en la clase DriverManager. No se puede usar en la dirección URL de conexión.  

Para obtener más información, consulte la propiedad Authentication en la página [establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) .  


## <a name="client-setup-requirements"></a>Requisitos de instalación de cliente
Para la autenticación **ActiveDirectoryMSI** , se deben instalar los componentes siguientes en el equipo cliente:
* Java 8 o posterior
* Microsoft JDBC driver 7,2 (o posterior) para SQL Server
* El entorno de cliente debe ser un recurso de Azure y debe tener habilitada la característica de "identidad".
* Un usuario de base de datos independiente que representa la identidad administrada asignada por el sistema de su recurso de Azure o una identidad administrada asignada por el usuario, o uno de los grupos a los que pertenece su MSI, debe existir en la base de datos de destino y debe tener el permiso CONNECT.

En el caso de otros modos de autenticación, se deben instalar los componentes siguientes en el equipo cliente:
* Java 7 o superior
* Microsoft JDBC driver 6,0 (o posterior) para SQL Server
* Si usa el modo de autenticación basada en tokens de acceso, necesita [Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias para ejecutar los ejemplos de este artículo. Para obtener más información, consulte la sección **conectarse mediante el token de acceso** .
* Si usa el modo de autenticación **ActiveDirectoryPassword** , necesita [Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias. Para obtener más información, consulte la sección **conectarse mediante el modo de autenticación ActiveDirectoryPassword** .
* Si usa el modo **ActiveDirectoryIntegrated** , necesita Azure-ActiveDirectory-Library-for-Java y sus dependencias. Para obtener más información, consulte la sección **conectarse mediante el modo de autenticación ActiveDirectoryIntegrated** .

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>Conexión mediante el modo de autenticación ActiveDirectoryMSI
En el siguiente ejemplo se muestra cómo usar el modo `authentication=ActiveDirectoryMSI`. Ejecute este ejemplo desde dentro de un recurso de Azure, e, g una máquina virtual de Azure, App Service o un Function App que esté federado con Azure Active Directory.

Reemplace el nombre del servidor o la base de datos por el nombre del servidor o la base de datos en las líneas siguientes antes de ejecutar el ejemplo:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

El ejemplo para usar el modo de autenticación de ActiveDirectoryMSI:

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Al ejecutar este ejemplo en una máquina virtual de Azure, se obtiene un token de acceso de identidad administrada asignada por el _sistema_ o _identidad administrada asignada_ por el usuario (si se especifica **msiClientId** ) y se establece una conexión con el acceso recuperado. muestras. Si se establece una conexión, debería ver el mensaje siguiente:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Conexión mediante el modo de autenticación ActiveDirectoryIntegrated
Con la versión 6,4, Microsoft JDBC driver agrega compatibilidad con la autenticación ActiveDirectoryIntegrated mediante un vale de Kerberos en varias plataformas (Windows, Linux y macOS).
Para obtener más información, consulte [establecer vale Kerberos en Windows, Linux y Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) . Como alternativa, en Windows, sqljdbc_auth. dll también se puede usar para la autenticación de ActiveDirectoryIntegrated con el controlador JDBC.

> [!NOTE]
>  Si usa una versión anterior del controlador, consulte este [vínculo](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) para las dependencias respectivas que se requieren para usar este modo de autenticación. 

En el siguiente ejemplo se muestra cómo usar el modo `authentication=ActiveDirectoryIntegrated`. Ejecute este ejemplo en un equipo unido a un dominio que esté federado con Azure Active Directory. Debe existir en la base de datos un usuario de base de datos independiente que represente a la entidad de seguridad de Azure AD, o uno de los grupos a los que pertenece, y debe tener el permiso CONNECT. 

Antes de compilar y ejecutar el ejemplo, en el equipo cliente (en el que desea ejecutar el ejemplo), descargue la [biblioteca Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias e inclúyalo en la ruta de acceso de compilación de Java.

Reemplace el nombre del servidor o la base de datos por el nombre del servidor o la base de datos en las líneas siguientes antes de ejecutar el ejemplo:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

El ejemplo para usar el modo de autenticación de ActiveDirectoryIntegrated:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Al ejecutar este ejemplo en un equipo cliente, se usa automáticamente el vale de Kerberos y no se requiere ninguna contraseña. Si se establece una conexión, debería ver el mensaje siguiente:

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Establecimiento del vale Kerberos en Windows, Linux y Mac

Debe configurar un vale de Kerberos que vincule el usuario actual a una cuenta de dominio de Windows. A continuación se incluye un resumen de los pasos clave.

#### <a name="windows"></a>Windows
JDK incluye `kinit`, que se puede usar para obtener un TGT de centro de distribución de claves (KDC) en un equipo unido a un dominio que está federado con Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Paso 1: recuperación de vales de concesión de vales
- **Ejecutar en**: Windows
- **Acción**:
  - Use el comando `kinit username@DOMAIN.COMPANY.COM` para obtener un TGT de KDC y, a continuación, le pedirá la contraseña del dominio.
  - Use `klist` para ver los vales disponibles. Si el kinit se realizó correctamente, debería ver un vale de krbtgt/dominio. COMPANY. COM @ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Es posible que tenga que especificar `.ini` un archivo `-Djava.security.krb5.conf` con para que la aplicación busque KDC.

#### <a name="linux-and-mac"></a>Linux y Mac

##### <a name="requirements"></a>Requisitos
Acceso a un equipo Windows unido a dominio para consultar el controlador de dominio de Kerberos.

##### <a name="step-1-find-kerberos-kdc"></a>Paso 1: buscar el KDC de Kerberos
- **Ejecutar en**: línea de comandos de Windows
- **Acción**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (donde "domain.Company.com" se asigna al nombre del dominio)
- **Salida del ejemplo**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Información que se va a extraer** Nombre del controlador de dominio, en este caso`co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Paso 2: configuración de KDC en krb5. conf
- **Ejecutar en**: Linux/Mac
- **Acción**: edite/etc/krb5.conf en el editor que prefiera. Configure las claves siguientes
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  Luego, guarde el archivo krb5.conf y salga.

> [!NOTE]
>  El dominio debe estar en MAYÚSCULAS.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Paso 3: Probar la recuperación de un vale de concesión de vales
- **Ejecutar en**: Linux/Mac
- **Acción**:
  - Use el comando `kinit username@DOMAIN.COMPANY.COM` para obtener un TGT de KDC y, a continuación, le pedirá la contraseña del dominio.
  - Use `klist` para ver los vales disponibles. Si el kinit se realizó correctamente, debería ver un vale de krbtgt/dominio. COMPANY. COM @ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Conexión mediante el modo de autenticación ActiveDirectoryPassword
En el siguiente ejemplo se muestra cómo usar el modo `authentication=ActiveDirectoryPassword`.

Antes de compilar y ejecutar el ejemplo:
1.  En el equipo cliente (en el que desea ejecutar el ejemplo), descargue la [biblioteca Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias e inclúyalo en la ruta de acceso de compilación de Java.
2.  Busque las siguientes líneas de código y reemplace el nombre del servidor o la base de datos por el nombre del servidor o la base de datos.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Busque las siguientes líneas de código y reemplace nombre de usuario por el nombre del usuario de AAD al que desea conectarse.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

El ejemplo para usar el modo de autenticación de ActiveDirectoryPassword:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
Si se establece la conexión, debería ver el siguiente mensaje como salida:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Debe existir una base de datos de usuario independiente y un usuario de base de datos independiente que represente al usuario Azure AD especificado o a uno de los grupos, el Azure AD usuario especificado pertenece a, debe existir en la base de datos y debe tener el permiso CONNECT (excepto Azure Active Directory Grupo o administrador del servidor)

## <a name="connecting-using-access-token"></a>Conexión mediante el token de acceso
Las aplicaciones y los servicios pueden recuperar un token de acceso del Azure Active Directory y usarlo para conectarse a Azure SQL Database/almacenamiento de datos.

> [!NOTE] 
> **accessToken** solo se puede establecer mediante el parámetro Properties del método getConnection () en la clase DriverManager. No se puede usar en la cadena de conexión.

El ejemplo siguiente contiene una sencilla aplicación Java que se conecta a Azure SQL Database/almacenamiento de datos mediante la autenticación basada en tokens de acceso. Antes de compilar y ejecutar el ejemplo, realice los pasos siguientes:
1.  Cree una cuenta de aplicación en Azure Active Directory para su servicio.
    1. Inicie sesión en Azure Portal.
    2. Haga clic en Azure Active Directory en el panel de navegación izquierdo.
    3. Haga clic en la pestaña "Registros de aplicaciones".
    4. En el cajón, haga clic en "nuevo registro de aplicación".
    5. Escriba mytokentest como nombre descriptivo para la aplicación, seleccione "aplicación web/API".
    6. No se necesita la dirección URL de inicio de sesión. Simplemente proporcione algo: "https://mytokentest".
    7. Haga clic en "crear" en la parte inferior.
    9. Mientras sigue en el Azure Portal, haga clic en la pestaña "configuración" de la aplicación y abra la pestaña "propiedades".
    10. Busque el valor "ID. de la aplicación" (también conocido como ID. de cliente) y cópielo, ya que lo necesitará más adelante cuando configure la aplicación (por ejemplo, 1846943b-ad04-4808-aa13-4702d908b5c1). Vea la siguiente instantánea.
    11. En la sección "claves", cree una clave rellenando el campo de nombre, seleccionando la duración de la clave y guardando la configuración (deje el campo de valor vacío). Después de guardar, el campo de valor se debe rellenar automáticamente y copiar el valor generado. Este es el secreto del cliente.
    12. Haga clic en Azure Active Directory en el panel de la izquierda. En "registros de aplicaciones", busque la pestaña "puntos finales". Copie la dirección URL en "OATH 2,0 TOKEN ENDPOINT", que es la dirección URL del STS.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Inicie sesión en la base de datos de usuario de Azure SQL Server como administrador de Azure Active Directory y use un comando T-SQL para aprovisionar un usuario de base de datos independiente para la entidad de seguridad de la aplicación. Para obtener más información, consulte [conexión a SQL Database o SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) mediante la autenticación de Azure Active Directory para obtener más detalles sobre cómo crear un administrador de Azure Active Directory y un usuario de base de datos independiente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  En el equipo cliente (en el que desea ejecutar el ejemplo), descargue la biblioteca [Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias e inclúyalo en la ruta de acceso de compilación de Java. Tenga en cuenta que Azure-ActiveDirectory-Library-for-Java solo es necesario para ejecutar este ejemplo específico. En el ejemplo se usan las API de esta biblioteca para recuperar el token de acceso de Azure AAD. Si ya tiene un token de acceso, puede omitir este paso. Tenga en cuenta que también debe quitar la sección del ejemplo que recupera el token de acceso.

En el ejemplo siguiente, reemplace la dirección URL del STS, el ID. de cliente, el secreto de cliente, el servidor y el nombre de la base de datos por sus valores.

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

Si la conexión es correcta, debería ver el siguiente mensaje como salida:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
