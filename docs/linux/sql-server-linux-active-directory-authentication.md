---
title: Tutorial de autenticación de Active Directory para SQL Server en Linux | Microsoft Docs
description: Este tutorial proporcionan los pasos de configuración para la autenticación de AAD para SQL Server en Linux.
author: meet-bhagdev
ms.date: 02/23/2018
ms.author: meetb
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 2804197643c96e21bd0f412cf757ba0b4e2bdfbc
ms.sourcegitcommit: ca5430ff8e3f20b5571d092c81b1fb4c950ee285
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/01/2018
ms.locfileid: "43381263"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Tutorial: Autenticación uso de Active Directory con SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial se explica cómo configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para admitir la autenticación de Active Directory (AD), autenticación integrada también se denomina. Para obtener información general, consulte [autenticación de Active Directory para SQL Server en Linux](sql-server-linux-active-directory-auth-overview.md).

Este tutorial consta de las siguientes tareas:

> [!div class="checklist"]
> * Únase a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio de AD
> * Crear un usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecer SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de servicio
> * Crear inicios de sesión de AD basada en Transact-SQL
> * Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

> [!NOTE]
>
> Si desea configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para usar un proveedor de AD de otros fabricantes, consulte [usar otros proveedores de Active Directory con SQL Server en Linux](./sql-server-linux-active-directory-third-party-providers.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de configurar la autenticación de AD, deberá:

* Configurar un controlador de dominio de Active Directory (Windows) en la red  
* Instale [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Únase a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio de AD

Siga estos pasos para unir un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host a un dominio de Active Directory:

1. Use **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** para unir el equipo host a su dominio de AD. Si no lo ha hecho ya, instale los paquetes de cliente de Kerberos y los realmd en el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipo host mediante el Administrador de paquetes de su distribución de Linux:

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Si la instalación del paquete de cliente Kerberos le pide un nombre de dominio Kerberos, escriba el nombre de dominio en mayúsculas.

   > [!NOTE]
   > En este tutorial usa "contoso.com" y "CONTOSO.COM" como nombres de dominio y del dominio de ejemplo, respectivamente. Debe reemplazar estos elementos con sus propios valores. Estos comandos distinguen mayúsculas de minúsculas, así que asegúrese de que usa mayúsculas siempre que se usa en este tutorial.

1. Configurar su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipo host para usar la dirección IP del controlador de dominio AD como un servidor de nombres DNS. 

   - **Ubuntu**:

      Editar el `/etc/network/interfaces` archivo para que la dirección IP del controlador de dominio AD aparece como un servidor de nombres de dns. Por ejemplo: 

      ```/etc/network/interfaces
      <...>
      # The primary network interface
      auto eth0
      iface eth0 inet dhcp
      dns-nameservers **<AD domain controller IP address>**
      dns-search **<AD domain name>**
      ```

      > [!NOTE]
      > La interfaz de red (eth0) podría diferir para distintas máquinas. Para averiguar cuál de ellos usa, ejecute ifconfig y copie la interfaz que tiene una dirección IP y los bytes transmitidos y recibidos.

      Después de editar este archivo, reinicie el servicio de red:

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      Ahora compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al ejemplo siguiente:  

      ```/etc/resolv.conf
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

     Editar el `/etc/sysconfig/network-scripts/ifcfg-eth0` archivo (o en otra configuración de interfaz de archivos según corresponda) para que la dirección IP del controlador de dominio AD aparece como un servidor DNS:

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     ```

     Después de editar este archivo, reinicie el servicio de red:

     ```bash
     sudo systemctl restart network
     ```

     Ahora compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al ejemplo siguiente:  

     ```/etc/resolv.conf
     nameserver **<AD domain controller IP address>**
     ```

   - **SLES**:

     Editar el `/etc/sysconfig/network/config` archivo para que la IP del controlador de dominio de AD se usará para las consultas DNS y el dominio de AD está en la lista de búsqueda de dominio:

     ```/etc/sysconfig/network/config
     <...>
     NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
     ```

     Después de editar este archivo, reinicie el servicio de red:

     ```bash
     sudo systemctl restart network
     ```

     Ahora compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al ejemplo siguiente:

     ```/etc/resolv.conf
     nameserver **<AD domain controller IP address>**
     ```

1. Unirse al dominio

   Una vez que haya confirmado que el DNS está configurado correctamente, unirse al dominio, ejecute el comando siguiente. Debe autenticarse con una cuenta de AD que tiene privilegios suficientes en Active Directory para unirse a un nuevo equipo al dominio.

   En concreto, este comando crea una nueva cuenta de equipo en AD, cree el `/etc/krb5.keytab` archivo keytab de host y configurar el dominio en `/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > Si ve un error, "no se instalan los paquetes necesarios", debe instalar los paquetes con el Administrador de paquetes de su distribución de Linux antes de ejecutar el `realm join` nuevo comando.
   >
   > Si recibe un error, "Permisos insuficientes para unirse al dominio,", a continuación, deberá comprobar con un administrador de dominio que tiene suficientes permisos para unir equipos Linux a su dominio.
   >
   > Si recibe un error, "respuesta KDC no coincide con las expectativas,", a continuación, es posible que no ha especificado el nombre de dominio correcto para el usuario. Nombres de dominio Kerberos distinguen mayúsculas de minúsculas, mayúsculas normalmente y puede identificarse con el comando `realm discover contoso.com`.
   
   > SQL Server utiliza SSSD y NSS para asignar cuentas de usuario y grupos a los identificadores de seguridad (SID). SSSD debe estar configurado y se ejecutan en orden para SQL Server crear los inicios de sesión de AD correctamente. Realmd normalmente lo hace automáticamente como parte de la unión al dominio, pero en algunos casos debe hacerlo por separado.
   >
   > Consulte las siguientes opciones para configurar [SSSD manualmente](https://access.redhat.com/articles/3023951), y [configurar NSS para trabajar con SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

  
5. Compruebe que ahora puede recopilar información acerca de un usuario del dominio y que puede adquirir un vale de Kerberos como ese usuario.

   En el ejemplo siguiente se usa **id**,  **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**, y **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** comandos para esto.

   ```bash
   id user@contoso.com
   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM
   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   <...>
   ```

   > [!NOTE]
   > Si `id user@contoso.com` devuelve, "Ningún tal usuario", asegúrese de que el servicio SSSD ha iniciado correctamente ejecutando el comando `sudo systemctl status sssd`. Si el servicio se está ejecutando y aún ve el error "No existe el usuario", pruebe a habilitar el registro detallado para SSSD. Para obtener más información, consulte la documentación de Red Hat para [solución de problemas de SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > Si `kinit user@CONTOSO.COM` devuelve, "respuesta KDC no coincide con las expectativas al obtener las credenciales de iniciales," Asegúrese de que especifica el dominio en mayúsculas.

Para obtener más información, consulte la documentación de Red Hat para [unirse a dominios de identidad y descubra](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html). 

## <a id="createuser"></a> Crear un usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecer SPN

  > [!NOTE]
  > Use los pasos siguientes su [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Si se encuentra en **Azure**, primero debe **[crearla](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** antes de continuar.

1. En el controlador de dominio, ejecute el [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando de PowerShell para crear un nuevo usuario de AD con una contraseña que no expira nunca. Este ejemplo asigna la cuenta "mssql", pero puede ser el nombre de cuenta que desee. Se le pedirá que escriba una contraseña nueva para la cuenta:

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > Es una práctica recomendada de seguridad para una cuenta de AD dedicada para SQL Server, para que las credenciales de SQL Server no se comparten con otros servicios que utilicen la misma cuenta. Sin embargo, puede reutilizar una cuenta de AD existente si lo prefiere, si conoce la contraseña de la cuenta (necesaria para generar un archivo keytab en el paso siguiente).

2. Establecer el ServicePrincipalName (SPN) para esta cuenta mediante el `setspn.exe` herramienta. El SPN debe tener el formato exactamente como se especifica en el ejemplo siguiente. Puede encontrar el nombre de dominio completo de la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipo host mediante la ejecución de `hostname --all-fqdns` en el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host y el puerto TCP deben ser 1433 a menos que haya configurado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar un número de puerto diferente.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Si recibe un error, "derechos de acceso insuficientes", debe comprobar con un administrador de dominio que tiene permisos suficientes para establecer un SPN en esta cuenta.
   >
   > Si cambia el puerto TCP en el futuro, debe volver a ejecutar el comando setspn con el nuevo número de puerto. También deberá agregar el SPN nuevo a la tabla de claves del servicio de SQL Server siguiendo los pasos descritos en la sección siguiente.

3. Para obtener más información, vea [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de servicio

1. Compruebe el número de versión de clave (kvno) para la cuenta de AD que creó en el paso anterior. Normalmente es 2, pero podría ser otro entero si cambió la contraseña de la cuenta por varias veces. En el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina host, ejecute lo siguiente:

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

   > [!NOTE]
   > SPN pueden tardar varios minutos en propagarse a través de su dominio, especialmente si el dominio es grande. Si recibe el error, "kvno: servidor no se encuentra en la base de datos de Kerberos al obtener las credenciales para MSSQLSvc /\*\*\<nombre de dominio completo del equipo host\>\*\*:\* \* \<el puerto tcp\>\*\*\@CONTOSO.COM ", espere unos minutos y vuelva a intentarlo.

2. Cree un archivo keytab con **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** para el usuario de AD que creó en el paso anterior. Cuando se le solicite, escriba la contraseña para esa cuenta de AD.

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > La herramienta ktutil no validar la contraseña, así que asegúrese de que ha escrito correctamente.

3. Agregar la cuenta de equipo a la tabla de claves con  **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)**. La cuenta de equipo (también denominada un UPN) está presente en `/etc/krb5.keytab` con el formato "\<hostname\>$\@\<realm.com\>" (p. ej. sqlhost$\@CONTOSO.COM). Copiamos estas entradas de `/etc/krb5.keytab` a `mssql.keytab`.

   ```bash
   sudo ktutil

   # Read all entries from /etc/krb5.keytab
   ktutil: rkt /etc/krb5.keytab

   # List all entries
   ktutil: list

   # Delete all entries by their slot number which are not the UPN one at a
   # time.
   # Warning: when an entry is deleted (e.g. slot 1), all values slide up by
   # one to take its place (e.g. the entry in slot 2 moves to slot 1 when slot
   # 1's entry is deleted)
   ktutil: delent <slot num>
   ktutil: delent <slot num>
   ...

   # List all entries to ensure only UPN entries are left
   ktutil: list

   # When only UPN entries are left, append these values to mssql.keytab
   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

4. Cualquier persona con acceso a este `keytab` puede suplantar el archivo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el dominio, por tanto, asegúrese de restringir el acceso a los archivos que sólo el `mssql` cuenta tiene acceso de lectura:

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

5. Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar este `keytab` archivo para la autenticación Kerberos:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

6. Opcional: Deshabilitar las conexiones UDP para el controlador de dominio para mejorar el rendimiento. En muchos casos, las conexiones UDP siempre producirá un error al conectarse a un controlador de dominio, por lo que puede establecer opciones de configuración `/etc/krb5.conf` para omitir las llamadas UDP. Editar `/etc/krb5.conf` y establecer las siguientes opciones:

   ```/etc/krb5.conf
   [libdefaults]
   udp_preference_limit=0
   ```

## <a id="createsqllogins"></a> Crear inicios de sesión de AD basada en Transact-SQL

1. Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y crear un inicio de sesión nuevo, en función de AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. Compruebe que el inicio de sesión aparece ahora en el [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista de catálogo del sistema:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

Inicie sesión en un equipo cliente mediante las credenciales del dominio. Ahora puede conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sin volver a escribir la contraseña, mediante la autenticación de AD. Si crea un inicio de sesión para un grupo de AD, puede conectar cualquier usuario de AD que sea un miembro de ese grupo en la misma manera.

El parámetro de cadena de conexión específica para los clientes que usen la autenticación de Active Directory depende en el controlador que se esté utilizando. Considere los ejemplos siguientes:

* `sqlcmd` en un cliente Linux unido al dominio

   Inicie sesión en un cliente Linux unido al dominio mediante `ssh` y sus credenciales de dominio:

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   Asegúrese de que ha instalado el [mssql-tools](sql-server-linux-setup-tools.md) del paquete y después conectar utilizando `sqlcmd` sin especificar las credenciales:

   ```bash
   sqlcmd -S mssql-host.contoso.com
   ```

* SSMS en un cliente de Windows unido al dominio

   Inicie sesión en un cliente de Windows unido al dominio con sus credenciales de dominio. Asegúrese de que [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] está instalado, a continuación, conectarse a su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia (por ejemplo, "mssql-host.contoso.com") mediante la especificación de **Windows autenticación** en el **conectar al servidor** cuadro de diálogo.

* Autenticación de Active Directory con otros controladores de cliente

  * JDBC: [con Kerberos de autenticación para conectarse a SQL Server integrada](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC: [mediante la autenticación integrada](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET: [sintaxis de la cadena de conexión](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)

## <a name="performance-improvements"></a>Mejoras de rendimiento
Si observa que las búsquedas de cuenta de AD tardan un tiempo y ha comprobado es válida con los pasos de configuración de AD [Use autenticación de Active Directory con SQL Server en Linux a través de proveedores de terceros AD](sql-server-linux-active-directory-third-party-providers.md), puede agregar el las líneas siguientes a `/var/opt/mssql/mssql.conf` para omitir las llamadas SSSD y utilizar directamente las llamadas LDAP.

```/var/opt/mssql/mssql.conf
[network]
disablesssd = true
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, hemos visto cómo configurar la autenticación de Active Directory con SQL Server en Linux. Ha aprendido a:
> [!div class="checklist"]
> * Únase a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio de AD
> * Crear un usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecer SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de servicio
> * Crear inicios de sesión de AD basada en Transact-SQL
> * Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

A continuación, explorar otros escenarios de seguridad para SQL Server en Linux.

> [!div class="nextstepaction"]
>[Cifrar conexiones a SQL Server en Linux](sql-server-linux-encrypted-connections.md)
