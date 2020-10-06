---
title: Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos
description: Descubra cómo registrar un nombre de entidad de seguridad de servicio (SPN) con Active Directory. Este registro es necesario para usar la autenticación Kerberos con SQL Server.
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 08/12/2020
ms.openlocfilehash: 27e19a66912c220e8c407c4182c3241906af5ea5
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670338"
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 Para usar la autenticación Kerberos con SQL Server se requiere el cumplimiento de las siguientes condiciones:  

- Los equipos servidor y cliente deben formar parte del mismo dominio de Windows o estar en dominios de confianza.  

- Se debe registrar un Nombre principal de servicio (SPN) en Active Directory, suponiendo que el rol del Centro de distribución de claves se encuentre en un dominio de Windows. El SPN, una vez registrado, se asigna a la cuenta de Windows que inició el servicio de la instancia de SQL Server. Si el registro del SPN no se ha realizado o ha provocado un error, el nivel de seguridad de Windows no podrá determinar la cuenta asociada al SPN y no se utilizará la autenticación Kerberos.

    > [!NOTE]  
    >  Si el servidor no puede registrar automáticamente el SPN, este se deberá registrar manualmente. Vea [Registro manual de SPN](#Manual).  

Puede comprobar que una conexión está utilizando Kerberos consultando la vista de administración dinámica sys.dm_exec_connections. Ejecute la consulta siguiente y compruebe el valor de la columna auth_scheme, que será "KERBEROS" si Kerberos está habilitado.

```sql
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;
```

> [!TIP]
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Administrador de configuración de Kerberos para SQL Server** es una herramienta de diagnóstico que sirve para solucionar problemas de conectividad de Kerberos relacionados con SQL Server. Para obtener más información, vea [Administrador de configuración de Microsoft Kerberos para SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  

##  <a name="the-role-of-the-spn-in-authentication"></a><a name="Role"></a> El rol del SPN en la autenticación  

Cuando una aplicación abre una conexión y usa la autenticación de Windows, SQL Server Native Client pasa el nombre del equipo de SQL Server, el nombre de instancia y, opcionalmente, un SPN. Si la conexión pasa un SPN, se utilizará sin ningún cambio.  

Si la conexión no pasa un SPN, se creará un SPN predeterminado basándose en el protocolo utilizado, el nombre del servidor y el nombre de instancia.  

En los escenarios anteriores, el SPN se envía al Centro de distribución de claves con el fin de obtener un token de seguridad para autenticar la conexión. Si no se puede obtener un token de seguridad, la autenticación utilizará NTLM.  

Un nombre principal de servicio (SPN) es el nombre por el que un cliente identifica de forma unívoca una instancia de un servicio. El servicio de autenticación de Kerberos puede utilizar un SPN para autenticar un servicio. Cuando un cliente desea conectarse a un servicio, busca una instancia del servicio, compone un SPN para esa instancia, se conecta al servicio y presenta el SPN para que lo autentique el servicio.  
  
> [!NOTE]  
>  La información proporcionada en este tema también se aplica a las configuraciones de SQL Server que utilizan la agrupación en clústeres.  
  
El método preferido para que los usuarios se autentiquen en SQL Server es la autenticación de Windows. Los clientes que usan la autenticación de Windows se autentican mediante NTLM o Kerberos. En un entorno de Active Directory, se intenta utilizar siempre en primer lugar la autenticación Kerberos. La autenticación Kerberos no está disponible para los clientes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] mediante canalizaciones con nombre.  

##  <a name="permissions"></a><a name="Permissions"></a> Permisos

Al iniciarse el servicio Motor de base de datos, se intenta registrar el nombre principal de servicio (SPN). Supongamos que la cuenta que inicia SQL Server no tiene permiso para registrar un SPN en Active Directory Domain Services. En ese caso, se produce un error en esta llamada y se registra un mensaje de advertencia en el registro de eventos de la aplicación, así como en el registro de errores de SQL Server. Para registrar el SPN, se debe ejecutar Motor de base de datos en una cuenta integrada, como Sistema local (no se recomienda) o Servicio de red, o bien, en una cuenta que tenga permiso para registrar un SPN. Puede registrar un SPN mediante una cuenta de administrador de dominio, pero no se recomienda en un entorno de producción. Cuando SQL Server se ejecuta en el sistema operativo Windows 7 o Windows Server 2008 R2, puede ejecutar SQL Server mediante una cuenta virtual o una cuenta de servicio administrada (MSA). Las cuentas virtuales y las MSA pueden registrar un SPN. Si SQL Server no se ejecuta en ninguna de estas cuentas, el SPN no se registrará en el inicio y el administrador de dominio deberá hacerlo manualmente.

> [!NOTE]  
>  Cuando el dominio de Windows está configurado para ejecutarse en un nivel menor que el funcional de Windows Server 2008 R2, la cuenta de servicio administrada no tendrá los permisos necesarios para registrar los SPN para el servicio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Si se requiere la autenticación Kerberos, el administrador de dominio debe registrar manualmente los SPN de SQL Server en la cuenta de servicio administrada.

Encontrará información adicional en [Implementar la delegación restringida de Kerberos con SQL Server 2008](/previous-versions/sql/sql-server-2008/ee191523(v=sql.100))  

##  <a name="spn-formats"></a><a name="Formats"></a> Formatos de SPN

A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], el formato de SPN ha cambiado para ser compatible con la autenticación Kerberos en TCP/IP, las canalizaciones con nombre y la memoria compartida. Los formatos de SPN admitidos para las instancias predeterminadas y con nombre son los siguientes.  
  
