---
title: Conexión a SQL Server mediante autenticación de Windows (Kerberos)
description: Obtenga información sobre cómo conectar Azure Data Studio a SQL Server mediante la autenticación integrada de Microsoft Kerberos.
ms.prod: azure-data-studio
ms.technology: ''
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.topic: conceptual
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 325d066ec88045380c45dc2784e6766a4f549757
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411161"
---
# <a name="connect-azure-data-studio-to-your-sql-server-using-windows-authentication---kerberos"></a>Conexión de Azure Data Studio a SQL Server mediante autenticación de Windows: Kerberos

Azure Data Studio admite la conexión a SQL Server mediante Kerberos.

Para usar autenticación integrada (autenticación de Windows) en MacOS o Linux, debe configurar un **vale Kerberos** que vincule el usuario actual a una cuenta de dominio de Windows.

## <a name="prerequisites"></a>Requisitos previos

- Acceso a un equipo unido a dominio de Windows para consultar el controlador de dominio de Kerberos.
- SQL Server debe configurarse para permitir la autenticación Kerberos. En el caso del controlador de cliente que se ejecuta en Unix, la autenticación integrada solo se admite con Kerberos. Para más información, vea [Uso de la autenticación integrada de Kerberos para conectar con SQL Server](../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md). Debe haber SPN registrados para cada instancia de SQL Server a la que se esté intentando conectar. Para más información, vea [Registro de un nombre de entidad de servicio](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats).


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Comprobación de si SQL Server tiene configuración de Kerberos

Inicie sesión en el equipo host de SQL Server. Desde el símbolo del sistema de Windows, use `setspn -L %COMPUTERNAME%`para enumerar todos los nombres de entidad de seguridad de servicio del host. Debería ver las entradas que comienzan por MSSQLSvc/HostName.Domain.com, lo que significa que SQL Server ha registrado un SPN y está listo para aceptar la autenticación Kerberos. 
- Si no tiene acceso al host de SQL Server, desde cualquier otro sistema operativo Windows unido a la misma instancia de Active Directory, puede usar el comando `setspn -L <SQLSERVER_NETBIOS>`, donde <SQLSERVER_NETBIOS> es el nombre de equipo del host de SQL Server.


## <a name="get-the-kerberos-key-distribution-center"></a>Obtener el Centro de distribución de claves de Kerberos

Busque el valor de configuración del KDC (Centro de distribución de claves) de Kerberos. Ejecute el siguiente comando en un equipo Windows que esté unido al dominio de Active Directory: 

Inicie `cmd.exe` y ejecute `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Copie el nombre del controlador de dominio que sea el valor de configuración necesario del KDC, en este caso dc-33.domain.company.com.

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Unir el sistema operativo al controlador de dominio de Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

Edite el archivo `/etc/network/interfaces` para que la dirección IP del controlador de dominio de AD aparezca como dns-nameserver. Por ejemplo: 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> La interfaz de red (eth0) puede diferir en los distintos equipos. Para averiguar cuál es la que está usando, ejecute ifconfig y copie la interfaz que tiene una dirección IP y bytes transmitidos y recibidos.

Después de editar este archivo, reinicie el servicio de red:

```bash
sudo ifdown eth0 && sudo ifup eth0
```

Ahora compruebe que el archivo `/etc/resolv.conf` contiene una línea similar a la siguiente:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>RedHat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

Edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` (u otro archivo de configuración de interfaz que corresponda) para que la dirección IP del controlador de dominio de AD aparezca como un servidor DNS:

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

Después de editar este archivo, reinicie el servicio de red:

```bash
sudo systemctl restart network
```

Ahora compruebe que el archivo `/etc/resolv.conf` contiene una línea similar a la siguiente:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- Una el equipo macOS al controlador de dominio de Active Directory mediante estos pasos:



## <a name="configure-kdc-in-krb5conf"></a>Configuración de KDC en krb5.conf

Edite `/etc/krb5.conf` en el editor que prefiera. Configure las claves siguientes

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

Luego, guarde el archivo krb5.conf y salga.

> [!NOTE]
> El dominio debe estar en MAYÚSCULAS.


## <a name="test-the-ticket-granting-ticket-retrieval"></a>Prueba de la recuperación de un vale de concesión de vales

Obtenga un vale de concesión de vales (TGT) del KDC.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Vea los vales disponibles mediante klist. Si el comando kinit se ha ejecutado correctamente, debería ver un vale. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-azure-data-studio"></a>Conexión mediante Azure Data Studio

* Cree un nuevo perfil de conexión.

* Elija **Autenticación de Windows** como tipo de autenticación.

* Complete el perfil de conexión y haga clic en **Conectar**.

Después de conectar correctamente, el servidor aparece en la barra lateral *Servidores*.
