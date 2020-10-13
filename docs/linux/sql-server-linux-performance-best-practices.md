---
title: Procedimientos recomendados de rendimiento para SQL Server en Linux
description: En este artículo se ofrecen instrucciones y procedimientos recomendados para ejecutar SQL Server en Linux.
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 41ed6122e2ff75220d0fc45a75d4769804d0638c
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867219"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Procedimientos recomendados de rendimiento e instrucciones de configuración para SQL Server en Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

En este artículo se ofrecen procedimientos recomendados y recomendaciones para maximizar el rendimiento de las aplicaciones de base de datos que se conectan a SQL Server en Linux. Estas recomendaciones son específicas para la ejecución en la plataforma Linux. Se siguen aplicando todas las recomendaciones normales de SQL Server, como el diseño de índices.

Las instrucciones siguientes contienen recomendaciones para configurar SQL Server y el sistema operativo Linux.

## <a name="sql-server-configuration"></a>Configuración de SQL Server

Se recomienda realizar las siguientes tareas de configuración después de instalar SQL Server en Linux para lograr el mejor rendimiento de la aplicación.

### <a name="best-practices"></a>Procedimientos recomendados

- **Uso de PROCESS AFFINITY en el nodo o las CPU**

   Se recomienda usar `ALTER SERVER CONFIGURATION` para establecer `PROCESS AFFINITY` en todos los **NUMANODE** o las CPU que usa para SQL Server (que suele ser para todos los NODE y las CPU) en un sistema operativo Linux. La afinidad del procesador contribuye a mantener un comportamiento eficaz de programación de Linux y SQL. El uso de la opción **NUMANODE** es el método más sencillo. Tenga en cuenta que debe utilizar **PROCESS AFFINITY** aunque solo tenga un único nodo NUMA en el equipo.  Consulte la documentación de [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) para obtener más información sobre cómo establecer **PROCESS AFFINITY**.