**Instancia con nombre**  
  
-   **MSSQLSvc/\<FQDN>:[\<port> | \<instancename>]** , donde:  
  
    -   **MSSQLSvc** es el servicio que se va a registrar.  
  
    -   **\<FQDN>** es el nombre de dominio completo del servidor.  
  
    -   **\<port>** es el número de puerto TCP.  
  
    -   **\<instancename>** es el nombre de la instancia de SQL Server.  
  
**Instancia predeterminada**  
  
-   **MSSQLSvc/\<FQDN>:\<port>**  | **MSSQLSvc/\<FQDN>** , donde:  
  
    -   **MSSQLSvc** es el servicio que se va a registrar.  
  
    -   **\<FQDN>** es el nombre de dominio completo del servidor.  
  
    -   **\<port>** es el número de puerto TCP.  
  
    > [!NOTE]
    > El nuevo formato SPN no requiere un número de puerto. Esto significa que un servidor con varios puertos o un protocolo que no use números de puerto puede utilizar la autenticación Kerberos.  
   
|Formato de SPN|Descripción|  
|-|-|  
|MSSQLSvc/\<FQDN>:\<port>|SPN predeterminado generado por el proveedor cuando se usa TCP. \<port> es un número de puerto TCP.|  
|MSSQLSvc/\<FQDN>|SPN predeterminado generado por el proveedor para una instancia predeterminada cuando se usa un protocolo distinto de TCP. \<FQDN> es un nombre de dominio completo.|  
|MSSQLSvc/\<FQDN>:\<instancename>|SPN predeterminado generado por el proveedor para una instancia con nombre cuando se usa un protocolo distinto de TCP. \<instancename> es el nombre de una instancia de SQL Server.|  

> [!NOTE]  
> En el caso de una conexión TCP/IP, en la que el puerto TCP está incluido en el SPN, SQL Server debe habilitar el protocolo TCP para que los usuarios puedan conectarse usando la autenticación Kerberos. 

##  <a name="automatic-spn-registration"></a><a name="Auto"></a> Registro automático de SPN  

Cuando se inicia una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , SQL Server intenta registrar el SPN para el servicio SQL Server. Cuando la instancia se detiene, SQL Server intenta anular el registro del SPN. Para una conexión TCP/IP, el SPN se registra con el formato *MSSQLSvc/\<FQDN>* : *\<tcpport>* . Las instancias con nombre y la instancia predeterminada se registran como *MSSQLSvc* y se usa el valor *\<tcpport>* para diferenciar las instancias.  
  
Para el resto de conexiones compatibles con Kerberos, el SPN se registra con el formato *MSSQLSvc/\<FQDN>* / *\<instancename>* para una instancia con nombre. El formato para registrar la instancia predeterminada es *MSSQLSvc/\<FQDN>* .  

Es posible que se requiera una intervención manual para registrar o anular el registro del SPN si la cuenta de servicio carece de los permisos requeridos para estas acciones.  

##  <a name="manual-spn-registration"></a><a name="Manual"></a> Registro manual de SPN  

