---
title: Conectarse mediante la autenticación de Azure Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c87e7b85282c7ca237689296e08d2b7645240ed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767143"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conectarse usando la autenticación de Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se proporciona información sobre cómo desarrollar aplicaciones de Java para usar la característica de autenticación de Azure Active Directory con Microsoft JDBC Driver 6.0 (o posterior) para SQL Server.

Puede usar la autenticación de Azure Active Directory (AAD), que es un mecanismo de conexión a Azure SQL Database v12 mediante identidades en Azure Active Directory. Use la autenticación de Azure Active Directory para administrar identidades de usuarios de base de datos de forma centralizada y como alternativa a la autenticación de SQL Server. El controlador JDBC permite especificar las credenciales de Azure Active Directory en la cadena de conexión JDBC para conectarse a Azure SQL DB. Para obtener información sobre cómo configurar la autenticación de Azure Active Directory, visite [conectarse a SQL base de datos mediante Azure Active Directory la autenticación](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Se agregaron dos nuevas propiedades de conexión para admitir la autenticación de Azure Active Directory:
*   **autenticación**: Utilice esta propiedad para indicar qué método de autenticación de SQL que se usará para la conexión. Los valores posibles son: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword**y el valor predeterminado **NotSpecified**.
    * Use "authentication = ActiveDirectoryIntegrated' para conectarse a una base de datos SQL mediante la autenticación integrada de Windows. Para usar este modo de autenticación, deberá federar la local Active Directory Federation Services (ADFS) con AAD en la nube. Una vez que se ha configurado, así como un vale de Kerberos, puede tener acceso a Azure SQL DB sin que se le pidan las credenciales cuando haya iniciado en una máquina unida al dominio. 
    * Use "authentication = ActiveDirectoryPassword" para conectarse a una base de datos de SQL con un nombre de entidad de seguridad de Azure AD y la contraseña.
    * Use "authentication = SqlPassword' para conectarse a un servidor SQL Server mediante las propiedades de usuario o nombre de usuario y contraseña.
    * Use ' autenticación = NotSpecified "o déjelo como valor predeterminado cuando se necesita ninguno de estos métodos de autenticación.

*   **accessToken**: Utilice esta propiedad para conectarse a una base de datos SQL mediante un token de acceso. accessToken solo puede establecerse mediante el parámetro de propiedades del método getConnection() en la clase DriverManager. No se puede usar en la dirección URL de conexión.  

Para obtener más información, vea la propiedad de autenticación en el [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) página.  


## <a name="client-setup-requirements"></a>Requisitos de configuración de cliente
Asegúrese de que los siguientes componentes están instalados en el equipo cliente:
* Java 7 o posterior
*   Microsoft JDBC Driver 6.0 (o posterior) para SQL Server
*   Si usa el modo de autenticación basada en token de acceso, necesitará [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias para ejecutar los ejemplos de este artículo. Para obtener más información, consulte **conectarse mediante el Token de acceso** sección.
*   Si usa el modo de autenticación ActiveDirectoryPassword, necesitará [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias. Para obtener más información, consulte **conectarse mediante el modo de autenticación ActiveDirectoryPassword** sección.
*   Si usa el modo ActiveDirectoryIntegrated, necesita azure-activedirectory-library-for-java y sus dependencias. Para obtener más información, consulte **conectarse utilizando el modo de autenticación ActiveDirectoryIntegrated** sección.
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Conectando con el modo de autenticación ActiveDirectoryIntegrated
 Con la versión 6.4, Microsoft JDBC Driver agrega compatibilidad con la autenticación de ActiveDirectoryIntegrated con un vale de Kerberos en varias plataformas (Windows/Linux y Mac).
Para obtener más información, consulte [vale de Kerberos establecido en Windows, Linux y Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) para obtener más detalles. Como alternativa, en Windows, sqljdbc_auth.dll también se pueden usar para la autenticación de ActiveDirectoryIntegrated con el controlador JDBC.

> [!NOTE]
>  Active esta opción si usa una versión anterior del controlador, [vínculo](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) para las dependencias correspondientes que son necesarios para usar este modo de autenticación. 

El ejemplo siguiente muestra cómo usar "authentication = ActiveDirectoryIntegrated' modo. En este ejemplo se ejecute en una máquina unida al dominio que está federada con Azure Active Directory. Un usuario de base de datos independiente que representa la entidad de seguridad de Azure AD, o uno de los grupos, pertenece a, debe existir en la base de datos y debe tener el permiso CONNECT. 

Antes de compilar y ejecutar el ejemplo, en el equipo cliente (en el que, para ejecutar el ejemplo), descargue el [biblioteca azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias e incluirlos en la ruta de acceso de compilación de Java

Antes de ejecutar el ejemplo, reemplace el nombre de servidor y base de datos con el nombre del servidor y base de datos en las siguientes líneas:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

El ejemplo para usar el modo de autenticación ActiveDirectoryIntegrated:
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
        ds.setHostNameInCertificate("*.database.windows.net");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {
            
            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
Ejecutar este ejemplo en un equipo cliente automáticamente usa el vale de Kerberos y no se requiere contraseña. Si se establece una conexión, debería ver el mensaje siguiente:
```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Establecer el vale de Kerberos en Windows, Linux y Mac

Deberá configurar un vale de Kerberos del usuario actual de vinculación a una cuenta de dominio de Windows. A continuación se incluye un resumen de los pasos clave.

#### <a name="windows"></a>Windows
JDK viene con `kinit`, que puede usar para obtener un vale desde el centro de distribución de claves (KDC) en un dominio Unidos a un equipo que está federado con Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Paso 1: Recuperación de vale de concesión de vales
- **Ejecutar en**: Windows
- **Acción**:
  - Use el comando `kinit username@DOMAIN.COMPANY.COM` para obtener un TGT de KDC, a continuación, se le pedirá que la contraseña de dominio.
  - Use `klist` para ver los vales disponibles. Si el kinit se realizó correctamente, debería ver un vale de krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Es posible que deba especificar un `.ini` de archivos con `-Djava.security.krb5.conf` para su aplicación buscar el KDC.

#### <a name="linux-and-mac"></a>Linux y Mac

##### <a name="requirements"></a>Requisitos
Acceso a un equipo unido al dominio de Windows para consultar el controlador de dominio Kerberos.

##### <a name="step-1-find-kerberos-kdc"></a>Paso 1: Búsqueda de KDC de Kerberos
- **Ejecutar en**: línea de comandos de Windows
- **Acción**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (donde "DOMAIN.COMPANY.COM" se asigna a su nombre de dominio)
- **Salida del ejemplo**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Información para extraer** el nombre de controlador, en este caso `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Paso 2: Configuración del KDC en krb5.conf
- **Ejecutar en**: Linux/Mac
- **Acción**: editar el /etc/krb5.conf en un editor que prefiera. Configure las claves siguientes
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  A continuación, guarde el archivo krb5.conf y salir

> [!NOTE]
>  Dominio debe estar en mayúsculas.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Paso 3: Probar la recuperación de vale de concesión de vales
- **Ejecutar en**: Linux/Mac
- **Acción**:
  - Use el comando `kinit username@DOMAIN.COMPANY.COM` para obtener un TGT de KDC, a continuación, se le pedirá que la contraseña de dominio.
  - Use `klist` para ver los vales disponibles. Si el kinit se realizó correctamente, debería ver un vale de krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Conectar con el modo de autenticación ActiveDirectoryPassword
El ejemplo siguiente muestra cómo usar "authentication = ActiveDirectoryPassword" modo.

Antes de compilar y ejecutar el ejemplo:
1.  En el equipo cliente (en el que, para ejecutar el ejemplo), descargue el [biblioteca azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias e incluirlos en la ruta de acceso de compilación de Java
2.  Busque las siguientes líneas de código y reemplace el nombre de servidor y base de datos con el nombre de servidor y base de datos.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Busque las siguientes líneas de código y reemplace el nombre de usuario, con el nombre del usuario AAD que desea conectarse como.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

El ejemplo para usar el modo de autenticación ActiveDirectoryPassword:
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
        ds.setHostNameInCertificate("*.database.windows.net");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {
            
            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
Si se establece la conexión, verá el siguiente mensaje como salida:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Debe existir una base de datos de usuario contenido y un usuario de base de datos independiente que representa el usuario de Azure AD o uno de los grupos de Azure especificado pertenece al usuario de AD, debe existir en la base de datos y debe tener el permiso CONNECT (excepto Azure Active Directory Administrador del servidor o grupo)

## <a name="connecting-using-access-token"></a>Conectar con el Token de acceso
Aplicaciones y servicios puede recuperar un token de acceso de Azure Active Directory y usarlo para conectarse a la base de datos de SQL Azure.

> [!NOTE] 
> **accessToken** solo puede establecerse mediante el parámetro de propiedades del método getConnection() en la clase DriverManager. No se puede usar en la cadena de conexión.

El ejemplo siguiente contiene una sencilla aplicación Java que se conecta a Azure SQL Database mediante la autenticación basada en token de acceso. Antes de compilar y ejecutar el ejemplo, realice los pasos siguientes:
1.  Crear una cuenta de la aplicación en Azure Active Directory para el servicio.
    1. Inicie sesión en Azure Portal.
    2. En el panel de navegación izquierdo, haga clic en Azure Active Directory.
    3. Haga clic en la pestaña "Registros de aplicación".
    4. En el cajón, haga clic en "Nuevo registro de aplicaciones".
    5. Escriba mytokentest como un nombre descriptivo para la aplicación, seleccione "aplicación Web o API".
    6. No necesitamos dirección URL de inicio de sesión. Basta con que proporcione cualquier cosa: "http://mytokentest".
    7. En la parte inferior, haga clic en "Crear".
    9. Mientras sigue en Azure portal, haga clic en la pestaña "Configuración" de la aplicación y abra la pestaña "Propiedades".
    10. Busque el valor "Id. de aplicación" (también conocido como Id. de cliente) y cópielo aparte, necesitará más adelante cuando configure la aplicación (por ejemplo, 1846943b-ad04-4808-aa13-4702d908b5c1). Consulte la siguiente instantánea.
    11. En la sección "Claves", cree una clave rellenando el campo nombre, seleccione la duración de la clave y guardar la configuración (deje vacío el campo de valor). Después de guardar, el campo de valor debe estar rellena automáticamente, copie el valor generado. Este es el secreto del cliente.
    12. En el panel izquierdo, haga clic en Azure Active Directory. En "Registros de aplicaciones", busque la pestaña "Puntos de conexión". Copie la dirección URL en "OATH 2.0 TOKEN ENDPOINT", se trata de la URL de STS.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Inicie sesión en base de datos de usuario del servidor de SQL Azure como un administrador de Azure Active Directory y utilizando una provisión de comando de T-SQL, un usuario de base de datos independiente para la aplicación principal. Para obtener más información, consulte el [conectarse a SQL Database o SQL Data Warehouse por usar Azure Active Directory autenticación](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) para obtener más información sobre cómo crear un administrador de Azure Active Directory y un usuario de base de datos independiente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  En el equipo cliente (en el que, para ejecutar el ejemplo), descargue el [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) biblioteca y sus dependencias e incluirlos en la ruta de acceso de compilación de Java. Tenga en cuenta que la azure-activedirectory-library-for-java solo es necesario para ejecutar este ejemplo concreto. El ejemplo usa las API de esta biblioteca para recuperar el token de acceso de Azure AAD. Si ya tiene un token de acceso, puede omitir este paso. Tenga en cuenta que también deba quitar la sección en el ejemplo que recupera el token de acceso.

En el ejemplo siguiente, reemplace el nombre de la URL de STS, Id. de cliente, secreto de cliente, servidor y base de datos con sus valores.

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
        ds.setHostNameInCertificate("*.database.windows.net");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {

            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

Si la conexión se realiza correctamente, verá el siguiente mensaje como salida:
```java
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
