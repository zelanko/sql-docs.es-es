---
title: "Autenticación de Active Directory con SQL Server en Linux | Documentos de Microsoft"
description: "Pasos de configuración para la autenticación de AAD para SQL Server en Linux"
author: tmullaney
ms.date: 07/17/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, AAD authentication
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9e6d1afdfa7b7d4ef1bfec4461badca746651c44
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="active-directory-authentication-with-sql-server-on-linux"></a>Autenticación de Active Directory con SQL Server en Linux  
[!INCLUDE[tsql-appliesto-sslinx-only_md](../../docs/includes/tsql-appliesto-sslinx-only_md.md)]


Este documento explica cómo configurar [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] en Linux para admitir la autenticación de Active Directory (AD), la autenticación también se denomina integrada. Autenticación de Active Directory permite que los clientes Unidos a un dominio de Windows o Linux para autenticarse en [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] con sus credenciales de dominio y el protocolo Kerberos. Autenticación de Active Directory tiene las siguientes ventajas sobre [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] autenticación:  
• Los usuarios se autentican a través de inicio de sesión único, sin que se le solicite una contraseña.   
• Mediante la creación de inicios de sesión para grupos de AD, puede administrar el acceso y permisos en [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] con las pertenencias a grupos de AD.  
• Cada usuario tiene una identidad única en toda la organización, por lo que no es necesario realizar un seguimiento del que [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] los inicios de sesión corresponden a las personas.   
• AD permite aplicar una directiva de contraseña centralizada a través de su organización.   

## <a name="prerequisites"></a>Requisitos previos
Antes de configurar la autenticación de Active Directory, debe:
- Configurar un controlador de dominio de Active Directory (Windows) en la red  
- Instale [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)].
  - [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  - [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  - [Ubuntu](quickstart-install-connect-ubuntu.md)

>  [!IMPORTANT]  
>   En este momento, el único método de autenticación admitido para el extremo de reflejo de la base de datos es certificado. Método de autenticación de WINDOWS se habilitará en una versión futura

## <a name="step-1-join-includessnoversiondocsincludesssnoversion-mdmd-host-to-ad-domain"></a>Paso 1: Unir [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] host del dominio de Active Directory
Existen numerosas herramientas que le ayudarán a unir el [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] máquina de host para el dominio de AD. Este tutorial usa  **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)**, un paquete de código abierto populares. Si no lo ha hecho ya, instale el realmd y los paquetes de cliente de Kerberos en el [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] máquina de host mediante el Administrador de paquetes de la distribución Linux:  
```bash  
# RHEL
sudo yum install realmd krb5-workstation

# SUSE
sudo zypper install realmd krb5-client

# Ubuntu
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```  

Si la instalación del paquete de cliente Kerberos le pide que especifique un nombre de dominio, escriba el nombre de dominio en mayúsculas.  

>  [!NOTE]  
>  Este tutorial utiliza "contoso.com" y "CONTOSO.COM" como nombres de dominio y el dominio Kerberos de ejemplo, respectivamente. Debe reemplazarlos con sus propios valores. Estos comandos distinguen mayúsculas de minúsculas, así que asegúrese de que utilice mayúsculas siempre que se usa en este tutorial.  

Ejecute el siguiente comando para comprobar que la [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] equipo host está configurado para usar el controlador de dominio de AD como un servidor de nombres DNS:
```bash  
sudo realm discover contoso.com -v
```  
Si no se encuentra el dominio, debe configurar su [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] máquina de host que se usará la dirección IP del controlador de dominio AD como un servidor de nombres DNS. Los pasos específicos para hacer esto dependen de la configuración de dispositivo de red, la configuración de dominio y la distribución de Linux. Estos son algunos métodos de ejemplo.

### <a name="example-dns-configuration-ubuntu"></a>Ejemplo de configuración de DNS: Ubuntu
Editar la `/etc/network/interfaces` de archivos para que la dirección IP del controlador de dominio AD aparece como un servidor de nombres dns. Por ejemplo: 
 
```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```  
>  [!NOTE]  
>  La interfaz de red (eth0) podría ser diferente en las máquinas diferente. Para averiguar cuál está utilizando, ejecute ifconfig y copie la interfaz que tiene una dirección IP y los bytes transmitidos y recibidos.

Después de editar este archivo, reinicie el servicio de red:
```bash
sudo ifdown eth0 && sudo ifup eth0
```
Ahora, compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al siguiente:  
```Code  
nameserver **<AD domain controller IP address>**
```  

### <a name="example-dns-configuration-rhel"></a>Ejemplo de configuración de DNS: RHEL
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
Ahora, compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al siguiente:  
```Code  
nameserver **<AD domain controller IP address>**
```  

### <a name="join-the-domain"></a>Unirse al dominio
Una vez que haya confirmado que el DNS está configurado correctamente, unirse al dominio, ejecute el comando siguiente. Debe autenticarse mediante una cuenta de AD que tiene privilegios suficientes en Active Directory para unirse a un nuevo equipo al dominio. En concreto, este comando se cree una nueva cuenta de equipo en Active Directory, cree la `/etc/krb5.keytab` archivo keytab de host y configurar el dominio en `/etc/sssd/sssd.conf`:
```bash                                     
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
 * Successfully enrolled machine in realm
```    

>  [!NOTE]  
>   Si ve un error, "paquetes necesarios no están instalados", debe instalar los paquetes mediante el Administrador de paquetes de la distribución de Linux antes de ejecutar el `realm join` comando nuevo. 
>  
>  Si recibe un error, "Permisos insuficientes para unirse al dominio," necesitará póngase en contacto con un administrador de dominio que tiene los permisos necesarios para unir máquinas virtuales Linux a su dominio.

 
Compruebe que ahora puede recopilar información sobre un usuario del dominio y que puede adquirir un vale de Kerberos como dicho usuario. 

We will use **id**, **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)** and **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** commands for this.

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

