---
title: Cómo configurar MSDTC en Linux | Microsoft Docs
description: Este artículo proporciona un tutorial para configurar MSDTC en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 127f39075a1b84b1250a27003efeb28083d1adbd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513187"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC) en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describe cómo configurar el Coordinador de transacciones distribuidas de Microsoft (MSTDC) en Linux. Compatibilidad MSDTC en Linux se introdujo en la versión preliminar de SQL Server 2019.

## <a name="overview"></a>Información general

Se habilitan las transacciones distribuidas en SQL Server en Linux mediante la introducción de MSDTC y RPC funcionalidad del asignador de extremos dentro de SQL Server. De forma predeterminada, un proceso de asignación de extremos RPC escucha en el puerto 135 para las solicitudes RPC entrantes y enruta a los componentes adecuados (por ejemplo, el servicio MSDTC). Un proceso requiere privilegios de superusuario para enlazar a puertos conocidos (números de puerto inferiores al 1024) en Linux. Para evitar el inicio de SQL Server con privilegios de raíz para el proceso RPC endpoint mapper, los administradores del sistema deben usar iptables para crear la traducción NAT para enrutar el tráfico en el puerto 135 al proceso de asignación de extremos RPC de SQL Server.

SQL Server 2019 presenta dos parámetros de configuración de la utilidad mssql-conf.

| configuración de MSSQL-conf | Descripción |
|---|---|
| **Network.rpcport** | El puerto TCP que se enlaza al proceso del asignador de extremos RPC. |
| **Network.servertcpport** | El puerto que escucha el servidor MSDTC. Si no se establece, el servicio MSDTC usa un puerto efímero aleatorio en el reinicio del servicio y las excepciones del firewall se deberán volver a configurar para asegurarse de que el servicio MSDTC puede continuar la comunicación. |

