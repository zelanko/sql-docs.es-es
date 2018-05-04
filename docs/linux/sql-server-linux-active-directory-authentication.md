---
title: Tutorial de autenticación de directorio activo para SQL Server en Linux | Documentos de Microsoft
description: Este tutorial indican los pasos de configuración para la autenticación de AAD para SQL Server en Linux.
author: meet-bhagdev
ms.date: 02/23/2018
ms.author: meetb
manager: craigg
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 0ff01d10ceb460375df9b3b3ce4a06191b5aaba2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Tutorial: Autenticación uso de Active Directory con SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial le explica cómo configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para admitir la autenticación de Active Directory (AD), la autenticación también se denomina integrada. Para obtener información general, vea [autenticación de Active Directory para SQL Server en Linux](sql-server-linux-active-directory-auth-overview.md).

Este tutorial consta de las siguientes tareas:

> [!div class="checklist"]
> * Unir [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host del dominio de Active Directory
> * Crear usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecer SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de servicio
> * Crear inicios de sesión basados en AD en Transact-SQL
> * Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

## <a name="prerequisites"></a>Requisitos previos

Antes de configurar la autenticación de Active Directory, debe:

* Configurar un controlador de dominio de Active Directory (Windows) en la red  
* Instale [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Unir [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host del dominio de Active Directory

Siga estos pasos para unir un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host a un dominio de Active Directory:

1. Use **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** para unir el equipo host a su dominio de AD. Si no lo ha hecho ya, instale el realmd y los paquetes de cliente de Kerberos en el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina de host mediante el Administrador de paquetes de la distribución Linux:

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Si la instalación del paquete de cliente Kerberos le pide que especifique un nombre de dominio, escriba el nombre de dominio en mayúsculas.

   > [!NOTE]
   > Este tutorial utiliza "contoso.com" y "CONTOSO.COM" como nombres de dominio y el dominio Kerberos de ejemplo, respectivamente. Debe reemplazarlos con sus propios valores. Estos comandos distinguen mayúsculas de minúsculas, así que asegúrese de que utilice mayúsculas siempre que se usa en este tutorial.

1. Configurar la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina de host que se usará la dirección IP del controlador de dominio AD como un servidor de nombres DNS. 

   - **Ubuntu**:

      Editar la `/etc/network/interfaces` de archivos para que la dirección IP del controlador de dominio AD aparece como un servidor de nombres dns. Por ejemplo: 

      ```/etc/network/interfaces
      <...>
      # The primary network interface
      auth eth0
      iface eth0 inet dhcp
      dns-nameservers **<AD domain controller IP address>**
      dns-search **<AD domain name>**
      ```

      > [!NOTE]
      > La interfaz de red (eth0) podría ser diferente en distintos equipos. Para averiguar cuál está utilizando, ejecute ifconfig y copie la interfaz que tiene una dirección IP y los bytes transmitidos y recibidos.

      Después de editar este archivo, reinicie el servicio de red:

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      Ahora, compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al ejemplo siguiente:  

      ```Code
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

     Editar el `/etc/sysconfig/network-scripts/ifcfg-eth0` archivo (o en otro config de la interfaz de archivos según corresponda) para que la dirección IP del controlador de dominio AD aparece como un servidor DNS:

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     ```

     Después de editar este archivo, reinicie el servicio de red:

     ```bash
     sudo systemctl restart network
     ```

     Ahora, compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al ejemplo siguiente:  

     ```Code
     nameserver **<AD domain controller IP address>**
     ```

1. Unirse al dominio

   Una vez que haya confirmado que el DNS está configurado correctamente, unirse al dominio ejecutando el comando siguiente. Debe autenticarse mediante una cuenta de AD que tiene privilegios suficientes en Active Directory para unirse a un nuevo equipo al dominio.

   En concreto, este comando crea una nueva cuenta de equipo en Active Directory, cree la `/etc/krb5.keytab` archivo keytab de host y configurar el dominio en `/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > Si ve un error, "paquetes necesarios no están instalados", debe instalar los paquetes mediante el Administrador de paquetes de la distribución de Linux antes de ejecutar el `realm join` comando nuevo.
   >
   > Si recibe un error, "Permisos insuficientes para unirse al dominio" necesario póngase en contacto con un administrador de dominio que tiene los permisos necesarios para unir máquinas virtuales Linux a su dominio.
   >
   > Si recibe un error, "respuesta KDC no coincidía con las expectativas,", a continuación, puede que no haya especificado el nombre del dominio correcto para el usuario. Nombres de dominio Kerberos distinguen mayúsculas de minúsculas, mayúsculas normalmente y se pueden identificar con el comando `realm discover contoso.com`.
   
   > SQL Server usa SSSD y NSS para asignar cuentas de usuario y grupos a los identificadores de seguridad (SID). SSSD debe estar configurado y ejecutándose en orden para SQL Server crear los inicios de sesión de AD correctamente. Realmd normalmente lo hace automáticamente como parte de unirse al dominio, pero en algunos casos debe hacer esto por separado.
   >
   > Consulte los siguientes procedimientos para configurar [SSSD manualmente](https://access.redhat.com/articles/3023951), y [configurar NSS para trabajar con SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

  
5. Compruebe que ahora puede recopilar información sobre un usuario del dominio y que puede adquirir un vale de Kerberos como dicho usuario.

   En el ejemplo siguiente se utiliza **identificador**,  **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**, y **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** comandos para este.

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
   > Si `id user@contoso.com` devuelve, "Ningún de estos usuarios," Asegúrese de que el servicio SSSD iniciado correctamente, ejecute el comando `sudo systemctl status sssd`. Si el servicio se está ejecutando y todavía aparece el error "No existe el usuario", pruebe a habilitar el registro detallado para SSSD. Para obtener más información, consulte la documentación de Red Hat para [SSSD de solución de problemas de](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > Si `kinit user@CONTOSO.COM` devuelve, "respuesta KDC no coincidía con las expectativas al obtener credenciales iniciales," Asegúrese de que especifica el dominio en mayúsculas.

Para obtener más información, consulte la documentación de Red Hat para [Descubra y unirse a dominios de identidad](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html). 

## <a id="createuser"></a> Crear usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecer SPN

  > [!NOTE]
  > Los siguientes pasos utilizan la [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Si se encuentra en **Azure**, primero debe **[crearlo](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/portal-create-fqdn)** antes de continuar.

1. En el controlador de dominio, ejecute el [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando de PowerShell para crear un nuevo usuario de AD con una contraseña que no expira nunca. Este ejemplo asigna nombre a la cuenta "mssql", pero el nombre de cuenta puede ser que desee. Se le pedirá que escriba una contraseña nueva para la cuenta:

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > Es un procedimiento recomendado de seguridad para tener una cuenta de AD dedicada de SQL Server, por lo que las credenciales de SQL Server no se comparten con otros servicios que utilicen la misma cuenta. Sin embargo, puede volver a usar una cuenta de AD existente si lo prefiere, si conoce la contraseña de la cuenta (necesaria para generar un archivo de tabla de claves en el paso siguiente).

2. Establecer el ServicePrincipalName (SPN) para esta cuenta mediante la `setspn.exe` herramienta. El SPN debe tener el formato exactamente como se especifica en el ejemplo siguiente. Puede encontrar el nombre de dominio completo de la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipo host mediante la ejecución de `hostname --all-fqdns` en el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host y el puerto TCP deben ser 1433 a menos que haya configurado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizar un número de puerto diferente.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Si recibe un error, "derechos de acceso insuficientes", debe póngase en contacto con un administrador de dominio que tiene los permisos necesarios para establecer un SPN en esta cuenta.
   >
   > Si cambia el puerto TCP en el futuro, debe volver a ejecutar el comando setspn con el nuevo número de puerto. También debe agregar el SPN nuevo a la tabla de claves del servicio de SQL Server siguiendo los pasos descritos en la sección siguiente.

3. Para obtener más información, vea [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de servicio

1. Compruebe el número de versión de clave (kvno) para la cuenta de AD que creó en el paso anterior. Normalmente es 2, pero podría ser otro entero si cambia la contraseña de cuenta de varias veces. En el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipo host, ejecute lo siguiente:

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

2. Crear un archivo keytab con **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** para el usuario de AD que creó en el paso anterior. Cuando se le solicite, escriba la contraseña para esa cuenta de AD.

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > La herramienta ktutil no valida la contraseña, por lo tanto asegúrese de que ha escrito correctamente.

3. Cualquier persona con acceso a este `keytab` puede suplantar al archivo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el dominio, por lo tanto asegúrese de restringir el acceso a los archivos que sólo el `mssql` cuenta tiene acceso de lectura:

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

4. Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usarlo `keytab` archivo para la autenticación Kerberos:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

## <a id="createsqllogins"></a> Crear inicios de sesión basados en AD en Transact-SQL

1. Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y crear un inicio de sesión nuevo, en función de AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. Compruebe que el inicio de sesión aparece ahora en el [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista de catálogo del sistema:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

Inicie sesión en un equipo cliente mediante sus credenciales de dominio. Ahora puede conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sin volver a escribir la contraseña, mediante la autenticación de AD. Si crea un inicio de sesión para un grupo de AD, puede conectar cualquier usuario de AD que sea un miembro de ese grupo de la misma manera.

El parámetro de cadena de conexión específica para los clientes que usen la autenticación de Active Directory depende de qué controlador que esté utilizando. Considere los ejemplos siguientes:

* `sqlcmd` en un cliente de Linux Unidos a un dominio

   Inicie sesión en un cliente Linux Unidos a un dominio mediante `ssh` y sus credenciales de dominio:

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   Asegúrese de que ha instalado el [mssql herramientas](sql-server-linux-setup-tools.md) del paquete y después conectar utilizando `sqlcmd` sin especificar las credenciales:

   ```bash
   sqlcmd -S mssql.contoso.com
   ```

* SSMS en un cliente de Windows Unidos a un dominio

   Inicie sesión en un cliente de Windows Unidos a un dominio con sus credenciales de dominio. Asegúrese de que [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] está instalado, a continuación, conectarse a su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia mediante la especificación **autenticación de Windows** en el **conectar al servidor** cuadro de diálogo.

* Autenticación de AD con otros controladores de cliente

  * JDBC: [con Kerberos de autenticación para conectarse a SQL Server integrada](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC: [mediante la autenticación integrada](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET: [sintaxis de la cadena de conexión](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)
  
## <a name="next-steps"></a>Pasos siguientes

En este tutorial, hemos visto cómo configurar la autenticación de Active Directory con SQL Server en Linux. También habrá aprendido cómo para:
> [!div class="checklist"]
> * Unir [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host del dominio de Active Directory
> * Crear usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecer SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de servicio
> * Crear inicios de sesión basados en AD en Transact-SQL
> * Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

A continuación, explorar otros escenarios de seguridad para SQL Server en Linux.

> [!div class="nextstepaction"]
>[Cifrado de las conexiones a SQL Server en Linux](sql-server-linux-encrypted-connections.md)