>  [!NOTE]  
>   Si `id user@contoso.com` devuelve, "Ningún de estos usuarios," Asegúrese de que el servicio SSSD iniciado correctamente, ejecute el comando `sudo systemctl status sssd`. Si el servicio se está ejecutando y todavía aparece el error "No existe el usuario", pruebe a habilitar el registro detallado para SSSD. Para obtener más información, consulte la documentación de Red Hat para [SSSD de solución de problemas de](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).  
>  
>  Si `kinit user@CONTOSO.COM` devuelve, "respuesta KDC no coincidía con las expectativas al obtener credenciales iniciales," Asegúrese de que especifica el dominio en mayúsculas.

Para obtener más información, consulte la documentación de Red Hat para [Descubra y unirse a dominios de identidad](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html). 

## <a name="step-2-create-ad-user-for-includessnoversiondocsincludesssnoversion-mdmd-and-set-spn"></a>Paso 2: Crear el usuario de AD para [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] y establecer SPN  

>  [!NOTE]  
>  En los pasos que se usará el [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Si se encuentra en **Azure**, tendrá que  **[crearlo](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/portal-create-fqdn)**  antes de continuar. 

En el controlador de dominio, ejecute el [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando de PowerShell para crear un nuevo usuario de AD con una contraseña que no expira nunca. Este ejemplo asigna nombre a la cuenta "mssql", pero el nombre de cuenta puede ser que desee. Se le pedirá que escriba una contraseña nueva para la cuenta:  
```PowerShell   
Import-Module ActiveDirectory

New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
```   

>  [!NOTE]  
>  Es un procedimiento recomendado de seguridad para tener una cuenta de AD dedicada de SQL Server, por lo que las credenciales de SQL Server no se comparten con otros servicios que utilicen la misma cuenta. Sin embargo, puede volver a usar una cuenta de AD existente si lo prefiere, si conoce la contraseña de la cuenta (necesaria para generar un archivo de tabla de claves en el paso siguiente).

Ahora debe configurar el ServicePrincipalName (SPN) para esta cuenta mediante la `setspn.exe` herramienta. El SPN debe tener el formato exactamente como se especifica en el siguiente ejemplo: puede encontrar el nombre de dominio completo de la [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] equipo host mediante la ejecución de `hostname --all-fqdns` en el [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] host y el puerto TCP deben ser 1433 a menos que haya configurado [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] utilizar un número de puerto diferente.  
```PowerShell   
setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
```   

>  [!NOTE]  
>  Si recibe un error, "derechos de acceso insuficientes", debe póngase en contacto con un administrador de dominio que tiene los permisos necesarios para establecer un SPN en esta cuenta.
>  
>  Si cambia el puerto TCP en el futuro, a continuación, debe volver a ejecutar el comando setspn con el nuevo número de puerto. También debe agregar el SPN nuevo a la tabla de claves del servicio de SQL Server siguiendo los pasos descritos en la sección siguiente.

Para obtener más información, vea [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  

## <a name="step-3-configure-includessnoversiondocsincludesssnoversion-mdmd-service-keytab"></a>Paso 3: Configurar [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] keytab de servicio  
En primer lugar, compruebe el número de versión de clave (kvno) para la cuenta de AD que creó en el paso anterior. Normalmente será 2, pero podría ser otro entero si cambia la contraseña de cuenta de varias veces. En el [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] equipo host, ejecute lo siguiente:

```bash
kinit user@CONTOSO.COM

kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
```

Ahora cree un archivo de tabla de claves para el usuario de AD que creó en el paso anterior. Para ello, utilizaremos  **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)**. Cuando se le solicite, escriba la contraseña para esa cuenta de AD. 
```bash  
sudo ktutil

ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

quit
```  

>  [!NOTE]  
>  La herramienta ktutil no valida la contraseña, por lo tanto asegúrese de que ha escrito correctamente.

Cualquier persona con acceso a este `keytab` puede suplantar al archivo [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] en el dominio, por lo tanto asegúrese de restringir el acceso a los archivos que sólo el `mssql` cuenta tiene acceso de lectura:  
```bash  
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```  
A continuación, configure [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] usarlo `keytab` archivo para la autenticación Kerberos:  
```bash  
sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```  

## <a name="step-4-create-ad-based-logins-in-transact-sql"></a>Paso 4: Crear inicios de sesión basados en AD en Transact-SQL  
Conectarse a [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] y crear un inicio de sesión nuevo, en función de AD:  
```Transact-SQL  
CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
```   

Compruebe que el inicio de sesión aparece ahora en el [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql.mc) vista de catálogo del sistema:  
```Transact-SQL  
SELECT name FROM sys.server_principals;
```  

## <a name="step-5-connect-to-includessnoversiondocsincludesssnoversion-mdmd-using-ad-authentication"></a>Paso 5: Conectarse a [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] mediante la autenticación de AD  
Inicie sesión en un equipo cliente mediante sus credenciales de dominio. Ahora puede conectarse a [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] sin volver a escribir la contraseña, mediante la autenticación de AD. Si crea un inicio de sesión para un grupo de AD, puede conectar cualquier usuario de AD que sea un miembro de ese grupo de la misma manera.  
El parámetro de cadena de conexión específica para los clientes que usen la autenticación de Active Directory depende de qué controlador que esté utilizando. Algunos ejemplos son a continuación.  

## <a name="examples"></a>Ejemplos  
### <a name="example-1-sqlcmd-on-a-domain-joined-linux-client"></a>Ejemplo 1: `sqlcmd` en un cliente de Linux Unidos a un dominio  
Inicie sesión en un cliente Linux Unidos a un dominio mediante `ssh` y sus credenciales de dominio:  
```bash  
ssh -l user@contoso.com client.contoso.com
```  

Asegúrese de que ha instalado el [mssql herramientas](sql-server-linux-setup-tools.md) del paquete y después conectar utilizando `sqlcmd` sin especificar las credenciales:  
```bash  
sqlcmd -S mssql.contoso.com
```  

### <a name="example-2-ssms-on-a-domain-joined-windows-client"></a>Ejemplo 2: SSMS en un cliente de Windows Unidos a un dominio  
Inicie sesión en un cliente de Windows Unidos a un dominio con sus credenciales de dominio. Asegúrese de que [!INCLUDE[ssmanstudiofull-md](../../docs/includes/ssmanstudiofull-md.md)] está instalado, a continuación, conectarse a su [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] instancia mediante la especificación **autenticación de Windows** en el **conectar al servidor** cuadro de diálogo.  

### <a name="ad-authentication-using-other-client-drivers"></a>Autenticación de AD con otros controladores de cliente  
• JDBC: [con Kerberos de autenticación para conectarse a SQL Server integrada](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server])  
• ODBC: [mediante la autenticación integrada](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)  
• ADO.NET: [sintaxis de la cadena de conexión](https://msdn.microsoft.com/library/ms254500.aspx)   


