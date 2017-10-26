---
title: "Conectarse usando la autenticación de Active Directory de Azure | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.topic: article
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83d5ad3bae131b58dd344c3f5f9bfc7f5d0c4f5a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conectarse usando la autenticación de Azure Active Directory
En este artículo se proporciona información sobre cómo desarrollar aplicaciones de Java para usar la característica de autenticación de Azure Active Directory con Microsoft JDBC Driver 6.0 (o superior) para SQL Server.

Desde Microsoft JDBC Driver 6.0 para SQL Server, puede utilizar autenticación de Azure Active Direcoty (AAD), que es un mecanismo de conectarse a la base de datos de SQL Azure v12 mediante identidades de Azure Active Directory. Utilizar autenticación de Azure Active Directory para administrar de forma centralizada las identidades de usuarios de base de datos y como una alternativa a la autenticación de SQL Server. El controlador JDBC 6.0 (o posterior) permite especificar las credenciales de Azure Active Directory en la cadena de conexión de JDBC para conectarse a la base de datos de SQL Azure. Para obtener información sobre cómo configurar la autenticación de Active Directory de Azure, visite [conectarse a SQL base de datos mediante Azure Active Directory autenticación](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Dos nuevas propiedades de conexión que se han agregado para admitir la autenticación de Azure Active Directory:
*   **autenticación**: Utilice esta propiedad para indicar qué método de autenticación de SQL que se utilizará para la conexión. Los valores posibles son: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword** y el valor predeterminado **NotSpecified** .
    * Use ' autenticación = ActiveDirectoryIntegrated' para conectarse a una base de datos de SQL mediante la autenticación integrada de Windows. Para usar este modo de autenticación debe federar la local Active Directory Federation Services (ADFS) con Azure AD en la nube. Una vez completada esta configuración, puede tener acceso a base de datos de SQL Azure sin que se le pidan ceredentials cuando se registran en un equipo unido a dominio. 
    * Use ' autenticación = ActiveDirectoryPassword' para conectarse a una base de datos de SQL mediante un nombre de entidad de seguridad de Azure AD y una contraseña.
    * Use ' autenticación = SqlPassword' para conectarse a SQL Server mediante las propiedades de nombre de usuario o usuario y una contraseña.
    * Use ' autenticación = NotSpecified' o dejarlo como valor predeterminado si se necesita ninguno de estos métodos de autenticación.

*   **accessToken**: Utilice esta propiedad para conectarse a una base de datos SQL con un token de acceso. accessToken sólo puede establecerse mediante el parámetro Properties del método getConnection() en la clase DriverManager. No se puede utilizar en la dirección URL de conexión.  

Para obtener más información, consulte la propiedad de autenticación en el [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) página.  


## <a name="client-setup-requirements"></a>Requisitos de configuración de cliente
Asegúrese de que los siguientes componentes están instalados en el equipo cliente:
* Java 7 o superior
*   6.2 (o superior) de Microsoft JDBC Driver para SQL Server
*   Si está utilizando el modo de autenticación basada en tokens de acceso, deberá [azure biblioteca de Active Directory para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias para ejecutar los ejemplos de este artículo. Vea **conectar usando el Token de acceso** sección para obtener más detalles.
*   Si está utilizando el modo de autenticación ActiveDirectoryPassword deberá [azure biblioteca de Active Directory para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) y sus dependencias. Vea **conectarse con el modo de autenticación ActiveDirectoryPassword** sección para obtener más detalles.
*   Si está utilizando el modo de ActiveDirectoryIntegrated, debe instalar la biblioteca de autenticación de Active Directory para SQL Server (ADALSQL. DLL) y sqljdbc_auth.dll.
    * ADALSQL. DLL permite que las aplicaciones pueden autenticarse en Microsoft Azure SQL Database con Azure Active Directory. Descargar el archivo DLL de [biblioteca de autenticación de Microsoft Active Directory para Microsoft SQL Server](http://www.microsoft.com/en-us/download/details.aspx?id=48742)
    * Para ADALSQL. DLL dos versiones binarias X86 y X64 están disponibles para descargar. Si está instalada la versión binaria incorrecta o si falta el archivo DLL, el controlador generará el siguiente error: "no se puede cargar adalsql.dll (Authentication =...). Código de error: 0 x 2. ". En este caso, descargue la versión correcta de ADALSQL. DLL. 
    * sqljdbc_auth.dll está disponible en el paquete de controladores. Copie el archivo sqljdbc_auth.dll en un directorio en la ruta de acceso del sistema de Windows en el equipo donde está instalado el controlador JDBC. Alternativamente, puede especificar la propiedad del sistema java.libary.path para especificar el directorio de sqljdbc_auth.dll. 
    * Si está ejecutando una JVM de 64 bits en un procesador x64, utilice el archivo sqljdbc_auth.dll de la carpeta x64. 
    * Si está ejecutando una máquina virtual Java de (JVM, Java Virtual Machine) 32 bits, utilice el archivo sqljdbc_auth.dll en la carpeta x86, aun cuando la versión del sistema operativo sea la x64. 
    * Por ejemplo, si usas la JVM de 32 bits y el controlador JDBC está instalado en el directorio predeterminado, puede especificar la ubicación del archivo DLL mediante el siguiente argumento de la máquina virtual (VM) cuando se inicia la aplicación de Java:  
        ```
        -Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86
        ```
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Conectarse con el modo de autenticación ActiveDirectoryIntegrated
En el ejemplo siguiente se muestra cómo usar ' autenticación = ActiveDirectoryIntegrated' modo. En este ejemplo se ejecute en una máquina unida al dominio que se federa con Azure Active Directory. Un usuario de base de datos independiente que representa la entidad de seguridad de Azure AD, o uno de los grupos, pertenece a, debe existir en la base de datos y debe tener el permiso CONNECT. 
    
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
Ejecutar este ejemplo en un equipo unido a un dominio que se federa con Azure Active Directory usarán automáticamente sus credenciales de Windows y es necesaria ninguna contraseña. Si se establece la conexión, verá el mensaje siguiente:
```
You have successfully logged on as: <your domain user name>
```

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
Si se establece la conexión, verá el siguiente mensaje como salida:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Debe existir una base de datos de usuario independiente y un usuario de base de datos independiente que representa el valor usuario de Azure AD o uno de los grupos, Azure especificado pertenece a usuario de AD, debe existir en la base de datos y debe tener el permiso de conexión (a excepción de Azure Active Directory Administrador del servidor o grupo)


## <a name="connecting-using-access-token"></a>Conectar con el Token de acceso
Aplicaciones y servicios puede recuperar un token de acceso de Azure Active Directory y utilice para conectarse a la base de datos de SQL Azure. Tenga en cuenta que accessToken sólo se puede establecer utilizando el parámetro de propiedades del método getConnection() en la clase DriverManager. No se puede utilizar en la cadena de conexión.
 
En el ejemplo siguiente contiene una sencilla aplicación de Java que se conecta a la base de datos de SQL de Azure mediante la autenticación basada en tokens de acceso. Antes de compilar y ejecutar el ejemplo, siga los pasos siguientes:
1.  Crear una cuenta de aplicación en Azure Active Directory para el servicio.
    1. Inicie sesión en el portal de administración de Azure
    2. Haga clic en Azure Active Directory en el panel de navegación izquierdo
    3. Haga clic en el inquilino de directorio donde desea registrar la aplicación de ejemplo. Debe ser el mismo directorio que está asociado a la base de datos (el servidor que hospeda la base de datos).
    4. Haga clic en la pestaña aplicaciones.
    5. En el espacio, haga clic en Agregar.
    6. Haga clic en "Agregar una aplicación que mi organización está desarrollando".
    7. Escriba mytokentest como un nombre descriptivo para la aplicación, seleccione "Aplicación de la Web y/o API de Web" y haga clic en siguiente.
    8. Suponiendo que esta aplicación es un servicio de demonio y no es una aplicación web, no tiene un inicio de sesión de dirección URL o URI de Id. de aplicación. Para estos dos campos, escriba http://mytokentest
    9. Mientras se encuentra en el portal de Azure, haga clic en la ficha configurar de la aplicación
    10. Buscar el valor de identificador de cliente y se copia, se necesitará más adelante cuando configure la aplicación (es decir,  a4bbfe26-dbaa-4fec-8ef5-223d229f647d). Vea la siguiente instantánea.
    11. En la sección "Claves", seleccione la duración de la clave, guardar la configuración y copie la clave para su uso posterior. Esto es el secreto del cliente.
    12. En la parte inferior, haga clic en "Ver extremos" y copie la dirección URL en "Extremo de autorización de OAUTH 2.0" para su uso posterior. Ésta es la URL de STS.


![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)


2. Inicie sesión en la base de datos de usuario del servidor de SQL Azure como un administrador de Azure Active Directory y mediante el aprovisionamiento de un comando de T-SQL un usuario de base de datos independiente para la entidad de seguridad de la aplicación. Consulte la [conectarse a la base de datos SQL o SQL datos almacenamiento mediante Azure Active Directory autenticación](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/) para obtener más información sobre cómo crear un administrador de Azure Active Directory y un usuario de base de datos independiente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  En el equipo cliente (en el que, que desea ejecutar el ejemplo), descargue el [azure biblioteca de Active Directory para java](https://github.com/AzureAD/azure-activedirectory-library-for-java) biblioteca y sus dependencias e incluirlos en la ruta de acceso de compilación de Java. Tenga en cuenta que el azure Active Directory-biblioteca-de-java solo es necesario para ejecutar este ejemplo concreto, ya que usa las API de esta biblioteca para recuperar el token de acceso de Azure AD. Si ya tiene un token de acceso, puede omitir este paso. Tenga en cuenta que también deba quitar la sección en el ejemplo que recupera el token de acceso.

En el ejemplo siguiente, sustituir la URL de STS, Id. de cliente, secreto de cliente, servidor y nombre de base de datos con sus valores.

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
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "a4bbfe26-dbaa-4fec-8ef5-223d229f647d"; // Replace with your client ID.
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

Si la conexión se realiza correctamente, verá el siguiente mensaje como salida:
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 

