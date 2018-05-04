---
title: Con Kerberos de autenticación para conectarse a SQL Server integrada | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d9023c31e0d7b985e17991a080a7c9afc077ff6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Mediante la autenticación integrada de Kerberos para conectarse a SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A partir de [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], una aplicación puede utilizar el **authenticationScheme** propiedad de conexión para indicar que va a conectar a una base de datos mediante la autenticación integrada de Kerberos de tipo 4. Vea [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) para obtener más información sobre propiedades de conexión. Para obtener más información sobre Kerberos, consulte [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758).  
  
 Cuando se usa la autenticación integrada con el de Java **Krb5LoginModule**, puede configurar el módulo mediante [clase Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).  
  
 El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] establece las siguientes propiedades para las máquinas virtuales Java de IBM:  
  
-   **useDefaultCcache = true**  
  
-   **moduleBanner = false**  
  
 El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] establece las siguientes propiedades para todas las demás máquinas virtuales Java:  
  
-   **useTicketCache = true**  
  
-   **doNotPrompt = true**  
  
## <a name="remarks"></a>Comentarios  
 Anteriores a [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], las aplicaciones podían especificar la autenticación integrada (usando Kerberos o NTLM, dependiendo de lo que hubiera disponible) mediante el uso de la **integratedSecurity** propiedad de conexión y haciendo referencia a  **sqljdbc_auth.dll**, tal y como se describe en [generar URL de conexión](../../connect/jdbc/building-the-connection-url.md).  
  
 A partir de [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], una aplicación puede utilizar el **authenticationScheme** propiedad de conexión para indicar que va a conectar a una base de datos utilizando Kerberos integrado autenticación mediante el Kerberos pura de Java implementación:  
  
-   Si desea usar la autenticación integrada **Krb5LoginModule**, aún se debe especificar el **integratedSecurity = true** propiedad de conexión. Después debe especificar también el **authenticationScheme = Kerberos** propiedad de conexión.  
  
-   Para continuar usando la autenticación integrada con **sqljdbc_auth.dll**, simplemente especifique **integratedSecurity = true** propiedad de conexión (y, opcionalmente, **authenticationScheme = NativeAuthentication**).  
  
-   Si especifica **authenticationScheme = Kerberos** pero no se especifica también **integratedSecurity = true**, el controlador omitirá la **authenticationScheme** propiedad de conexión y esperará hasta que encuentre las credenciales de nombre y la contraseña de usuario en la cadena de conexión.  
  
 Al utilizar un origen de datos para crear conexiones, puede establecer mediante programación el esquema de autenticación mediante setAuthenticationScheme y (opcionalmente) establecer el SPN para las conexiones con Kerberos mediante **setServerSpn**.  
  
 Se ha agregado un nuevo registrador para admitir la autenticación Kerberos: com.microsoft.sqlserver.jdbc.internals.KerbAuthentication. Para obtener más información, consulte [funcionamiento del controlador de seguimiento](../../connect/jdbc/tracing-driver-operation.md).  
  
 Las directrices siguientes le ayudarán a configurar Kerberos:  
  
