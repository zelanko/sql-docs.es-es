---
title: Utilizar autenticación de Active Directory (Kerberos) cuando se conecta con las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft
description: Obtenga información acerca de cómo habilitar Kerberos para usar autenticación de Active Directory para las operaciones de SQL Studio (versión preliminar)
ms.custom: tools|sos
ms.date: 11/17/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.openlocfilehash: 46726247dc8540e67611173f6692ce092bb5be33
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>Conectar [!INCLUDE[name-sos](../includes/name-sos-short.md)] a SQL Server mediante la autenticación de Windows - Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] admite la conexión a SQL Server mediante Kerberos.

Para poder utilizar la autenticación integrada (autenticación de Windows) en Mac OS o Linux, debe configurar un **vale de Kerberos** vincular el usuario actual a una cuenta de dominio de Windows. 

## <a name="prerequisites"></a>Requisitos previos

- Acceso a un equipo unido a un dominio de Windows para consultar el controlador de dominio Kerberos.
- SQL Server debe configurarse para permitir la autenticación Kerberos. En el controlador de cliente que se ejecutan en Unix, la autenticación integrada solamente se admite con Kerberos. Puede encontrar más información sobre cómo configurar Sql Server para autenticar con Kerberos [aquí](https://support.microsoft.com/en-us/help/319723/how-to-use-kerberos-authentication-in-sql-server). Debería haber SPN registrados para cada instancia de Sql Server está intentando conectarse. Se muestran detalles acerca del formato de SPN de SQL Server [aquí](https://technet.microsoft.com/en-us/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Comprobando si Sql Server tiene la configuración de Kerberos

Inicie sesión en el equipo host de Sql Server. Línea de comandos de Windows, use la `setspn -L %COMPUTERNAME%` para enumerar todos los nombres de entidad de servicio para el host. Debería ver las entradas que comienzan por MSSQLSvc/HostName.Domain.com lo que significa que Sql Server se ha registrado un SPN y está listo para aceptar la autenticación Kerberos. 
- Si no tiene acceso al Host de Sql Server, desde cualquier otro sistema operativo Windows unido a Active Directory mismo, puede utilizar el comando `setspn -L <SQLSERVER_NETBIOS>` donde < SQLSERVER_NETBIOS > es el nombre de equipo del host de Sql Server.


## <a name="get-the-kerberos-key-distribution-center"></a>Obtener el centro de distribución de claves de Kerberos

Busque el valor de configuración de Kerberos KDC (Key Distribution Center). Ejecute el siguiente comando en un equipo de Windows que se ha unido al dominio de Active Directory: 

Iniciar `cmd.exe` y ejecute `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where “DOMAIN.COMPANY.COM” maps to your domain’s name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Copie el nombre de controlador de dominio que es el valor de configuración de KDC necesario, en este caso dc-33.domain.company.com

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Unirse a su sistema operativo para el controlador de dominio de Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

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

Ahora, compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al siguiente:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>Enterprise RedHat Linux
```bash
sudo yum install realmd krb5-workstation
```

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

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>MacOS

- Combine el macOS con el controlador de dominio de Active Directory [siguiendo estos pasos] (https://support.apple.com/kb/PH26282?viewlocale=en_US&locale=en_US).



## <a name="configure-kdc-in-krb5conf"></a>Configura el KDC en krb5.conf

Editar el `/etc/krb5.conf` en un editor de su elección. Configura las siguientes claves

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

A continuación, guarde el archivo krb5.conf y salir

> [!NOTE]
> Dominio debe estar en mayúsculas


## <a name="test-the-ticket-granting-ticket-retrieval"></a>Probar la recuperación de vale de concesión de vales

Obtener un vale de concesión de vales (TGT) de KDC.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Ver los vales disponibles mediante kinit. Si el kinit fue correcta, debería ver un vale. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>Conectar usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* Crear un nuevo perfil de conexión

* Elija **autenticación de Windows** como el tipo de autenticación

* Complete el perfil de conexión, haga clic en **conectar**

Después de conectarse correctamente, el servidor aparece en el *servidores* sidebar.
