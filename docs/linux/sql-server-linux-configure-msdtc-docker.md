---
title: Cómo usar transacciones distribuidas con SQL Server en Docker | Microsoft Docs
description: Este artículo explica cómo usar Dprovides un tutorial para configurar MSDTC en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 3242f0d074dc3c2f33fc83de4604a20bfdcbd64a
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049415"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>Cómo usar transacciones distribuidas con SQL Server en Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo configurar SQL Server en Docker para las transacciones distribuidas.

A partir de la versión preliminar de SQL Server 2019, imágenes de contenedor admiten la Microsoft distribuida (Coordinador de transacciones) necesarios para las transacciones distribuidas. Para comprender los requisitos de las comunicaciones de MSDTC, vea [cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC) en Linux](sql-server-linux-configure-msdtc.md). En este artículo se explica los requisitos especiales y escenarios relacionados con los contenedores de Docker de SQL Server.

## <a name="configuration"></a>Configuración

Para habilitar la transacción de MSDTC en contenedores de docker, debe establecer dos nuevas variables de entorno:

- **MSSQL_RPC_PORT**: el puerto TCP que el servicio de asignador de extremos de RPC se enlaza a y escucha en el.  
- **MSSQL_DTC_TCP_PORT** el puerto que el servicio MSDTC está configurado para escuchar en.

### <a name="pull-and-run"></a>Extraer y ejecutar

El ejemplo siguiente muestra cómo usar estas variables de entorno para extraer y ejecutar un contenedor configurado para MSDTC. Esto le permite comunicarse con cualquier aplicación en todos los hosts.

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=13500' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 13500:13500 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

El comando siguiente muestra el mismo comando de Docker en Windows en PowerShell:

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=13500" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 13500:13500 -p 51000:51000 `
   -d "mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu"
```

En este comando, el **Endpoint Mapper de RPC** service se ha enlazado al puerto 13500 y el **MSDTC** servicio se ha enlazado al puerto 51000 dentro de la red virtual de docker. Se produce comunicación TDS de SQL Server en el puerto 1433 dentro de la red virtual de docker. Se han expuesto externamente estos puertos al host como puerto TDS 51433, puerto de asignador de extremos RPC 13500 y puerto 51000 de MSDTC.

> [!NOTE]
> El Endpoint Mapper de RPC y el puerto MSDTC no es necesario que sea el mismo en el host y el contenedor. Por lo que aunque puerto Endpoint Mapper de RPC se ha configurado para ser 13500 en contenedor, potencialmente podría asignarse para el puerto 13501 o cualquier otro puerto disponible en el servidor host.

## <a name="configure-the-firewall"></a>Configuración del firewall

Para poder comunicarse y a través del host, también debe configurar el firewall en el servidor de host para los contenedores. Abra el firewall para todos los puertos que docker contenedor expone para la comunicación externa. En el ejemplo anterior, esto sería puertos 135, 51433 y 51000. Estos son los puertos en el propio host y no los puertos que se asignan en el contenedor. Por lo tanto, si se asigna el puerto de asignador 51000 del contenedor al puerto de host 51001, un punto de conexión de RPC, a continuación, el puerto 51001 (no 51000) se debe abrir en el firewall para la comunicación con el host.  

El ejemplo siguiente muestra cómo crear estas reglas en Ubuntu.

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

El ejemplo siguiente muestra cómo esto puede realizarse en Red Hat Enterprise Linux (RHEL):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>Configurar el enrutamiento de puerto en el host

Si el contenedor de docker participa en transacciones distribuidas con un servidor fuera del host, debe configurar el host de enrutamiento del puerto. Para obtener más información, consulte [configurar el enrutamiento de puerto](sql-server-linux-configure-msdtc.md#configure-port-routing).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de MSDTC en Linux, consulte [cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC) en Linux](sql-server-linux-configure-msdtc.md).