1.  Establecer **AllowTgtSessionKey** en 1 en el registro de Windows. Para obtener más información, consulte [entradas del registro y las claves de configuración del KDC en Windows Server 2003 del protocolo Kerberos](http://support.microsoft.com/kb/837361).  
  
2.  Asegúrese de que la configuración de Kerberos (krb5.conf en entornos UNIX) apunta al dominio Kerberos y al KDC correctos para su entorno.  
  
3.  Inicialice la memoria caché del TGT mediante kinit o iniciando sesión en el dominio.  
  
4.  Cuando una aplicación que utiliza **authenticationScheme = Kerberos** se ejecuta en el Windows Vista o Windows 7, sistemas operativos, debe usar una cuenta de usuario estándar. Sin embargo, si ejecuta la aplicación en una cuenta de administrador, la aplicación debe ejecutarse con privilegios de administrador.  
  
> [!NOTE]  
>  El atributo de conexión serverSpn solo es compatible con Microsoft JDBC Drivers 4.2 y posterior.  
  
## <a name="service-principal-names"></a>Nombres de entidad de seguridad de servicio  
 Un nombre principal de servicio (SPN) es el nombre por el que un cliente identifica de forma unívoca una instancia de un servicio.  
  
 Puede especificar el SPN usando la **serverSpn** propiedad de conexión, o simplemente dejar que el controlador lo genere por usted (el valor predeterminado).  Esta propiedad es en forma de: "MSSQLSvc/fqdn:port@REALM" donde fqdn es el nombre de dominio completo, port es el número de puerto y el territorio es el dominio Kerberos de SQL Server en letras mayúsculas.  La parte del dominio Kerberos de esta propiedad es opcional si el dominio Kerberos predeterminado de la configuración Kerberos es el mismo que el del servidor y no se incluye de forma predeterminada.  Si desea admitir un escenario de autenticación entre dominios Kerberos donde el dominio Kerberos predeterminado en la configuración de Kerberos es diferente del dominio Kerberos del servidor, debe establecer el SPN con la propiedad serverSpn.  
  
 Por ejemplo, los SPN sería: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433@ZZZZ.CORP.CONTOSO.COM"  
  
 Para obtener más información sobre los nombres de entidad de seguridad de servicio (SPN), vea:  
  
-   [Cómo usar la autenticación Kerberos en SQL Server](http://support.microsoft.com/kb/319723)  
  
-   [Usar Kerberos con SQL Server](http://go.microsoft.com/fwlink/?LinkId=207814)  

> [!NOTE]  
> Antes de 6.2.0 de la versión del controlador JDBC, para el uso apropiado de Cross dominio Kerberos, deberá establecer explícitamente el **serverSpn**.
>
> A partir de la 6.2.0 versión, el controlador será capaz de crear el **serverSpn** de forma predeterminada, incluso cuando se utiliza Cross dominio Kerberos. Aunque se pueden usar **serverSpn** explícitamente demasiado. 
  
## <a name="creating-a-login-module-configuration-file"></a>Crear un archivo de configuración de un módulo de inicio de sesión  
 Si lo desea, puede especificar un archivo de configuración de Kerberos. Si no se especifica ningún archivo de configuración, se usarán las configuraciones siguientes:  
  
 Máquina virtual Java de Sun  
 com.sun.security.auth.module.Krb5LoginModule requiere useTicketCache = true;  
  
 Máquina virtual Java de IBM  
 com.ibm.security.auth.module.Krb5LoginModule requiere useDefaultCcache = true;  
  
 Si decide crear un archivo de configuración de un módulo de inicio de sesión, el archivo debe seguir este formato:  
  
```  
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```  
  
 Un archivo de configuración de inicio de sesión consta de una o varias entradas, cada una de las cuales especifica qué tecnología de autenticación subyacente se debe usar para una o varias aplicaciones determinadas. Por ejemplo,  
  
```  
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```  
  
 Cada entrada de un archivo de configuración de un módulo de inicio de sesión consta de un nombre seguido de una o varias entradas específicas del módulo, donde cada una de estas entradas termina con un signo de punto y coma y todo el grupo de entradas específicas del módulo está entre llaves. Cada entrada del archivo de configuración termina con un signo de punto y coma.  
  
 Además de permitir al controlador adquirir credenciales de Kerberos usando las configuraciones especificadas en el archivo de configuración del módulo de inicio de sesión, el controlador puede emplear credenciales existentes. Esto puede resultar útil cuando la aplicación necesite crear conexiones usando credenciales de más de un usuario.  
  
 El controlador intentará usar credenciales existentes si están disponibles, antes de intentar el inicio de sesión usando el módulo de inicio de sesión especificado. Así, cuando se usa el método Subject.doAs para ejecutar código bajo un contexto determinado, se creará una conexión con las credenciales pasadas a la llama a Subject.doAs.  
  
 Para obtener más información, consulte [archivo de configuración de inicio de sesión JAAS](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) y [clase Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).  

 A partir de Microsoft JDBC Driver 6.2, opcionalmente se puede pasar el nombre del archivo de configuración del módulo de inicio de sesión utilizando jaasConfigurationName de propiedad de conexión, esto permite que cada conexión tiene su propia configuración de inicio de sesión.
 
## <a name="creating-a-kerberos-configuration-file"></a>Crear un archivo de configuración de Kerberos  
 Para obtener más información sobre los archivos de configuración de Kerberos, consulte [requisitos de Kerberos](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html).  
  
 A continuación se muestra un archivo de configuración de dominio de ejemplo, donde YYYY e ZZZZ son nombres de dominio de su sitio.  
  
```  
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
 Puede habilitar un archivo de configuración de dominio con -Djava.security.krb5.conf. Puede habilitar un archivo de configuración del módulo de inicio de sesión con **-Djava.security.auth.login.config**.  
  
 Por ejemplo, al iniciar la aplicación podría usar esta línea de comandos:  
  
```  
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  
  
```  
  
## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Comprobar que se puede obtener acceso a SQL Server mediante Kerberos  
 Ejecute la consulta siguiente en SQL Server Management Studio:  
  
 **Seleccione auth_scheme de sys.dm_exec_connections donde session_id = @@spid**  
  
 Asegúrese de que tiene el permiso necesario para ejecutar esta consulta.  

## <a name="constrained-delegation"></a>Delegación restringida
A partir de Microsoft JDBC Driver 6.2, el controlador admite la delegación limitada de Kerberos. Se pueden pasar las credenciales delegada como objeto org.ietf.jgss.GSSCredential, estas credenciales se utilizan por controlador para establecer conexión. 

```
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>Conexión de Kerberos mediante nombres de entidad de seguridad y las contraseñas
A partir de Microsoft JDBC Driver 6.2, el controlador puede establecer Kerberos pasa con el nombre de entidad de seguridad y la contraseña de conexión en la cadena de conexión. 
```
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```
La propiedad de nombre de usuario no requiere el dominio KERBEROS si el usuario pertenece a la default_realm establecido en el archivo krb5.conf. Cuando `userName` y `password` establecer junto con `integratedSecurity=true;` y `authenticationScheme=JavaKerberos;` propiedad, la conexión se establece con el valor del nombre de usuario como el Principal de Kerberos junto con la contraseña proporcionada.
 
## <a name="see-also"></a>Vea también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
