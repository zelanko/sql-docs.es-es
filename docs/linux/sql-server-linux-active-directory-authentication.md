---
title: 'Tutorial: Uso de la autenticación de AD para SQL Server en Linux'
titleSuffix: SQL Server
description: En este tutorial se proporcionan los pasos para configurar la autenticación de AD para SQL Server en Linux.
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 69bbeb31f8da4023bd0630ae0d944165407e2dec
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027330"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Tutorial: Uso de la autenticación de Active Directory con SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial se explica cómo configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para admitir la autenticación de Active Directory (AD), también conocida como autenticación integrada. Para consultar una introducción, vea [Autenticación de Active Directory para SQL Server en Linux](sql-server-linux-active-directory-auth-overview.md).

Este tutorial consta de las tareas siguientes:

> [!div class="checklist"]
> * Unión del host de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el dominio de AD
> * Creación del usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecimiento del SPN
> * Configuración del archivo keytab del servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> * Protección del archivo keytab
> * Configuración de SQL Server para usar el archivo keytab para la autenticación Kerberos
> * Creación de inicios de sesión basados en AD en Transact-SQL
> * Conexión con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

## <a name="prerequisites"></a>Prerequisites

Antes de configurar la autenticación de AD, debe hacer lo siguiente:

* Configurar un controlador de dominio de AD (Windows) en la red.  
* Instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Unión del host de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el dominio de AD

Debe unir el host de SQL Server Linux con un controlador de dominio de Active Directory. Para obtener información sobre cómo unir un dominio de Active Directory, consulte [Unión de SQL Server en un host de Linux a un dominio de Active Directory](sql-server-linux-active-directory-join-domain.md).

## <a id="createuser"></a> Creación del usuario de AD (o MSA) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecimiento del SPN

