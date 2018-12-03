---
title: Usar la autenticación integrada de Kerberos para conectar con SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7bd04090fd6c6a0cc7a0b8374930f3aba378113
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396166"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Mediante la autenticación integrada de Kerberos para conectarse a SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partir de [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], una aplicación puede usar la propiedad de conexión **authenticationScheme** para indicar que quiere conectar con una base de datos mediante la autenticación integrada de Kerberos de tipo 4. Consulte [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) para obtener más información sobre las propiedades de conexión. Para obtener más información sobre Kerberos, vea [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758).

Cuando se usa la autenticación integrada con **Krb5LoginModule** de Java, se puede configurar el módulo mediante [Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] establece las propiedades siguientes para las máquinas virtuales Java de IBM:

- **useDefaultCcache = true**
- **moduleBanner = false**

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] establece las propiedades siguientes para todas las demás máquinas virtuales Java:

- **useTicketCache = true**
- **doNotPrompt = true**

## <a name="remarks"></a>Notas

Anteriores a [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], las aplicaciones podían especificar la autenticación integrada (usando Kerberos o NTLM, dependiendo de que está disponible) mediante el uso de la **integratedSecurity** propiedad de conexión y haciendo referencia a  **sqljdbc_auth.dll**, tal y como se describe en [generar URL de conexión](../../connect/jdbc/building-the-connection-url.md).

A partir de [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], una aplicación puede usar la propiedad de conexión **authenticationScheme** para indicar que quiere conectar con una base de datos mediante la autenticación integrada de Kerberos con la implementación Kerberos pura de Java:

- Si desea usar la autenticación integrada **Krb5LoginModule**, todavía debe especificar el **integratedSecurity = true** propiedad de conexión. Después debe especificar también el **authenticationScheme = Kerberos** propiedad de conexión.

- Para continuar con la autenticación integrada con **sqljdbc_auth.dll**, basta con especificar **integratedSecurity = true** propiedad de conexión (y, opcionalmente, **authenticationScheme = NativeAuthentication**).

- Si especifica **authenticationScheme = Kerberos** pero no se especifica también **integratedSecurity = true**, el controlador omitirá la **authenticationScheme** propiedad de conexión y esperará buscar las credenciales de nombre y la contraseña de usuario en la cadena de conexión.

Cuando se usa un origen de datos para crear conexiones, se puede establecer mediante programación el esquema de autenticación con setAuthenticationScheme y, opcionalmente, establecer el SPN para las conexiones de Kerberos mediante **setServerSpn**.

Se ha agregado un nuevo registrador para admitir la autenticación Kerberos: com.microsoft.sqlserver.jdbc.internals.KerbAuthentication. Para obtener más información, vea [Hacer un seguimiento del funcionamiento del controlador](../../connect/jdbc/tracing-driver-operation.md).

Las directrices siguientes le ayudarán a configurar Kerberos:

1. Establecer **AllowTgtSessionKey** en 1 en el registro de Windows. Para obtener más información, vea [Kerberos protocol registry entries and KDC configuration keys in Windows Server 2003](https://support.microsoft.com/kb/837361) (Entradas del Registro del protocolo Kerberos y claves de configuración del KDC en Windows Server 2003).
2. Asegúrese de que la configuración de Kerberos (krb5.conf en entornos UNIX) apunta al dominio Kerberos y al KDC correctos para su entorno.
3. Inicialice la memoria caché del TGT mediante kinit o iniciando sesión en el dominio.
4. Cuando una aplicación que usa **authenticationScheme=JavaKerberos** se ejecuta en los sistemas operativos Windows Vista o Windows 7, debe emplear una cuenta de usuario estándar. Sin embargo, si ejecuta la aplicación en una cuenta de administrador, la aplicación debe ejecutarse con privilegios de administrador.

> [!NOTE]  
> El atributo de conexión serverSpn solo es compatible con Microsoft JDBC Driver 4.2 y superior.

## <a name="service-principal-names"></a>Nombres de entidad de seguridad de servicio

Un nombre principal de servicio (SPN) es el nombre por el que un cliente identifica de forma unívoca una instancia de un servicio.

Puede especificar el SPN con la propiedad de conexión **serverSpn** o simplemente dejar que el controlador lo genere automáticamente (el valor predeterminado). Esta propiedad tiene el formato: "MSSQLSvc/fqdn:port\@REALM", donde fqdn es el nombre de dominio completo, port es el número de puerto y REALM es el dominio Kerberos de SQL Server en letras mayúsculas. La parte del dominio Kerberos de esta propiedad es opcional si el dominio Kerberos predeterminado de la configuración Kerberos es el mismo que el del servidor y no se incluye de forma predeterminada. Si desea admitir un escenario de autenticación entre dominios Kerberos donde el dominio Kerberos predeterminado en la configuración de Kerberos es diferente del dominio Kerberos del servidor, debe establecer el SPN con la propiedad serverSpn.

Por ejemplo, el SPN sería: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433\@ZZZZ. CORP. CONTOSO.COM"

Para obtener más información sobre los nombres de entidad de seguridad de servicio (SPN), vea:

- [Cómo utilizar la autenticación Kerberos en SQL Server](https://support.microsoft.com/kb/319723)

- [Usar Kerberos con SQL Server](https://go.microsoft.com/fwlink/?LinkId=207814)

> [!NOTE]  
> Antes de la versión 6.2 del controlador JDBC, uso adecuado de cruce del dominio Kerberos, deberá establecer explícitamente el **serverSpn**.
>
> A partir de la versión 6.2, será capaz de crear el controlador del **serverSpn** de forma predeterminada, incluso cuando se usa entre del dominio Kerberos. Aunque se pueden usar **serverSpn** explícitamente demasiado.

## <a name="creating-a-login-module-configuration-file"></a>Crear un archivo de configuración de un módulo de inicio de sesión

Si lo desea, puede especificar un archivo de configuración de Kerberos. Si no se especifica ningún archivo de configuración, se usarán las configuraciones siguientes:

Máquina virtual Java de Sun  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;

Máquina virtual Java de IBM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;

Si decide crear un archivo de configuración de un módulo de inicio de sesión, el archivo debe seguir este formato:

```java
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```

Un archivo de configuración de inicio de sesión consta de una o varias entradas, cada una de las cuales especifica qué tecnología de autenticación subyacente se debe usar para una o varias aplicaciones determinadas. Por ejemplo,

```java
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```

Cada entrada de un archivo de configuración de un módulo de inicio de sesión consta de un nombre seguido de una o varias entradas específicas del módulo, donde cada una de estas entradas termina con un signo de punto y coma y todo el grupo de entradas específicas del módulo está entre llaves. Cada entrada del archivo de configuración termina con un signo de punto y coma.

Además de permitir al controlador adquirir credenciales de Kerberos usando las configuraciones especificadas en el archivo de configuración del módulo de inicio de sesión, el controlador puede emplear credenciales existentes. Esto puede resultar útil cuando la aplicación necesite crear conexiones usando credenciales de más de un usuario.

El controlador intentará usar credenciales existentes si están disponibles, antes de intentar el inicio de sesión usando el módulo de inicio de sesión especificado. Así, cuando se usa el método Subject.doAs para ejecutar código bajo un contexto determinado, se creará una conexión con las credenciales pasadas a la llama a Subject.doAs.

Para obtener más información, vea [JAAS Login Configuration File](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) (Archivo de configuración de inicio de sesión JAAS) y [Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html) (Clase Krb5LoginModule).

A partir de Microsoft JDBC Driver 6.2, opcionalmente se puede pasar el nombre del archivo de configuración del módulo de inicio de sesión mediante jaasConfigurationName de propiedad de conexión, esto permite que cada conexión a tener su propia configuración de inicio de sesión.

## <a name="creating-a-kerberos-configuration-file"></a>Crear un archivo de configuración de Kerberos

Para obtener más información sobre los archivos de configuración de Kerberos, vea [Requisitos de Kerberos](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html).

A continuación se muestra un archivo de configuración de dominio de ejemplo, donde YYYY e ZZZZ son nombres de dominio de su sitio.

```ini
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  

[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  

[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  

        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  

```

## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>Habilitar el archivo de configuración de dominio y el archivo de configuración del módulo de inicio de sesión

Puede habilitar un archivo de configuración de dominio con -Djava.security.krb5.conf. Puede permitir que un archivo de configuración del módulo de inicio de sesión con **-Djava.security.auth.login.config**.

Por ejemplo, al iniciar la aplicación podría usar esta línea de comandos:

```bash
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  

```

## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Comprobar que se puede obtener acceso a SQL Server mediante Kerberos

Ejecute la consulta siguiente en SQL Server Management Studio:

```sql
select auth_scheme from sys.dm_exec_connections where session_id=\@\@spid
```

Asegúrese de que tiene el permiso necesario para ejecutar esta consulta.

## <a name="constrained-delegation"></a>Delegación restringida

A partir de Microsoft JDBC Driver 6.2, el controlador admite la delegación restringida de Kerberos. Las credenciales de delegado pueden pasarse como objeto org.ietf.jgss.GSSCredential, estas credenciales se usan por el controlador para establecer conexión.

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>Conexión de Kerberos con los nombres de entidad de seguridad y la contraseña

A partir de Microsoft JDBC Driver 6.2, el controlador puede establecer Kerberos pasa con el nombre de entidad de seguridad y la contraseña de conexión en la cadena de conexión.

```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```

La propiedad de nombre de usuario no requiere el dominio KERBEROS si el usuario pertenece a la default_realm establecido en el archivo krb5.conf. Cuando `userName` y `password` se establece junto con `integratedSecurity=true;` y `authenticationScheme=JavaKerberos;` propiedad, la conexión se establece con el valor de nombre de usuario como el Principal de Kerberos a lo largo de con la contraseña proporcionada.

## <a name="see-also"></a>Ver también

[Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
