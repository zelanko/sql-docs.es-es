---
title: 'Tutorial: Utilizar autenticación de Active Directory para SQL Server en Linux'
titleSuffix: SQL Server
description: Este tutorial proporcionan los pasos de configuración para la autenticación de AD para SQL Server en Linux.
author: Dylan-MSFT
ms.author: Dylan.Gray
ms.reviewer: rothja
ms.date: 04/01/2019
manager: craigg
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 5e75a0315c0e632e9637ad1f1467acc90dc586cf
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240783"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Tutorial: Usar la autenticación de Active Directory con SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial se explica cómo configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para admitir la autenticación de Active Directory (AD), autenticación integrada también se denomina. Para obtener información general, consulte [autenticación de Active Directory para SQL Server en Linux](sql-server-linux-active-directory-auth-overview.md).

Este tutorial consta de las siguientes tareas:

> [!div class="checklist"]
> * Únase a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio de AD
> * Crear un usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecer SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de servicio
> * Proteger el archivo keytab
> * Configurar SQL Server para usar el archivo keytab para la autenticación Kerberos
> * Crear inicios de sesión de AD basada en Transact-SQL
> * Conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

## <a name="prerequisites"></a>Requisitos previos

Antes de configurar la autenticación de AD, deberá:

* Configurar un controlador de dominio de Active Directory (Windows) en la red  
* Install [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Únase a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio de AD

Debe unirse el host de SQL Server Linux con un controlador de dominio de Active Directory. Para obtener información sobre cómo unirse a un dominio de Active Directory, consulte [Join de SQL Server en un host Linux a un dominio de Active Directory](sql-server-linux-active-directory-join-domain.md).

## <a id="createuser"></a> Crear usuario de AD (o MSA) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecer SPN

> [!NOTE]
> Los pasos siguientes usan la [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Si se encuentra en **Azure**, primero debe **[crearla](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** antes de continuar.

1. En el controlador de dominio, ejecute el [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando de PowerShell para crear un nuevo usuario de AD con una contraseña que no expira nunca. El siguiente ejemplo nombra la cuenta `mssql`, pero puede ser el nombre de cuenta que desee. Se le pedirá que escriba una contraseña nueva para la cuenta.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > Es una práctica recomendada de seguridad para una cuenta de AD dedicada para SQL Server, para que las credenciales de SQL Server no se comparten con otros servicios que utilicen la misma cuenta. Sin embargo, si lo desea puede reutilizar una cuenta de AD existente si conoce la contraseña de la cuenta (que es necesaria para generar un archivo keytab en el paso siguiente).

2. Establecer el ServicePrincipalName (SPN) para esta cuenta mediante la **setspn.exe** herramienta. El SPN debe tener el formato exactamente como se especifica en el ejemplo siguiente. Puede encontrar el nombre de dominio completo de la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipo host mediante la ejecución de `hostname --all-fqdns` en el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host. El puerto TCP debe ser 1433 a menos que haya configurado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar un número de puerto diferente.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Si recibe un error, `Insufficient access rights`, póngase en contacto con su administrador de dominio que tiene permisos suficientes para establecer un SPN en esta cuenta.
   >
   > Si cambia el puerto TCP en el futuro, debe ejecutar el **setspn** comando nuevo con el nuevo número de puerto. También deberá agregar el SPN nuevo a la tabla de claves del servicio de SQL Server siguiendo los pasos descritos en la sección siguiente.

Para obtener más información, vea [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de servicio

Hay dos maneras diferentes de configurar los archivos de tabla de claves del servicio de SQL Server. La primera opción es usar una cuenta de equipo (UPN), mientras que la segunda opción se utiliza una cuenta de servicio administrada (MSA) en la configuración de la tabla de claves. Ambos mecanismos son igualmente funcionales, y puede elegir el método más adecuado para su entorno.

En ambos casos, es necesario el SPN que creó en el paso anterior y se debe registrar el SPN en la tabla de claves.

Para configurar el archivo keytab de servicio de SQL Server:

1. Configurar la [entradas de SPN keytab](#spn) en la sección siguiente.

1. A continuación, ya sea [agregar UPN](#upn) (opción 1) o [MSA](#msa) entradas (opción 2) en el archivo keytab siguiendo los pasos descritos en las secciones respectivas.

> [!IMPORTANT]
> Si se cambia la contraseña para el UPN/MSA o se cambia la contraseña de la cuenta que los SPN se asignan a, debe actualizar la tabla de claves con la nueva contraseña y el número de versión de clave (KVNO). Algunos servicios también pueden girar automáticamente las contraseñas. Revise las directivas de rotación de contraseñas para las cuentas en cuestión y alinearlos con las actividades de mantenimiento programado para evitar tiempos de inactividad inesperados.

### <a id="spn"></a> Entradas de tabla de claves SPN

1. Compruebe el número de versión de clave (KVNO) para la cuenta de AD que creó en el paso anterior. Normalmente es 2, pero podría ser otro entero si cambió la contraseña de la cuenta por varias veces. En el equipo host de SQL Server, ejecute los siguientes comandos:

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

   > [!NOTE]
   > SPN pueden tardar varios minutos en propagarse a través de su dominio, especialmente si el dominio es grande. Si recibe el error, `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`, espere unos minutos y vuelva a intentarlo.  

1. Iniciar **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Agregue las entradas de tabla de claves para cada SPN mediante los siguientes comandos:

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac -sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac -sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. Escribir la tabla de claves en un archivo y, a continuación, cierre ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > El **ktutil** herramienta no valida la contraseña, así que asegúrese de que escriba correctamente cuando se le solicite.

### <a id="upn"></a> Opción 1: Uso de UPN para configurar la tabla de claves

Agregar la cuenta de equipo a la tabla de claves con **ktutil**. La cuenta de equipo (también denominada un UPN) está presente en **/etc/krb5.keytab** en el formulario `<hostname>$@<realm.com>` (por ejemplo, `sqlhost$@CONTOSO.COM`). Copie estas entradas de **/etc/krb5.keytab** a **mssql.keytab**.

1. Iniciar **ktuil** con el siguiente comando:

   ```bash
   sudo ktutil
   ```

1. Use la **rkt** comando leer todas las entradas de **/etc/krb5.keytab**.

   ```bash
   rkt /etc/krb5.keytab
   ```

1. A continuación, se enumeran las entradas.

   ```bash
   list
   ```

1. Elimine todas las entradas por su número de ranura que no son el UPN. Hacerlo uno a la vez, repita el comando siguiente:

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > Cuando se elimina una entrada como ranura 1, todas las diapositivas de valores de uno para ocupar su lugar. Esto significa que la entrada en la ranura 2 se mueve a la ranura 1 cuando se elimina la entrada de la ranura de 1.

1. Lista de las entradas de nuevo hasta que quedan solo las entradas UPN.

   ```bash
   list
   ```

1. Cuando quedan solo las entradas UPN, anexar estos valores a **mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. Salga de **ktutil**.

   ```bash
   quit
   ```

### <a id="msa"></a> Opción 2:  Uso de MSA para configurar la tabla de claves

Para la opción de MSA, debe crear tabla de claves de Kerberos de SQL Server. Debe contener toda la [SPN registrados en el primer paso](#spn) y las credenciales para la MSA para que los SPN están registrados. 

1. Después de la tabla de claves SPN se crean las entradas, ejecute los comandos siguientes desde una máquina Linux que está unido al dominio:

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   Este paso muestra la KVNO para la cuenta de usuario asignada la propiedad SPN. Este paso trabajar, el SPN debe se asignaron a la cuenta MSA durante su creación. Si el SPN no se le asignó MSA, el KVNO muestra se de cuenta de propietario actual de SPN y sean incorrectos que se usará para la configuración.  

1. Iniciar **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Agregar la MSA con los dos comandos siguientes:

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. Escribir la tabla de claves en un archivo y, a continuación, cierre ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. Cuando se usa el enfoque MSA, una opción de configuración debe establecerse con el **mssql-conf** herramienta para especificar la MSA que se usará al obtener acceso al archivo keytab. Asegúrese de que los siguientes valores están en **/var/opt/mssql/mssql.conf**.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > Incluir solo el nombre MSA y no el nombre de dominio\cuenta.

## <a id="securekeytab"></a> Proteger el archivo keytab

Cualquier persona con acceso a este archivo keytab puede suplantar a SQL Server en el dominio, así que asegúrese de que restringir el acceso al archivo de modo que sólo la cuenta mssql tenga acceso de lectura:

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> Configurar SQL Server para usar el archivo keytab para la autenticación Kerberos

Usar siguiendo los pasos para configurar el servidor de SQL para empezar a usar el archivo de la tabla de claves para la autenticación Kerberos.

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

La opción de deshabilitar las conexiones UDP para el controlador de dominio para mejorar el rendimiento. En muchos casos, las conexiones UDP constantemente un error al conectarse a un controlador de dominio, por lo que puede establecer opciones de configuración **/etc/krb5.conf** para omitir las llamadas UDP. Editar **/etc/krb5.conf** y establecer las siguientes opciones:

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

En este punto, está listo para usar inicios de sesión de AD basada en SQL Server como sigue.

## <a id="createsqllogins"></a> Crear inicios de sesión de AD basada en Transact-SQL

1. Conectarse a SQL Server y cree un inicio de sesión nuevo, en función de AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. Compruebe que el inicio de sesión aparece ahora en el [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista de catálogo del sistema:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Conectarse a SQL Server mediante autenticación de AD

Inicie sesión en un equipo cliente mediante las credenciales del dominio. Ahora puede conectarse a SQL Server sin volver a escribir la contraseña mediante la autenticación de AD. Si crea un inicio de sesión para un grupo de AD, puede conectar cualquier usuario de AD que sea un miembro de ese grupo en la misma manera.

El parámetro de cadena de conexión específica para los clientes que usen la autenticación de Active Directory depende en el controlador que se esté utilizando. Considere los ejemplos en las secciones siguientes.

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>Sqlcmd en un cliente Linux unido al dominio

Inicie sesión en un cliente Linux unido al dominio mediante **ssh** y sus credenciales de dominio:

```bash
ssh -l user@contoso.com client.contoso.com
```

Asegúrese de que ha instalado el [mssql-tools](sql-server-linux-setup-tools.md) del paquete y después conectar utilizando **sqlcmd** sin especificar las credenciales:

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>SSMS en un cliente de Windows unido al dominio

Inicie sesión en un cliente de Windows unido al dominio con sus credenciales de dominio. Asegúrese de que está instalado SQL Server Management Studio, a continuación, conectarse a la instancia de SQL Server (por ejemplo, `mssql-host.contoso.com`) mediante la especificación de **Windows autenticación** en el **conectar al servidor** cuadro de diálogo.

### <a name="ad-authentication-using-other-client-drivers"></a>Autenticación de Active Directory con otros controladores de cliente

En la tabla siguiente se describe las recomendaciones para que otros controladores de cliente:

| Controlador de cliente | Recomendación |
|---|---|
| **JDBC** | Usar la autenticación integrada de Kerberos para conectarse a SQL Server. |
| **ODBC** | Usar la autenticación integrada. |
| **ADO.NET** | Sintaxis de cadena de conexión. |

## <a id="additionalconfig"></a> Opciones de configuración adicionales

Si está utilizando las utilidades de terceros, como [pbi](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), o [Centrify](https://www.centrify.com/) para unir el host de Linux a AD dominio y le gustaría obligar a SQL server en uso la openldap biblioteca directamente, puede configurar el **disablesssd** opción con **mssql-conf** como sigue:

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> Hay utilidades como **realmd** que configura SSSD, mientras que otras herramientas, como los pbi, VAS y Centrify no configurar SSSD. Si la utilidad empleada para unirse a dominio de AD no configuración SSSD, se recomienda configurar **disablesssd** opción `true`. Aunque no es necesario que SQL Server intentará usar SSSD para AD antes de recurrir al mecanismo de openldap, sería más eficaz para configurarlo para que SQL Server realiza llamadas de openldap directamente omitir el mecanismo de SSSD.

Si el controlador de dominio es compatible con LDAPS, puede forzar que todas las conexiones de SQL Server a los controladores de dominio con LDAPS. Para comprobar que el cliente puede ponerse en contacto con el controlador de dominio mediante ldaps, ejecute el siguiente comando de bash, `ldapsearch -H ldaps://contoso.com:3269`. Para configurar SQL Server para usar solo LDAPS, ejecute lo siguiente:

```bash
sudo mssql-conf set network.forceldaps true
systemctl restart mssql-server
```

Utilizar LDAPS a través de SSSD Si une al dominio de Active Directory de host se realizó con el paquete SSSD y **disablesssd** no está establecida en true. Si **disablesssd** está establecido en true junto con **forceldaps** se establece en true, entonces se utilizará Protocolo LDAPS a través de las llamadas de biblioteca openldap realizadas por SQL Server.

### <a name="post-sql-server-2017-cu14"></a>Registrar SQL Server 2017 CU14

A partir de SQL Server 2017 CU14, si SQL Server se ha unido a un controlador de dominio de AD mediante proveedores de terceros y está configurado para usar llamadas openldap para la búsqueda de AD general estableciendo **disablesssd** a true, también puede usar **enablekdcfromkrb5** opción para obligar a SQL Server para usar la biblioteca krb5 para la búsqueda KDC en lugar de búsqueda inversa de DNS para el servidor KDC.

Esto puede ser útil para el escenario donde desea configurar manualmente los controladores de dominio que intente comunicarse con SQL Server. Y usar el mecanismo de biblioteca openldap mediante el uso de la lista KDC en **krb5.conf**.

En primer lugar, establezca **disablessd** y **enablekdcfromkrb5conf** en true y, a continuación, reinicie SQL Server:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

A continuación, configure la lista KDC en **/etc/krb5.conf** como sigue:

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> Aunque no se recomienda, es posible usar utilidades, como **realmd**, que establece al unirse al dominio, el host de Linux durante la configuración de SSSD **disablesssd** en true para que use SQL Server OpenLDAP llamadas en su lugar de SSSD para Active Directory relacionados con las llamadas.

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