> [!NOTE]
> En los siguientes pasos se usa el [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Si está en **Azure**, debe **[crear uno](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** para poder continuar.

1. En el controlador de dominio, ejecute el comando de PowerShell [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) para crear un usuario de AD con una contraseña que no expire nunca. En el ejemplo siguiente se asigna el nombre `mssql` a la cuenta, pero el nombre de la cuenta puede ser el que quiera. Se le pedirá que escriba una nueva contraseña para la cuenta.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > Es un procedimiento de seguridad recomendado tener una cuenta de AD dedicada para SQL Server, de modo que las credenciales de SQL Server no se compartan con otros servicios que usen la misma cuenta. En cambio, si quiere puede volver a usar una cuenta de AD existente si conoce su contraseña (que es necesaria para generar un archivo keytab en el paso siguiente).

2. Establezca el ServicePrincipalName (SPN) de esta cuenta mediante la herramienta **setspn.exe**. El SPN debe tener el formato exacto que se especifica en el ejemplo siguiente. Para buscar el nombre de dominio completo del equipo host de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], ejecute `hostname --all-fqdns` en el host de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. El puerto TCP debe ser 1433 a menos que haya configurado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar otro número de puerto.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Si recibe el error `Insufficient access rights`, pídale al administrador del dominio que compruebe si tiene permisos suficientes para establecer un SPN en esta cuenta.
   >
   > Si cambia el puerto TCP en el futuro, debe volver a ejecutar el comando **setspn** con el nuevo número de puerto. También debe seguir los pasos de la siguiente sección para agregar el nuevo SPN al archivo keytab del servicio SQL Server.

Para obtener más información, vea [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configuración del archivo keytab del servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Hay dos formas diferentes de configurar los archivos keytab del servicio SQL Server. La primera opción es usar una cuenta de equipo (UPN), mientras que en la segunda opción se usa una cuenta de servicio administrada (MSA) en la configuración de keytab. Ambos mecanismos funcionan igualmente y puede elegir el método que mejor se adapte a su entorno.

En ambos casos, se necesita el SPN creado en el paso anterior, que debe estar registrado en el archivo keytab.

Para configurar el archivo keytab del servicio SQL Server:

1. Configure las [entradas de keytab del SPN](#spn) en la sección siguiente.

1. Después, [agregue las entradas del UPN](#upn) (opción 1) o [MSA](#msa) (opción 2) en el archivo keytab; para ello, siga los pasos de las secciones correspondientes.

> [!IMPORTANT]
> Si se cambia la contraseña de UPN/MSA o se cambia la contraseña de la cuenta a la que se asignan los SPN, debe actualizar el archivo keytab con la nueva contraseña y el número de versión de la clave (KVNO). Algunos servicios también pueden rotar las contraseñas automáticamente. Consulte las directivas de rotación de contraseñas de las cuentas en cuestión y adáptelas a las actividades de mantenimiento programado para evitar tiempos de inactividad inesperados.

### <a id="spn"></a> Entradas del archivo keytab de SPN

1. Compruebe el número de versión de la clave (KVNO) de la cuenta de AD creada en el paso anterior. Suele ser 2, pero podría ser otro entero si ha cambiado la contraseña de la cuenta varias veces. En el equipo host de SQL Server, ejecute los siguientes comandos:

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > Los SPN pueden tardar varios minutos en propagarse por el dominio, sobre todo si el dominio es grande. Si recibe el error `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`, espere unos minutos y vuelva a intentarlo.  

1. Inicie **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Agregue entradas de keytab de cada SPN mediante los siguientes comandos:

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. Escriba el archivo keytab en un archivo y después salga de ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > La herramienta **ktutil** no valida la contraseña, por lo que debe asegurarse de escribirla correctamente cuando se le pida.

### <a id="upn"></a> Opción 1: uso del UPN para configurar el archivo keytab

Agregue la cuenta de equipo al archivo keytab con **ktutil**. La cuenta de equipo (también denominada UPN) está presente en **/etc/krb5.keytab** con el formato `<hostname>$@<realm.com>` (por ejemplo, `sqlhost$@CONTOSO.COM`). Copie estas entradas de **/etc/krb5.keytab** en **mssql.keytab**.

1. Inicie **ktutil** con el comando siguiente:

   ```bash
   sudo ktutil
   ```

1. Use el comando **rkt** para leer todas las entradas de **/etc/krb5.keytab**.

   ```bash
   rkt /etc/krb5.keytab
   ```

1. Después, enumere las entradas.

   ```bash
   list
   ```

1. Elimine todas las entradas que no sean el UPN por su número de ranura. Repita el siguiente comando y hágalo de una en una:

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > Al eliminar una entrada, como la ranura 1, todos los valores se deslizan hacia arriba una vez para ocupar su lugar. Esto significa que la entrada de la ranura 2 se mueve a la ranura 1 cuando se elimina la entrada de la ranura 1.

1. Vuelva a enumerar las entradas hasta que solo queden las entradas del UPN.

   ```bash
   list
   ```

1. Cuando solo queden las entradas del UPN, anexe estos valores a **mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. Salga de **ktutil**.

   ```bash
   quit
   ```

### <a id="msa"></a> Opción 2:  uso de MSA para configurar el archivo keytab

En el caso de la opción de MSA, debe crear el archivo keytab de Kerberos de SQL Server. Debe contener todos los [SPN registrados en el primer paso](#spn) y las credenciales de la MSA en la que se registran los SPN. 

1. Una vez creadas las entradas de keytab del SPN, ejecute los siguientes comandos desde un equipo Linux que esté unido a un dominio:

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   En este paso se muestra el KVNO de la cuenta de usuario asignada a la propiedad del SPN. Para que este paso funcione, el SPN debe haberse asignado a la cuenta de MSA durante su creación. Si el SPN no se ha asignado a la MSA, el KVNO que se muestra será la cuenta del propietario del SPN actual y será incorrecto usarla para la configuración.  

1. Inicie **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Agregue la cuenta de MSA con los dos comandos siguientes:

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. Escriba el archivo keytab en un archivo y después salga de ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. Al usar el enfoque de MSA, es necesario establecer una opción de configuración con la herramienta **mssql-conf** para especificar la cuenta de MSA que se va a usar al acceder al archivo keytab. Asegúrese de que los valores siguientes están en **/var/opt/mssql/mssql.conf**.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > Incluya solo el nombre de la MSA y no el dominio\nombre de la cuenta.

## <a id="securekeytab"></a> Protección del archivo keytab

Cualquier persona con acceso a este archivo keytab puede suplantar SQL Server en el dominio, por lo que debe asegurarse de restringir el acceso al archivo de forma que solo la cuenta mssql tenga acceso de lectura:

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> Configuración de SQL Server para usar el archivo keytab para la autenticación Kerberos

Siga los pasos que se indican a continuación para configurar SQL Server a fin de empezar a usar el archivo keytab para la autenticación Kerberos.

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

Opcionalmente, deshabilite las conexiones UDP al controlador de dominio para mejorar el rendimiento. En muchos casos, se produce un error coherente en las conexiones UDP al conectarse a un controlador de dominio, por lo que puede establecer opciones de configuración en **/etc/krb5.conf** para omitir las llamadas a UDP. Edite **/etc/krb5.conf** y establezca las siguientes opciones:

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

En este momento, ya puede usar inicios de sesión basados en AD en SQL Server como se indica a continuación.

## <a id="createsqllogins"></a> Creación de inicios de sesión basados en AD en Transact-SQL

1. Conéctese a SQL Server y cree un inicio de sesión basado en AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. Compruebe que el inicio de sesión aparece en la vista del catálogo del sistema [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md):

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Conexión con SQL Server mediante la autenticación de AD

Inicie sesión en un equipo cliente con sus credenciales de dominio. Ya puede conectarse a SQL Server sin volver a escribir la contraseña mediante la autenticación de AD. Si crea un inicio de sesión para un grupo de AD, cualquier usuario de AD que pertenezca a ese grupo podrá conectarse de la misma manera.

El parámetro de cadena de conexión específico para que los clientes usen la autenticación de AD depende del controlador que esté usando. Fíjese en los ejemplos de las secciones siguientes.

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>sqlcmd en un cliente Linux unido a un dominio

Inicie sesión en un cliente Linux unido a un dominio con **ssh** y sus credenciales de dominio:

```bash
ssh -l user@contoso.com client.contoso.com
```

Asegúrese de que ha instalado el paquete [mssql-tools](sql-server-linux-setup-tools.md) y después conéctese con **sqlcmd** sin especificar ninguna credencial:

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>SSMS en un cliente Windows unido a un dominio

Inicie sesión en un cliente Windows unido a un dominio con sus credenciales de dominio. Asegúrese de que SQL Server Management Studio esté instalado y luego conéctese a su instancia de SQL Server (por ejemplo, `mssql-host.contoso.com`) al especificar **Autenticación de Windows** en el cuadro de diálogo **Conectar al servidor**.

### <a name="ad-authentication-using-other-client-drivers"></a>Autenticación de AD con otros controladores de cliente

En la tabla siguiente se describen las recomendaciones de otros controladores de cliente:

| Controlador de cliente | Recomendación |
|---|---|
| **JDBC** | Use la autenticación integrada Kerberos para conectarse con SQL Server. |
| **ODBC** | Use la autenticación integrada. |
| **ADO.NET** | Sintaxis de la cadena de conexión. |

## <a id="additionalconfig"></a> Opciones de configuración adicionales

Si usa utilidades de terceros como [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/) o [Centrify](https://www.centrify.com/) para unir el host de Linux con el dominio de AD y quiere forzar que SQL server use la biblioteca openldap directamente, puede configurar la opción **disablesssd** con **mssql-conf** de la siguiente forma:

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> Hay utilidades como **realmd** que configuran SSSD, mientras que otras herramientas como PBI, VAS y Centrify no configuran SSSD. Si la utilidad que ha usado para unirse al dominio de AD no configura SSSD, se recomienda configurar la opción **disablesssd** en `true`. Aunque no es necesario ya que SQL Server intentará usar SSSD para AD antes de revertir al mecanismo de openldap, sería más eficaz configurarlo para que SQL Server haga que las llamadas a openldap omitan directamente el mecanismo de SSSD.

Si su controlador de dominio admite LDAPS, puede forzar que todas las conexiones de SQL Server a los controladores de dominio sean a través de LDAPS. Para comprobar si el cliente puede ponerse en contacto con el controlador de dominio mediante LDAPS, ejecute el siguiente comando de Bash: `ldapsearch -H ldaps://contoso.com:3269`. Para establecer SQL Server para que solo use LDAPS, ejecute lo siguiente:

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

De esta forma, se usará LDAPS antes que SSSD si la unión a un dominio de AD en el host se ha realizado mediante el paquete SSSD y **disablesssd** no está establecido en true. Si **disablesssd** está establecido en true y **forcesecureldap** está establecido en true, usará el protocolo LDAPS antes que las llamadas a la biblioteca openldap realizadas por SQL Server.

### <a name="post-sql-server-2017-cu14"></a>A partir de SQL Server 2017 CU14

A partir de SQL Server 2017 CU14, si SQL Server se ha unido a un controlador de dominio de AD mediante proveedores de terceros y está configurado para usar llamadas a openldap para la búsqueda general de AD al establecer **disablesssd** en true, también puede usar la opción **enablekdcfromkrb5** para forzar que SQL Server use la biblioteca krb5 para la búsqueda de KDC en lugar de la búsqueda inversa de DNS para el servidor de KDC.

Esto puede ser útil para el escenario en el que quiere configurar manualmente los controladores de dominio con los que SQL Server intenta comunicarse. Para usar el mecanismo de la biblioteca openldap, se utiliza la lista de KDC de **krb5.conf**.

En primer lugar, establezca **disablessd** y **enablekdcfromkrb5conf** en true y después reinicie SQL Server:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

Luego, configure la lista de KDC en **/etc/krb5.conf** como se indica a continuación:

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> Aunque no se recomienda, es posible usar utilidades, como **realmd**, que configuran SSSD a la vez que unen el host de Linux al dominio, al mismo tiempo que se configura **disablesssd** en true para que SQL Server use las llamadas a openldap en lugar de SSSD para las llamadas relacionadas con Active Directory.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se ha descrito cómo configurar la autenticación de Active Directory con SQL Server en Linux. Ha aprendido lo siguiente:
> [!div class="checklist"]
> * Unión del host de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el dominio de AD
> * Creación del usuario de AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y establecimiento del SPN
> * Configuración del archivo keytab del servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> * Creación de inicios de sesión basados en AD en Transact-SQL
> * Conexión con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la autenticación de AD

Explore ahora otros escenarios de seguridad para SQL Server en Linux.

> [!div class="nextstepaction"]
> [Cifrado de conexiones a SQL Server en Linux](sql-server-linux-encrypted-connections.md)
