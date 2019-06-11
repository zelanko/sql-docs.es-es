---
title: Únase a SQL Server en Linux con Active Directory
titleSuffix: SQL Server
description: ''
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: rothja
ms.date: 04/01/2019
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 50f2685b5b981cddfdba61f91b7ec04e9f6345d6
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822526"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>Únase a SQL Server en un host Linux a un dominio de Active Directory

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se proporciona instrucciones generales sobre cómo unir una máquina de host de Linux de SQL Server a un dominio de Active Directory (AD). Hay dos métodos: usar un paquete SSSD integrado o usar otros proveedores de Active Directory. Ejemplos de productos de unión de dominio de otros fabricantes son [PowerBroker Identity Services (pbi)](https://www.beyondtrust.com/), [una sola identidad](https://www.oneidentity.com/products/authentication-services/), y [Centrify](https://www.centrify.com/). Esta guía incluye los pasos para comprobar la configuración de Active Directory. Sin embargo, no está pensado para proporcionar instrucciones sobre cómo unir un equipo a un dominio al usar las utilidades de terceros.

## <a name="prerequisites"></a>Requisitos previos

Antes de configurar la autenticación de Active Directory, deberá configurar un controlador de dominio de Active Directory, Windows, en la red. A continuación, unir el servidor de SQL en el host de Linux a un dominio de Active Directory.

> [!IMPORTANT]
> Los pasos de ejemplo descritos en este artículo son únicamente como guía. Los pasos reales pueden diferir ligeramente en su entorno según cómo esté configurado el entorno general. Póngase en contacto a los administradores del sistema y de dominio para su entorno para la configuración específica, la personalización y cualquier solución de problemas.

## <a name="check-the-connection-to-a-domain-controller"></a>Compruebe la conexión a un controlador de dominio

Compruebe que puede ponerse en contacto con el controlador de dominio con los nombres cortos y completos del dominio:

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> Este tutorial se usa **contoso.com** y **CONTOSO.COM** como nombres de dominio y del dominio de ejemplo, respectivamente. También usa **DC1. CONTOSO.COM** como el ejemplo de nombre de dominio del controlador de dominio completo. Debe reemplazar estos nombres con sus propios valores.

Si se produce un error en cualquiera de estas comprobaciones de nombre, actualice la lista de búsqueda de dominio. Las secciones siguientes proporcionan instrucciones para Ubuntu, Red Hat Enterprise Linux (RHEL) y SUSE Linux Enterprise Server (SLES), respectivamente.

### <a name="ubuntu"></a>Ubuntu

1. Editar el **/etc/network/interfaces** de archivos, por lo que es el dominio de Active Directory en la lista de búsqueda de dominio:

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > La interfaz de red `eth0`, podrían ser diferentes en distintos equipos. Para averiguar cuál de ellos usa, ejecute **ifconfig**. A continuación, copie la interfaz que tiene una dirección IP y los bytes transmitidos y recibidos.

1. Después de editar este archivo, reinicie el servicio de red:

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. A continuación, compruebe que su **/etc/resolv.conf** archivo contiene una línea similar al ejemplo siguiente:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel"></a>RHEL

1. Editar el **/etc/sysconfig/network-scripts/ifcfg-eth0** de archivos, por lo que es el dominio de Active Directory en la lista de búsqueda de dominio. O bien, edite el archivo de configuración de otra interfaz según corresponda:

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. Después de editar este archivo, reinicie el servicio de red:

   ```bash
   sudo systemctl restart network
   ```

1. Ahora compruebe que su **/etc/resolv.conf** archivo contiene una línea similar al ejemplo siguiente:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. Si todavía no se puede hacer ping en el controlador de dominio, buscar el nombre de dominio completo y la dirección IP del controlador de dominio. Es un nombre de dominio de ejemplo **DC1. CONTOSO.COM**. Agregue la siguiente entrada al **/etcetera/hosts**:

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles"></a>SLES

1. Editar el **/etc/sysconfig/network/config** archivo, para que la IP del controlador de dominio de Active Directory se utiliza para consultas DNS y el dominio de Active Directory está en la lista de búsqueda de dominio:

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. Después de editar este archivo, reinicie el servicio de red:

   ```bash
   sudo systemctl restart network
   ```

1. A continuación, compruebe que su **/etc/resolv.conf** archivo contiene una línea similar al ejemplo siguiente:

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>Unirse al dominio de AD

Después de comprobar la configuración básica y la conectividad con el controlador de dominio, hay dos opciones para unirse a un equipo de host de SQL Server Linux con el controlador de dominio de Active Directory:

- [Opción 1: Utilizar un paquete SSSD](#option1)
- [Opción 2: Usar las utilidades de terceros openldap proveedor](#option2)

### <a id="option1"></a> Opción 1: Use el paquete SSSD para unirse a dominio de AD

Este método une a un dominio de AD mediante el host de SQL Server **realmd** y **sssd** paquetes.

> [!NOTE]
> Este es el método preferido de unirse a un host de Linux a un controlador de dominio de AD.

Realice los pasos siguientes para unir un host de SQL Server a un dominio de Active Directory:

1. Use [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join) para unir el equipo host a su dominio de AD. En primer lugar debe instalar tanto el **realmd** y paquetes de cliente de Kerberos en el equipo host de SQL Server mediante el Administrador de paquetes de su distribución de Linux:

   **RHEL:**

   ```base
   sudo yum install realmd krb5-workstation
   ```

   **SUSE:**

   ```bash
   sudo zypper install realmd krb5-client
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Si la instalación del paquete de cliente Kerberos le pide un nombre de dominio Kerberos, escriba el nombre de dominio en mayúsculas.

1. Después de confirmar que el DNS está configurado correctamente, unirse al dominio, ejecute el comando siguiente. Debe autenticarse con una cuenta de AD que tiene privilegios suficientes en Active Directory para unirse a un nuevo equipo al dominio. Este comando crea una nueva cuenta de equipo en AD, se crea el **/etc/krb5.keytab** host archivo keytab, configura el dominio en **/etc/sssd/sssd.conf**, actualizaciones y **/etc/krb5.conf**.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   Debería ver el mensaje, `Successfully enrolled machine in realm`.

   En la tabla siguiente se enumera algunos mensajes de error que puede recibir y sugerencias sobre cómo resolver ellos:

   | Mensaje de error | Recomendación |
   |---|---|
   | `Necessary packages are not installed` | Instale los paquetes con el Administrador de paquetes de su distribución de Linux antes de ejecutar el comando de combinación del dominio nuevo. |
   | `Insufficient permissions to join the domain` | Compruebe con el Administrador de dominio que tiene suficientes permisos para unir equipos Linux a su dominio. |
   | `KDC reply did not match expectations` | No es posible que haya especificado el nombre de dominio correcto para el usuario. Nombres de dominio Kerberos distinguen mayúsculas de minúsculas, mayúsculas normalmente y puede identificarse con el dominio Kerberos de comando detectar contoso.com. |

   SQL Server utiliza SSSD y NSS para asignar cuentas de usuario y grupos a los identificadores de seguridad (SID). SSSD debe estar configurado y en ejecución para SQL Server crear los inicios de sesión de AD correctamente. **realmd** normalmente lo hace automáticamente como parte de unirse al dominio, pero en algunos casos, debe hacerlo por separado.

   Para obtener más información, vea cómo [configuración manual de SSSD](https://access.redhat.com/articles/3023951), y [configurar NSS para trabajar con SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options).

1. Compruebe que ahora puede recopilar información acerca de un usuario del dominio y que puede adquirir un vale de Kerberos como ese usuario. En el ejemplo siguiente se usa **id**, [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html), y [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) comandos para esto.

   ```bash
   id user@contoso.com

   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM

   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   ```

   > [!NOTE]
   > - Si **id user@contoso.com**  devuelve, `No such user`, asegúrese de que el servicio SSSD ha iniciado correctamente ejecutando el comando `sudo systemctl status sssd`. Si el servicio se está ejecutando y siguen viendo el error, intente habilitar el registro detallado para SSSD. Para obtener más información, consulte la documentación de Red Hat para [solución de problemas de SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > - Si **kinit user@CONTOSO.COM**  devuelve, `KDC reply did not match expectations while getting initial credentials`, asegúrese de que especifica el dominio en mayúsculas.

Para obtener más información, consulte la documentación de Red Hat para [unirse a dominios de identidad y descubra](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html).

### <a id="option2"></a> Opción 2: Usar las utilidades de terceros openldap proveedor

Puede usar las utilidades de terceros, como [pbi](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), o [Centrify](https://www.centrify.com/). Este artículo no trata los pasos para cada utilidad individual. En primer lugar, debe usar una de estas utilidades para unir el host de Linux para SQL Server al dominio antes de continuar al día.  

SQL Server no utiliza código del integrador de sistemas de terceros o la biblioteca en todas las consultas relacionadas con AD. SQL Server siempre consulta AD mediante llamadas a bibliotecas de openldap directamente en esta configuración. Los integradores de sistemas de terceros solo se usan para unir el host de Linux al dominio de Active Directory y SQL Server no tiene ninguna comunicación directa con estas utilidades.

> [!IMPORTANT]
> Vea las recomendaciones para el uso de la **mssql-conf** `network.disablesssd` opción de configuración en el **opciones de configuración adicionales** sección del artículo [uso activo Autenticación de directorio con SQL Server en Linux](sql-server-linux-active-directory-authentication.md#additionalconfig).

Compruebe que su **/etc/krb5.conf** está configurado correctamente. Para la mayoría de los proveedores de Active Directory de terceros, esta configuración se realiza automáticamente. Sin embargo, comprobar **/etc/krb5.conf** para los valores siguientes evitar problemas futuros:

```/etc/krb5.conf
[libdefaults]
default_realm = CONTOSO.COM

[realms]
CONTOSO.COM = {
}

[domain_realm]
contoso.com = CONTOSO.COM
.contoso.com = CONTOSO.COM
```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>Compruebe que el DNS inverso está configurado correctamente

El siguiente comando debe devolver el nombre de dominio completo (FQDN) del host que ejecuta SQL Server. Un ejemplo es **SqlHost.contoso.com**.

```bash
host **<IP address of SQL Server host>**
```

El resultado de este comando debe ser similar a `**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`. Si este comando no devuelve el FQDN de su host, o si el FQDN no es correcto, agregue una entrada DNS inversa para SQL Server en el host de Linux al servidor DNS.

## <a name="next-steps"></a>Pasos siguientes

En este artículo se trata los requisitos previos de cómo configurar un servidor SQL Server en un equipo de host de Linux con la autenticación de Active Directory. Para finalizar la configuración de SQL Server en Linux para admitir cuentas de Active Directory, siga las instrucciones de [autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).