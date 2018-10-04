---
title: Usar otros proveedores de Active Directory con SQL Server en Linux | Microsoft Docs
description: Este tutorial proporcionan los pasos de configuración para la autenticación de AD con proveedores de terceros
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: beb342156098ebb5516466ad7fd4a771cc5a0616
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787303"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Usar otros proveedores de Active Directory con SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo de host de Linux con la autenticación de Active Directory cuando se usan proveedores de AD de otros fabricantes, como [PowerBroker Identity Services (pbi)](https://www.beyondtrust.com/), [Vintela Authentication Services (VAS)](https://www.oneidentity.com/products/authentication-services/), y [Centrify](https://www.centrify.com/). Esta guía incluye los pasos para comprobar la configuración de AD y no está pensado para indicar cómo unir una máquina a un dominio. Para obtener instrucciones detalladas sobre cómo combinar una [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host a un dominio con el dominio KERBEROS y SSSD, consulte [autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de configurar la autenticación de AD, deberá configurar un controlador de dominio de AD (Windows) en la red y combinación su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en host de Linux a un dominio de AD. Puede usar [pbi](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), o [Centrify](https://www.centrify.com/).

> [!NOTE]
>
>Este tutorial usa "contoso.com" y "CONTOSO.COM" como nombres de dominio y el dominio Kerberos de ejemplo, respectivamente. También usa "DC1. "CONTOSO.COM" como el nombre de dominio completo del ejemplo del controlador de dominio. Debe reemplazar estos elementos con sus propios valores.

## <a name="check-connection-to-domain-controller"></a>Compruebe la conexión al controlador de dominio

Compruebe que puede ponerse en contacto con el controlador de dominio con el nombre corto y completo del dominio.

   ```bash
   ping contoso

   ping contoso.com
   ```

   Si se produce un error en cualquiera de estos, actualice la lista de búsqueda de dominio.

   - **Ubuntu**:

     Editar el `/etc/network/interfaces` archivo para que el dominio de AD está en la lista de búsqueda de dominio: 

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
     search contoso.com com  
     nameserver **<AD domain controller IP address>**
     ```

   - **RHEL**:

     Editar el `/etc/sysconfig/network-scripts/ifcfg-eth0` archivo (o en otra configuración de interfaz de archivos según corresponda) para que sea su dominio de AD en la lista de búsqueda de dominio:

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

   Si todavía no se puede hacer ping en el controlador de dominio, buscar el nombre de dominio completo (por ejemplo, DC1. CONTOSO.COM) y la dirección IP del controlador de dominio y agregue la siguiente entrada al `/etc/hosts`

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

   - **SLES**:

     Editar el `/etc/sysconfig/network/config` archivo para que la IP del controlador de dominio de AD se usará para las consultas DNS y el dominio de AD está en la lista de búsqueda de dominio:

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

## <a name="check-reverse-dns-is-properly-configured"></a>Comprobación de que DNS inverso está configurado correctamente

El siguiente comando debe devolver el nombre de dominio completo del host que ejecuta SQL Server (p. ej. "SqlHost.contoso.com").

   ```bash
   host **<IP address of SQL Server host>**
   # **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
   ```

   Si esto no devuelve el FQDN de su host o el FQDN no es correcto, agregue una entrada DNS inversa para su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en host de Linux al servidor DNS.

## <a name="check-your-krb5-configuration-is-correct"></a>Compruebe que la configuración de KRB5 es correcta

Compruebe su `/etc/krb5.conf` está configurado correctamente. Para la mayoría de los proveedores de AD de otros fabricantes, esto se hace automáticamente. Sin embargo, comprobar `/etc/krb5.conf` para los valores siguientes evitar problemas futuros:

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

En este artículo, describimos cómo configurar un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo host de Linux con la autenticación de Active Directory cuando se usan proveedores de AD de otros fabricantes. Para finalizar la configuración [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para admitir cuentas de AD, siga las instrucciones de [autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).

> [!div class="nextstepaction"]
> [Usar la autenticación de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> Puede omitir la sección "Host de la combinación SQL Server al dominio de AD" en [autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md) como que acaba de hacer que en este tutorial.
