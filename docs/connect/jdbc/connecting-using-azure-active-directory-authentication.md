---
title: Conectarse usando la autenticación de Active Directory de Azure | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.technology:
- drivers
ms.topic: article
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ed4b2623b7a80358622b8153d316428b742ef31e
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conectarse usando la autenticación de Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se proporciona información sobre cómo desarrollar aplicaciones de Java para usar la característica de autenticación de Azure Active Directory con Microsoft JDBC Driver 6.0 (o superior) para SQL Server.

Puede utilizar la autenticación de Azure Active Directory (AAD), que es un mecanismo de conectarse a la base de datos de SQL Azure v12 mediante identidades de Azure Active Directory. Utilizar autenticación de Azure Active Directory para administrar de forma centralizada las identidades de usuarios de base de datos y como una alternativa a la autenticación de SQL Server. El controlador JDBC permite especificar sus credenciales de Azure Active Directory en la cadena de conexión de JDBC para conectarse a la base de datos de SQL Azure. Para obtener información sobre cómo configurar la autenticación de Active Directory de Azure, visite [conectarse a SQL base de datos mediante Azure Active Directory autenticación](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Dos nuevas propiedades de conexión que se han agregado para admitir la autenticación de Azure Active Directory:
*   **autenticación**: Utilice esta propiedad para indicar qué método de autenticación de SQL que se utilizará para la conexión. Los valores posibles son: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword**y el valor predeterminado **NotSpecified**.
    * Use ' autenticación = ActiveDirectoryIntegrated' para conectarse a una base de datos de SQL mediante la autenticación integrada de Windows. Para usar este modo de autenticación, debe federar la local Active Directory Federation Services (ADFS) con Azure AD en la nube. Una vez que está configurado, así como un vale de Kerberos, puede tener acceso a base de datos de SQL Azure sin que se le pidan las credenciales cuando se registran en un equipo unido a dominio. 
    * Use ' autenticación = ActiveDirectoryPassword' para conectarse a una base de datos de SQL mediante un nombre de entidad de seguridad de Azure AD y una contraseña.
    * Use ' autenticación = SqlPassword' para conectarse a SQL Server mediante las propiedades de nombre de usuario o usuario y una contraseña.
    * Use ' autenticación = NotSpecified' o dejarlo como valor predeterminado cuando se necesita ninguno de estos métodos de autenticación.

*   **accessToken**: Utilice esta propiedad para conectarse a una base de datos SQL con un token de acceso. accessToken sólo puede establecerse mediante el parámetro Properties del método getConnection() en la clase DriverManager. No se puede utilizar en la dirección URL de conexión.  

Para obtener más información, consulte la propiedad de autenticación en el [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) página.  


## <a name="client-setup-requirements"></a>Requisitos de configuración de cliente
Asegúrese de que los siguientes componentes están instalados en el equipo cliente:
* Java 7 o superior
*   Microsoft JDBC Driver 6.0 (o posterior) para SQL Server
*   Si está utilizando el modo de autenticación basada en autorización token de acceso, deberá [azure biblioteca de Active Directory para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias para ejecutar los ejemplos de este artículo. Para obtener más información, consulte **conectar usando el Token de acceso** sección.
*   Si está utilizando el modo de autenticación ActiveDirectoryPassword, deberá [azure biblioteca de Active Directory para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias. Para obtener más información, consulte **conectarse con el modo de autenticación ActiveDirectoryPassword** sección.
*   Si está utilizando el modo de ActiveDirectoryIntegrated, necesita azure biblioteca de Active Directory para java y sus dependencias. Para obtener más información, consulte **conectarse con el modo de autenticación ActiveDirectoryIntegrated** sección.
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Conectarse con el modo de autenticación ActiveDirectoryIntegrated
 Con la versión 6.4, Microsoft JDBC Driver agrega compatibilidad con la autenticación de ActiveDirectoryIntegrated con un vale de Kerberos en varias plataformas (Windows/Linux y Mac).
Vea [vale de Kerberos establecido en Windows, Linux y Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) para obtener más detalles. También, en Windows, sqljdbc_auth.dll también se pueden usar para la autenticación de ActiveDirectoryIntegrated con un controlador JDBC.

> [!NOTE]
>  Active esta casilla si está utilizando una versión anterior del controlador, [vínculo](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) para las dependencias correspondientes que son necesarios para usar este modo de autenticación. 

En el ejemplo siguiente se muestra cómo usar ' autenticación = ActiveDirectoryIntegrated' modo. En este ejemplo se ejecute en una máquina unida al dominio que se federa con Azure Active Directory. Un usuario de base de datos independiente que representa la entidad de seguridad de Azure AD, o uno de los grupos, pertenece a, debe existir en la base de datos y debe tener el permiso CONNECT. 

Antes de compilar y ejecutar el ejemplo, en el equipo cliente (en el que, que desea ejecutar el ejemplo), descargue el [biblioteca de azure biblioteca de Active Directory para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias e incluirlos en la ruta de acceso de compilación de Java

Antes de ejecutar el ejemplo, reemplace el nombre de servidor y base de datos con el nombre de servidor y base de datos en las siguientes líneas:

```
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

El ejemplo para usar el modo de autenticación de ActiveDirectoryIntegrated:
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class IntegratedExample {

    public static void main(String[] args) throws Exception {
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
Ejecute este ejemplo en un equipo cliente usa el vale de Kerberos y es necesaria ninguna contraseña. Si se establece una conexión, debería ver el mensaje siguiente:
```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Establecer el vale de Kerberos en Windows, Linux y Mac

Debe configurar un vale de Kerberos vincular el usuario actual a una cuenta de dominio de Windows. A continuación se incluye un resumen de pasos claves.

#### <a name="windows"></a>Windows
JDK viene con `kinit` que puede usar para obtener un vale de KDC (Key Distribution Center) en un dominio Unidos a un equipo que está federada con Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Paso 1: Recuperación de vale de concesión de vales
- **Ejecutar en**: Windows
- **Acción**:
  - Use el comando `kinit username@DOMAIN.COMPANY.COM` para obtener un vale de KDC, a continuación, le solicitará la contraseña del dominio.
  - Use `klist` para ver los vales disponibles. Si el kinit fue correcta, debería ver un vale de krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Puede que necesite especificar una `.ini` de archivos con `-Djava.security.krb5.conf` para la aplicación buscar el KDC.

#### <a name="linux-and-mac"></a>Linux y Mac

##### <a name="requirements"></a>Requisitos
Acceso a un equipo unido a un dominio de Windows para consultar el controlador de dominio Kerberos

##### <a name="step-1-find-kerberos-kdc"></a>Paso 1: Obtener KDC de Kerberos
- **Ejecutar en**: línea de comandos de Windows
- **Acción**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (donde "DOMAIN.COMPANY.COM" se asigna al nombre de su dominio)
- **Salida del ejemplo**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Información para extraer** el nombre de controlador, en este caso `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Paso 2: Configurar KDC en krb5.conf
- **Ejecutar en**: Linux/Mac
- **Acción**: editar el /etc/krb5.conf en un editor de su elección. Configura las siguientes claves
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
  - Use el comando `kinit username@DOMAIN.COMPANY.COM` para obtener un vale de KDC, a continuación, le solicitará la contraseña del dominio.
  - Use `klist` para ver los vales disponibles. Si el kinit fue correcta, debería ver un vale de krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Conectarse con el modo de autenticación ActiveDirectoryPassword
En el ejemplo siguiente se muestra cómo usar ' autenticación = ActiveDirectoryPassword' modo.

Antes de compilar y ejecutar el ejemplo:
1.  En el equipo cliente (en el que, que desea ejecutar el ejemplo), descargue el [biblioteca de azure biblioteca de Active Directory para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias e incluirlos en la ruta de acceso de compilación de Java
2.  Busque las siguientes líneas de código y reemplace el nombre de servidor y base de datos con el nombre de servidor y base de datos.
    ```
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Busque las siguientes líneas de código y reemplace el nombre de usuario, con el nombre de usuario de Azure AD al que desea conectarse como.
    ```
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

El ejemplo para usar el modo de autenticación de ActiveDirectoryPassword:
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class UserPasswordExample {
    
    public static void main(String[] args) throws Exception{
        SQLServerDataSource ds = new SQLServerDataSource();
        
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        ds.setHostNameInCertificate("*.database.windows.net");
        
        Connection connection = ds.getConnection();
        
        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
Si se establece la conexión, verá el mensaje siguiente como salida:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Debe existir una base de datos de usuario independiente y un usuario de base de datos independiente que representa el valor usuario de Azure AD o uno de los grupos, Azure especificado pertenece al usuario de AD, debe existir en la base de datos y debe tener el permiso de conexión (a excepción de Azure Active Directory Administrador del servidor o grupo)


## <a name="connecting-using-access-token"></a>Conectar con el Token de acceso
Aplicaciones y servicios puede recuperar un token de acceso de Azure Active Directory y utilice para conectarse a la base de datos de SQL Azure. Tenga en cuenta que accessToken sólo se puede establecer utilizando el parámetro de propiedades del método getConnection() en la clase DriverManager. No se puede utilizar en la cadena de conexión.
 
En el ejemplo siguiente contiene una sencilla aplicación de Java que se conecta a la base de datos de SQL de Azure mediante la autenticación basada en autorización token de acceso. Antes de compilar y ejecutar el ejemplo, siga los pasos siguientes:
1.  Crear una cuenta de aplicación en Azure Active Directory para el servicio.
    1. Inicie sesión en el portal de administración de Azure
    2. Haga clic en Azure Active Directory en el panel de navegación izquierdo
    3. Haga clic en la ficha "Registros de aplicación".
    4. En el espacio, haga clic en "Nuevo registro de aplicación".
    5. Escriba mytokentest como un nombre descriptivo para la aplicación, seleccione "aplicación/API Web".
    6. No es necesario URL de inicio de sesión. Basta con que proporcione nada: "http://mytokentest".
    7. Haga clic en "Crear" en la parte inferior.
    9. Mientras se encuentra en el portal de Azure, haga clic en la ficha "Configuración" de la aplicación y abra la ficha "Propiedades".
    10. Busque el valor de "identificador de aplicación de (también conocido como Id. de cliente) y cópielo, necesita esto más adelante cuando configure la aplicación (por ejemplo, 1846943b-ad04-4808-aa13-4702d908b5c1). Vea la siguiente instantánea.
    11. Busque el valor de "Dirección URL de Id. de aplicación" y cópielo, ésta es la URL de STS.
    12. En la sección "Claves", cree una clave rellenando el campo de nombre, seleccionando la duración de la clave y guardar la configuración (deje el campo de valor vacío). Después de guardar, el campo de valor debe estar rellena automáticamente, copie el valor generado. Esto es el secreto del cliente.

    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Inicie sesión en la base de datos de usuario del servidor de SQL Azure como un administrador de Azure Active Directory y usar un usuario de base de datos independiente de una disposición de comando de T-SQL para su aplicación principal. Consulte la [conectarse a la base de datos SQL o SQL datos almacenamiento mediante Azure Active Directory autenticación](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) para obtener más información sobre cómo crear un administrador de Azure Active Directory y un usuario de base de datos independiente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  En el equipo cliente (en el que, que desea ejecutar el ejemplo), descargue el [azure biblioteca de Active Directory para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) biblioteca y sus dependencias e incluirlos en la ruta de acceso de compilación de Java. Tenga en cuenta que el azure Active Directory-biblioteca-de-java solo es necesario para ejecutar este ejemplo concreto, ya que usa las API de esta biblioteca para recuperar el token de acceso de Azure AD. Si ya tiene un token de acceso, puede omitir este paso. Tenga en cuenta que también deba quitar la sección en el ejemplo que recupera el token de acceso.

En el ejemplo siguiente, reemplace el nombre de la URL de STS, Id. de cliente, secreto de cliente, servidor y base de datos con sus valores.

```
import java.sql.Connection;
import java.sql.ResultSet;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD. 
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;


public class TokenBasedExample {

    public static void main(String[] args) throws Exception{

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://microsoft.onmicrosoft.com/..."; // Replace with your STS URL.
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

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
``` 

Si la conexión se realiza correctamente, verá el mensaje siguiente como salida:
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
