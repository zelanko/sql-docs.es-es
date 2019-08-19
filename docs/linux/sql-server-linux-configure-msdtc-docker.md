---
title: Procedimiento para usar transacciones distribuidas con SQL Server en Docker
description: En este artículo se explica cómo usar Microsoft DTC (Coordinador de transacciones distribuidas) para las transacciones distribuidas en un contenedor de SQL Server en Docker.
author: VanMSFT
ms.author: vanto
ms.date: 08/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e4d9d52541b6f9c9ca87bcbe4dc1db3c4448725c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770841"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>Procedimiento para usar transacciones distribuidas con SQL Server en Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo, se explica cómo configurar contenedores de SQL Server para Linux en Docker para realizar transacciones distribuidas.

Las imágenes de contenedor de SQL Server pueden usar Microsoft DTC (Coordinador de transacciones distribuidas), que es necesario para las transacciones distribuidas. Para comprender los requisitos de comunicaciones de MSDTC, vea [Procedimiento para configurar Microsoft DTC (Coordinador de transacciones distribuidas) en Linux](sql-server-linux-configure-msdtc.md). En este artículo, se explican los requisitos especiales y los escenarios relacionados con los contenedores de Docker de SQL Server.

## <a name="configuration"></a>Configuración

Para habilitar la transacción de MSDTC en contenedores para Docker, necesita establecer dos nuevas variables de entorno:

- **MSSQL_RPC_PORT**: el puerto TCP al que se enlaza el servicio del asignador de puntos de conexión de RPC y en el que escucha.  
- **MSSQL_DTC_TCP_PORT**: el puerto en el que se ha configurado el servicio MSDTC para escuchar.

### <a name="pull-and-run"></a>Extraer y ejecutar

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

En el ejemplo siguiente, se muestra cómo usar estas variables de entorno para extraer y ejecutar un único contenedor de SQL Server 2017 configurado para MSDTC. Esto le permite comunicarse con cualquier aplicación en cualquier host.

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=135" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 135:135 -p 51000:51000  `
   -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

En el ejemplo siguiente, se muestra cómo usar estas variables de entorno para extraer y ejecutar un único contenedor de SQL Server 2019 en versión preliminar configurado para MSDTC. Esto le permite comunicarse con cualquier aplicación en cualquier host.

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
```

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=135" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 135:135 -p 51000:51000  `
   -d mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
```

::: moniker-end

> [!IMPORTANT]
> El comando anterior solo funciona para Docker en Linux. Si ejecuta Docker en Windows, el host de Windows ya escucha en el puerto 135. Puede quitar el parámetro `-p 135:135` para Docker en Windows, pero esto tiene algunas limitaciones. El contenedor resultante no podrá usarse para transacciones distribuidas en las que participe el host; solo puede participar en transacciones distribuidas entre contenedores de Docker en el host.

En este comando, el servicio **Asignador de puntos de conexión de RPC** se ha enlazado al puesto 135, y el servicio **MSDTC** se ha enlazado al puerto 51000 en la red virtual de Docker. La comunicación de TDS de SQL Server se realiza en el puerto 1433 de la red virtual de Docker. Estos puertos se han expuesto externamente al host, como el puerto TDS 51433, el puerto 135 del asignador de puntos de conexión de RPC y el puerto 51000 de MSDTC.

> [!NOTE]
> El asignador de puntos de conexión de RPC y el puerto de MSDTC no tienen que coincidir en el host y en el contenedor. Por lo tanto, si el puerto del asignador de puntos de conexión de RPC se ha configurado en el puerto 135 del contenedor, podría asignarse al puerto 13501 o a cualquier otro puerto disponible en el servidor host.

## <a name="configure-the-firewall"></a>Configuración del firewall

Para comunicarse con el host y a través de este, también necesita configurar el firewall en el servidor host para los contenedores. En el firewall, abra todos los puertos donde el contenedor de Docker se exponga para las comunicaciones externas. En el ejemplo anterior, se usarían los puertos 135, 51433 y 51000. Estos son los puertos en el host en sí, y no los puertos a los que se asignan en el contenedor. Por lo tanto, si el puerto 51000 del asignador de puntos de conexión de RPC del contenedor se ha asignado al puerto de host 51001, el puerto 51001 (y no el puerto 51000) tiene que abrirse en el firewall para permitir la comunicación con el host.  

En el ejemplo siguiente, se muestra cómo crear estas reglas en Ubuntu.

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

En el ejemplo siguiente, se muestra cómo podría realizarse este procedimiento en Red Hat Enterprise Linux (RHEL):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>Configurar el enrutamiento de puertos en el host

En el ejemplo anterior, como un único contenedor de Docker asigna el puerto 135 de RPC al puerto 135 en el host, las transacciones distribuidas con el host tendrían que funcionar sin una configuración adicional. Tenga en cuenta que se puede usar directamente el puerto 135 en el contenedor, ya que SQL Server se ejecuta con privilegios elevados en un contenedor. Para SQL Server fuera de un contenedor, es necesario usar otro puerto efímero; además, el tráfico al puerto 135 tiene que enrutarse a ese puerto.

Pero, si asignó el puerto 135 del contenedor a otro puerto en el host (por ejemplo, 13500), necesita configurar el enrutamiento del puerto en el host. Esto permite al contenedor de Docker participar en transacciones distribuidas con el host y con otros servidores externos. Para obtener más información, vea [Configuración del enrutamiento de puertos](sql-server-linux-configure-msdtc.md#configure-port-routing).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre MSDTC en Linux, vea [Procedimiento para configurar Microsoft DTC (Coordinador de transacciones distribuidas) en Linux](sql-server-linux-configure-msdtc.md).
