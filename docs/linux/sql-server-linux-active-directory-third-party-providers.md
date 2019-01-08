---
title: Usar otros proveedores de Active Directory con SQL Server en Linux
titleSuffix: SQL Server
description: Este tutorial proporcionan los pasos de configuración para la autenticación de Active Directory con proveedores de terceros
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: de28696efd16a2be61864a810b3fd713b1066258
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160573"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Usar otros proveedores de Active Directory con SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un equipo de host de Linux con la autenticación de Active Directory cuando se usan proveedores de Active Directory de terceros. Algunos ejemplos son [PowerBroker Identity Services (pbi)](https://www.beyondtrust.com/), [una sola identidad](https://www.oneidentity.com/products/authentication-services/), y [Centrify](https://www.centrify.com/). Esta guía incluye los pasos para comprobar la configuración de Active Directory. No se ha diseñado para indicar cómo unir una máquina a un dominio. Para obtener instrucciones detalladas sobre cómo combinar una [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de host a un dominio con realmd y SSSD, consulte [autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de configurar la autenticación de Active Directory, deberá configurar un controlador de dominio de Active Directory, Windows, en la red. A continuación, unir su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en host de Linux a un dominio de Active Directory. Puede usar [pbi](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), o [Centrify](https://www.centrify.com/).

> [!NOTE]
>
>Este tutorial se usa **`contoso.com`** y **`CONTOSO.COM`** como nombres de dominio y del dominio de ejemplo, respectivamente. También usa **`DC1.CONTOSO.COM`** como el ejemplo de nombre de dominio del controlador de dominio completo. Debe reemplazar estos nombres con sus propios valores.

## <a name="check-the-connection-to-a-domain-controller"></a>Compruebe la conexión a un controlador de dominio

Compruebe que puede ponerse en contacto con el controlador de dominio con los nombres cortos y completos del dominio:

```bash
ping contoso

ping contoso.com
```

Si se produce un error en cualquiera de estas comprobaciones de nombre, actualice la lista de búsqueda de dominio:

- **Ubuntu**

  Editar la `/etc/network/interfaces` de archivos, por lo que es el dominio de Active Directory en la lista de búsqueda de dominio: 

  ```/etc/network/interfaces
  <...>
  # The primary network interface
  auto eth0
  iface eth0 inet dhcp
  dns-nameservers **<AD domain controller IP address>**
  dns-search **<AD domain name>**
  ```

  > [!NOTE]  
  > La interfaz de red **eth0**, podrían ser diferentes en distintos equipos. Para averiguar cuál de ellos usa, ejecute **ifconfig**. A continuación, copie la interfaz que tiene una dirección IP y los bytes transmitidos y recibidos.

  Después de editar este archivo, reinicie el servicio de red:

  ```bash
  sudo ifdown eth0 && sudo ifup eth0
  ```

  Ahora compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al ejemplo siguiente:  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

- **RHEL**

  Editar la `/etc/sysconfig/network-scripts/ifcfg-eth0` de archivos, por lo que es el dominio de Active Directory en la lista de búsqueda de dominio. O bien, edite el archivo de configuración de otra interfaz según corresponda:

  ```/etc/sysconfig/network-scripts/ifcfg-eth0
  <...>
  PEERDNS=no
  DNS1=**<AD domain controller IP address>**
  DOMAIN="contoso.com com"
  ```

  Después de editar este archivo, reinicie el servicio de red:

  ```bash
  sudo systemctl restart network
  ```

  Ahora compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al ejemplo siguiente:  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

  Si todavía no se puede hacer ping en el controlador de dominio, buscar el nombre de dominio completo y la dirección IP del controlador de dominio. Es un nombre de dominio de ejemplo `DC1.CONTOSO.COM`. Agregue la siguiente entrada al `/etc/hosts`:

  ```/etc/hosts
  **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
  ```

- **SLES**

  Editar el `/etc/sysconfig/network/config` archivo, para que la IP del controlador de dominio de Active Directory se utiliza para consultas DNS y el dominio de Active Directory está en la lista de búsqueda de dominio:

  ```/etc/sysconfig/network/config
  <...>
  NETCONFIG_DNS_STATIC_SEARCHLIST=""
  NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
  ```

  Después de editar este archivo, reinicie el servicio de red:

  ```bash
  sudo systemctl restart network
  ```

  Ahora compruebe que su `/etc/resolv.conf` archivo contiene una línea similar al ejemplo siguiente:

  ```/etc/resolv.conf
  search contoso.com com
  nameserver **<AD domain controller IP address>**
  ```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>Compruebe que el DNS inverso está configurado correctamente

El siguiente comando debe devolver el nombre de dominio completo del host que ejecuta SQL Server. Un ejemplo es **`SqlHost.contoso.com`**.

```bash
host **<IP address of SQL Server host>**
# **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
```

Si este comando no devuelve el FQDN de su host, o si el FQDN no es correcto, agregue una entrada DNS inversa para que es [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en host de Linux al servidor DNS.

## <a name="check-that-your-krb5-configuration-is-correct"></a>Compruebe que la configuración de KRB5 es correcta

Compruebe que su `/etc/krb5.conf` está configurado correctamente. Para la mayoría de los proveedores de Active Directory de terceros, esta configuración se realiza automáticamente. Sin embargo, comprobar `/etc/krb5.conf` para los valores siguientes evitar problemas futuros:

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

## <a name="next-steps"></a>Pasos siguientes

En este artículo se explica cómo configurar un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un equipo de host de Linux con la autenticación de Active Directory cuando se usan proveedores de Active Directory de terceros. Para finalizar la configuración [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para admitir cuentas de Active Directory, siga las instrucciones de [autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).

> [!div class="nextstepaction"]
> [Usar la autenticación de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> Puede omitir el **host Join de SQL Server al dominio de Active Directory** sección [autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md) como que acaba de hacer que en este tutorial.