Para registrar el SPN manualmente, el administrador debe usar la herramienta Setspn.exe incluida en las herramientas de soporte técnico de Microsoft [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] . Para obtener más información, vea el artículo de Knowledge Base [Herramientas de soporte técnico del Service Pack 1 de Windows Server 2003](https://support.microsoft.com/kb/892777) .  

Setspn.exe es una herramienta de línea de comandos que le permite leer, modificar y eliminar la propiedad de directorio Nombres de la entidad de seguridad del servicio (SPN). Esta herramienta también le permite ver los SPN actuales, restablecer los SPN predeterminados de la cuenta y agregar o eliminar los SPN complementarios.  

El ejemplo siguiente muestra la sintaxis usada para registrar manualmente un SPN para una conexión TCP/IP mediante una cuenta de usuario de dominio:  

```
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 redmond\accountname  
```

> [!NOTE]
> Si un SPN ya existe, se debe eliminar antes de que se pueda volver a registrar. Para ello, use el comando `setspn` junto con el modificador `-D` . Los ejemplos siguientes muestran cómo registrar manualmente un nuevo SPN basado en instancias. Para una instancia predeterminada que usa una cuenta de usuario de dominio, utilice:  

```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com redmond\accountname  
```  
  
Para una instancia con nombre, use:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:instancename redmond\accountname  
```  
  
##  <a name="client-connections"></a><a name="Client"></a> Conexiones de cliente  

Los SPN especificados por el usuario son compatibles con los controladores de cliente. Sin embargo, si no se proporciona un SPN, se generará automáticamente basándose en el tipo de conexión de cliente. Para una conexión TCP, se usa un SPN con el formato *MSSQLSvc*/*FQDN*:[*puerto*] tanto para las instancias predeterminadas como para las instancias con nombre.  
  
Para las conexiones de canalización con nombre y de memoria compartida, se usa un SPN con el formato *MSSQLSvc/\<FQDN>:\<instancename>* para una instancia con nombre y *MSSQLSvc/\<FQDN>* para la instancia predeterminada.  
  
**Usar una cuenta de servicio como un SPN**  
  
Las cuentas de servicio se pueden usar como un SPN. Se especifican mediante el atributo de conexión para la autenticación Kerberos y pueden tener los formatos siguientes:  
  
- **NombreDeUsuario\@dominio** o **dominio\nombreDeUsuario** para una cuenta de usuario de dominio.  

- **equipo$\@dominio** o **host\FQDN** para una cuenta de dominio de equipo, como Sistema local o SERVICIOS DE RED.  

Para determinar el método de autenticación de una conexión, ejecute la consulta siguiente.  
  
```sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
``` 

##  <a name="authentication-defaults"></a><a name="Defaults"></a> Valores predeterminados de autenticación  

En la tabla siguiente se describen los valores predeterminados de autenticación que se usan basándose en los escenarios de registro de SPN.  
  
|Escenario|Método de autenticación|  
|--------------|---------------------------|  
|El SPN se asigna a la cuenta de dominio, cuenta virtual, MSA o cuenta integrada correcta. Por ejemplo, Sistema local o Servicio de red.|Las conexiones locales usan NTLM, mientras que las conexiones remotas usan Kerberos.|  
|El SPN es la cuenta de dominio, cuenta virtual, MSA o cuenta integrada correcta.|Las conexiones locales usan NTLM, mientras que las conexiones remotas usan Kerberos.|  
|El SPN se asigna a una cuenta de dominio, cuenta virtual, MSA o cuenta integrada incorrecta.|Se produce un error en la autenticación.|  
|Se produce un error en la búsqueda de SPN o no se asigna a una cuenta de dominio, cuenta virtual, MSA o cuenta integrada correcta, o no es una cuenta de dominio, cuenta virtual MSA o cuenta integrada correcta.|Tanto las conexiones locales como las remotas usan NTLM.|  

> [!NOTE]
> En otras palabras, la cuenta asignada por el SPN registrado es la cuenta en la que se está ejecutando el servicio SQL Server.  

##  <a name="comments"></a><a name="Comments"></a> Comentarios  

La conexión de administrador dedicada (DAC) usa un SPN basado en el nombre de instancia. Se puede usar la autenticación Kerberos con una DAC si se ha registrado correctamente ese SPN. Como alternativa, el usuario puede especificar el nombre de cuenta como un SPN.

Si no se puede registrar el SPN durante el inicio, se indica el problema en el registro de errores de SQL Server y el inicio continúa.  

Si no se puede anular el registro del SPN durante el cierre, se indica el problema en el registro de errores de SQL Server y el cierre continúa.  

## <a name="see-also"></a>Vea también  
- [Compatibilidad con Nombre de entidad de seguridad de servicio &#40;SPN&#41; en conexiones cliente](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)
- [Nombres de entidad de seguridad de servicio &#40;SPNs&#41; en conexiones cliente &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)
- [Nombres de entidad de seguridad de servicio &#40;SPNs&#41; en conexiones cliente &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)
- [Características de SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)
- [Administrar problemas de autenticación Kerberos en un entorno de Reporting Services](/previous-versions/sql/sql-server-2008/ff679930(v=sql.100))