Para obtener más información acerca de estas opciones y otras opciones de MSDTC relacionados, consulte [configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md#msdtc).

## <a name="supported-msdtc-configurations"></a>Configuraciones admitidas de MSDTC

Se admiten las siguientes configuraciones de MSDTC:

- OLE TX transacciones distribuidas en SQL Server en Linux para proveedores de ODBC y JDBC.
- Transacciones distribuidas XA se establecen en SQL Server en Linux mediante proveedores de JDBC.
- Transacciones distribuidas en el servidor vinculado.

Para conocer limitaciones y problemas conocidos de MSDTC en versión preliminar, consulte [notas de versión preliminar de SQL Server 2019 en Linux](sql-server-linux-release-notes-2019.md#msdtc).

## <a name="msdtc-configuration-steps"></a>Pasos de configuración de MSDTC

Hay tres pasos para configurar la funcionalidad y la comunicación de MSDTC. Si no se realizan los pasos de configuración necesarios, SQL Server no habilitar la funcionalidad MSDTC.

- Configurar **network.rpcport** y **distributedtransaction.servertcpport** con mssql-conf.
- Configurar el firewall para permitir la comunicación en **rpcport**, **servertcpport**y el puerto 135.
- Configurar el enrutamiento del servidor de Linux para que la comunicación de RPC en el puerto 135 se redirige a SQL Server **network.rpcport**.

Las secciones siguientes proporcionan instrucciones detalladas para cada paso.

## <a name="configure-rpc-and-msdtc-ports"></a>Configurar puertos RPC y MSDTC

En primer lugar, configure **network.rpcport** y **distributedtransaction.servertcpport** con mssql-conf.

1. Use mssql-conf para establecer el **network.rpcport** valor. El ejemplo siguiente establece en 13500.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. Establecer el **distributedtransaction.servertcpport** valor. El ejemplo siguiente establece en 51999.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. Reinicie SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>Configuración del firewall

El último paso es configurar el firewall para permitir la comunicación en **rpcport**, **servertcpport**y el puerto 135.  Esto permite que el proceso MSDTC para comunicarse externamente a otros administradores de transacciones y los coordinadores y el proceso de asignación de extremos RPC. Los pasos reales para esto variará dependiendo de la distribución de Linux y el firewall. 

El ejemplo siguiente muestra cómo crear estas reglas en Ubuntu.

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

El ejemplo siguiente muestra cómo esto puede realizarse en Red Hat Enterprise Linux (RHEL):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

Es importante configurar el firewall antes de configurar el enrutamiento del puerto en la sección siguiente. Actualizar el firewall puede borrar las reglas de enrutamiento de puerto en algunos casos.

## <a name="configure-port-routing"></a>Configurar el enrutamiento de puerto

Configurar la tabla de enrutamiento del servidor de Linux para que la comunicación de RPC en el puerto 135 se redirige a SQL Server **network.rpcport**. Mecanismo de configuración de puertos reenvío en distribución diferentes puede diferir. En las distribuciones que no usan servicios firewalld, las reglas de iptable son un mecanismo eficaz para lograr esto. Ejemplo de este tipo distrubution son Ubuntu 16.04 y v12 SUSE Enterprise Linux. Las reglas de iptable pueden no conservarse durante los reinicios, por lo que los siguientes comandos también proporcionan instrucciones para restaurar las reglas tras un reinicio.

1. Crear reglas de enrutamiento para el puerto 135. En el ejemplo siguiente, se dirige el puerto 135 para el puerto RPC, 13500, definido en la sección anterior. Reemplace `<ipaddress>` con la dirección IP del servidor.

   ```bash
   iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   El `--comment RpcEndPointMapper` ayuda de parámetro en los comandos anteriores con la administración de estas reglas en comandos posteriores.

2. Ver las reglas de enrutamiento que creó con el siguiente comando:

   ```bash
   iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. Guardar las reglas de enrutamiento en un archivo en el equipo.

   ```bash
   iptables-save > /etc/iptables.conf
   ```

4. Para volver a cargar las reglas tras un reinicio, agregue el siguiente comando para `/etc/rc.local` (para Ubuntu o RHEL) o a `/etc/init.d/after.local` (para SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

El **iptables guardar** y **iptables restauración** comandos proporcionan un mecanismo básico para guardar y restaurar las entradas de iptables. Según la distribución de Linux, hay podría ser más avanzadas o automatizar las opciones disponibles. Por ejemplo, es una alternativa de Ubuntu la **iptables persistente** paquete para realizar entradas persistente. 

En las distribuciones que utilizan service firewalld, el mismo servicio puede utilizarse para ambos apertura del puerto en el servidor y el reenvío de puerto interno. Por ejemplo, en Red Hat Enterprise Linux, debe usar el servicio de firewalld (a través de la utilidad de configuración del firewall cmd-agregar-reenviar-puerto u opciones similares) para crear y administrar las reglas en lugar de usar iptables de reenvío de puerto persistente.

```bash
firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
```

> [!IMPORTANT]
> Los pasos anteriores suponen una dirección IP fija. Si cambia la dirección IP para la instancia de SQL Server (debido a una intervención manual o DHCP), debe quitar y volver a crear las reglas de enrutamiento si se hubieran creado con iptables. Si necesita volver a crear o eliminar reglas de enrutamiento existentes, puede usar el siguiente comando para quitar el antiguo `RpcEndPointMapper` reglas:
> 
> ```bash
> iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

## <a name="verify"></a>Verify

En este momento, SQL Server debe ser capaz de participar en transacciones distribuidas. Para comprobar que SQL Server está escuchando, ejecute el **netstat** comando (si usa RHEL, es posible que deba instalar primero el **net-tools** paquete):

```bash
sudo netstat -tulpn | grep sqlservr
```

Debería ver resultados similares al siguiente:

```bash
tcp 0 0 0.0.0.0:1433 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 127.0.0.1:1434 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:13500 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:51999 0.0.0.0:* LISTEN 13911/sqlservr
tcp6 0 0 :::1433 :::* LISTEN 13911/sqlservr
tcp6 0 0 ::1:1434 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::13500 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::51999 :::* LISTEN 13911/sqlservr
```

Sin embargo, después del reinicio, SQL Server no se inicia la escucha en el **servertcpport** hasta que la primera transacción distribuida. En este caso, no vería escuchando en el puerto 51999 en este ejemplo hasta la primera transacción distribuida de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server en Linux, consulte [SQL Server en Linux](sql-server-linux-overview.md).