- **Configuración de varios archivos de datos de tempdb**

   Dado que una instalación de SQL Server en Linux no ofrece una opción para configurar varios archivos de tempdb, se recomienda que se plantee la posibilidad de crear varios archivos de datos de tempdb después de la instalación. Para obtener más información, consulte las instrucciones del artículo [Recomendaciones para reducir la contención de asignación en la base de datos tempdb de SQL Server](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configuración avanzada

Las siguientes recomendaciones son valores de configuración opcionales que puede ejecutar tras la instalación de SQL Server en Linux. Estas opciones se basan en los requisitos de la carga de trabajo y la configuración del sistema operativo Linux.

- **Establecimiento de un límite de memoria con mssql-conf**

   Para asegurarse de que hay suficiente memoria física disponible para el sistema operativo Linux, el proceso de SQL Server solo utiliza de forma predeterminada el 80 % de la RAM física. En algunos sistemas con gran cantidad de RAM física, el 20 % puede ser una cantidad considerable. Por ejemplo, en un sistema con 1 TB de RAM, el valor predeterminado dejaría alrededor de 200 GB de RAM sin usar. En esta situación, es posible que quiera configurar el límite de memoria en un valor más alto. Consulte la documentación sobre la herramienta **mssql-conf** y la opción [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) que controla la memoria visible para SQL Server (en unidades de MB).

   Al cambiar esta opción, tenga cuidado de no establecer este valor demasiado alto. Si no deja suficiente memoria, podría experimentar problemas con el sistema operativo Linux y otras aplicaciones de Linux.

## <a name="linux-os-configuration"></a>Configuración del sistema operativo Linux

Plantéese utilizar las siguientes opciones de configuración del sistema operativo Linux para obtener el mejor rendimiento para una instalación de SQL Server.

### <a name="kernel-settings-for-high-performance"></a>Configuración de kernel para alto rendimiento
Se trata de la configuración recomendada del sistema operativo Linux relacionada con el alto rendimiento de una instalación de SQL Server. Consulte la documentación del sistema operativo Linux para obtener información sobre el proceso de configuración de estas opciones.



> [!Note]
> En el caso de los usuarios de Red Hat Enterprise Linux (RHEL), el perfil de rendimiento [optimizado](https://tuned-project.org) configura de forma automática estas opciones (excepto para C-States). A partir de RHEL 8.0, se ha desarrollado un perfil de mssql /usr/lib/tuned integrado conjuntamente con Red Hat y ofrece optimizaciones relacionadas con el rendimiento de Linux más precisas para cargas de trabajo de SQL Server. Este perfil incluye el perfil de rendimiento de RHEL y a continuación se presentan sus definiciones para que las revise con otras distribuciones de Linux y versiones de RHEL sin este perfil.

En la tabla siguiente se proporcionan recomendaciones para la configuración de la CPU:

| Configuración | Value | Más información |
|---|---|---|
| Regulador de frecuencia de CPU | rendimiento | Consulte el comando **cpupower**. |
| ENERGY_PERF_BIAS | rendimiento | Consulte el comando **x86_energy_perf_policy**. |
| min_perf_pct | 100 | Consulte la documentación sobre Intel P-state. |
| C-States | Solo C1 | Consulte la documentación del sistema o de Linux para saber cómo asegurarse de que C-States solo se establece en C1 |

En la tabla siguiente se proporcionan recomendaciones para la configuración del disco:

| Configuración | Value | Más información |
|---|---|---|
| lectura anticipada del disco | 4096 | Consulte el comando **blockdev**. |
| configuración de sysctl | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 10 | Consulte el comando **sysctl**. |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Configuración del equilibrio automático de NUMA del kernel con sistemas NUMA de varios nodos

Si instala SQL Server en sistemas **NUMA** de varios nodos, la configuración de kernel **kernel.numa_balancing** está habilitada de forma predeterminada. Para permitir que SQL Server funcione con la máxima eficacia en un sistema **NUMA**, deshabilite el equilibrio automático de NUMA en un sistema NUMA de varios nodos:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>Configuración del kernel para el espacio de direcciones virtuales

Es posible que la configuración predeterminada de **vm.max_map_count** (que es 65536) no sea lo suficientemente alta para una instalación SQL Server. Por este motivo, cambie el valor de **vm.max_map_count** a 262144 para una implementación de SQL Server y consulte la sección [Configuración propuesta de Linux mediante un perfil mssql optimizado](#proposed-linux-settings-using-a-tuned-mssql-profile) para realizar ajustes adicionales en estos parámetros de kernel. El valor máximo de vm.max_map_count es 2147483647.

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="proposed-linux-settings-using-a-tuned-mssql-profile"></a>Configuración propuesta de Linux mediante un perfil mssql optimizado

```bash
#
# A tuned configuration for SQL Server on Linux
#
    
[main]
summary=Optimize for Microsoft SQL Server
include=throughput-performance
    
[cpu]
force_latency=5

[sysctl]
vm.swappiness = 1
vm.dirty_background_ratio = 3
vm.dirty_ratio = 80
vm.dirty_expire_centisecs = 500
vm.dirty_writeback_centisecs = 100
vm.transparent_hugepages=always
# For multi-instance SQL deployments, use
# vm.transparent_hugepages=madvise
vm.max_map_count=1600000
net.core.rmem_default = 262144
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048576
kernel.numa_balancing=0
kernel.sched_latency_ns = 60000000
kernel.sched_migration_cost_ns = 500000
kernel.sched_min_granularity_ns = 15000000
kernel.sched_wakeup_granularity_ns = 2000000
```

Para habilitar este perfil optimizado, guarde estas definiciones en un archivo **tuned.conf** en una carpeta /usr/lib/tuned/mssql y habilite el perfil mediante

```bash
chmod +x /usr/lib/tuned/mssql/tuned.conf
tuned-adm profile mssql
```

Compruebe que se habilita con

```bash
tuned-adm active
```
o
```bash
tuned-adm list
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Deshabilitación de la última fecha y hora de acceso en los sistemas de archivos para los archivos de datos y de registro de SQL Server

Use el atributo **noatime** con cualquier sistema de archivos que se use para almacenar archivos de datos y de registro de SQL Server. Consulte la documentación de Linux para obtener información sobre cómo establecer este atributo.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Habilitación de Transparent Huge Pages (THP)

La mayoría de las instalaciones de Linux deben tener esta opción activada de forma predeterminada. Se recomienda que, para obtener un rendimiento más coherente, deje habilitada esta opción de configuración. Pero, por ejemplo, en el caso de una actividad de paginación de memoria alta en implementaciones de SQL Server con varias instancias o la ejecución de SQL Server con otras aplicaciones que requieren mucha memoria del servidor, se recomienda probar el rendimiento de las aplicaciones después de ejecutar el comando siguiente 

```bash
echo madvise > /sys/kernel/mm/transparent_hugepage/enabled
```
o bien, modificar el perfil optimizado de mssql con la línea

```bash
vm.transparent_hugepages=madvise
```
y activarlo después de la modificación.
```bash
tuned-adm off
tuned-adm profile mssql
```

### <a name="swapfile"></a>Archivo de intercambio

Asegúrese de que tiene un archivo de intercambio configurado correctamente para evitar problemas de memoria insuficiente. Consulte la documentación de Linux para obtener información sobre cómo crear y ajustar correctamente el tamaño de un archivo de intercambio.

### <a name="virtual-machines-and-dynamic-memory"></a>Virtual Machines y Memoria dinámica

Si ejecuta SQL Server en Linux en una máquina virtual, asegúrese de seleccionar opciones para corregir la cantidad de memoria reservada para la máquina virtual. No use características como Memoria dinámica de Hyper-V.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre características de SQL Server que mejoran el rendimiento, consulte [Introducción a las características de rendimiento](sql-server-linux-performance-get-started.md).

Para obtener más información sobre SQL Server en Linux, consulte [Introducción a SQL Server en Linux](sql-server-linux-overview.md).
