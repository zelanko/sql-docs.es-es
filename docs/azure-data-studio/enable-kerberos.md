---
title: Usar autenticación de Active Directory (Kerberos) cuando se conecta con Azure Data Studio | Microsoft Docs
description: Obtenga información sobre cómo habilitar Kerberos usar autenticación de Active Directory para Azure Data Studio
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.openlocfilehash: 8bbd03d815594cfae850a94ae8067d37f0f5c744
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356327"
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>Conectar [!INCLUDE[name-sos](../includes/name-sos-short.md)] a SQL Server mediante la autenticación de Windows - Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] admite la conexión a SQL Server mediante Kerberos.

Para usar la autenticación integrada (autenticación de Windows) en macOS o Linux, deberá configurar un **vale de Kerberos** vincular el usuario actual a una cuenta de dominio de Windows. 

## <a name="prerequisites"></a>Requisitos previos

- Acceso a un equipo unido al dominio de Windows con el fin de consultar el controlador de dominio Kerberos.
- SQL Server debe configurarse para permitir la autenticación Kerberos. Para el controlador de cliente que se ejecutan en Unix, es sólo admite la autenticación integrada con Kerberos. Puede encontrar más información sobre cómo configurar Sql Server para autenticar con Kerberos [aquí](https://support.microsoft.com/en-us/help/319723/how-to-use-kerberos-authentication-in-sql-server). Debe haber un SPN registrados para cada instancia de Sql Server está intentando conectarse a. Se incluye información detallada sobre el formato del SPN de SQL Server [aquí](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Comprobando si Sql Server tiene la configuración de Kerberos

Inicie sesión en el equipo host de Sql Server. Línea de comandos de Windows, utilice el `setspn -L %COMPUTERNAME%` para enumerar todos los nombres de entidad de servicio para el host. Debería ver las entradas que comienzan por MSSQLSvc/HostName.Domain.com lo que significa que Sql Server ha registrado un SPN y está listo para aceptar la autenticación Kerberos. 
- Si no tiene acceso al Host de Sql Server y, después, desde cualquier otro SO de Windows unido al mismo Active Directory, puede utilizar el comando `setspn -L <SQLSERVER_NETBIOS>` donde < SQLSERVER_NETBIOS > es el nombre de equipo del host de Sql Server.


## <a name="get-the-kerberos-key-distribution-center"></a>Obtener el centro de distribución de claves de Kerberos

Busque el valor de configuración de KDC de Kerberos (Key Distribution Center). Ejecute el siguiente comando en un equipo de Windows que se une a su dominio de Active Directory: 

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

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Únase a su sistema operativo para el controlador de dominio de Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

Editar el `/etc/network/interfaces` archivo para que la dirección IP del controlador de dominio AD aparece como un servidor de nombres de dns. Por ejemplo: 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
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

Ahora compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al siguiente:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>Red Hat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

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

Ahora compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al siguiente:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- Combinar su macOS con el controlador de dominio de Active Directory siguiendo [estos pasos] (https://support.apple.com/kb/PH26282?viewlocale=en_US&locale=en_US).



## <a name="configure-kdc-in-krb5conf"></a>Configura el KDC en krb5.conf

Editar el `/etc/krb5.conf` en un editor que prefiera. Configure las claves siguientes

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

Obtenga un vale de concesión de vales (TGT) de KDC.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Ver los vales disponibles mediante kinit. Si el kinit se realizó correctamente, debería ver un vale. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>Conectar utilizando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* Crear un nuevo perfil de conexión

* Elija **Windows autenticación** como el tipo de autenticación

* Complete el perfil de conexión, haga clic en **Connect**

Después de conectarse correctamente, el servidor aparece en el *servidores* barra lateral.
