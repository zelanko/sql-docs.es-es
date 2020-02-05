---
title: Procedimientos recomendados de rendimiento para SQL Server en Linux
description: En este artículo se ofrecen instrucciones y procedimientos recomendados para ejecutar SQL Server en Linux.
author: rgward
ms.author: bobward
ms.reviewer: vanto
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 543488eada46a088f3c634ce2326c7e2db2a97a5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68105440"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Procedimientos recomendados de rendimiento e instrucciones de configuración para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

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
> En el caso de los usuarios de Red Hat Enterprise Linux (RHEL), el perfil de rendimiento configurará automáticamente estas opciones (excepto para C-States).

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

Es posible que la configuración predeterminada de **vm.max_map_count** (que es 65536) no sea lo suficientemente alta para una instalación SQL Server. Cambie este valor (que es un límite superior) a 256 KB.

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Deshabilitación de la última fecha y hora de acceso en los sistemas de archivos para los archivos de datos y de registro de SQL Server

Use el atributo **noatime** con cualquier sistema de archivos que se use para almacenar archivos de datos y de registro de SQL Server. Consulte la documentación de Linux para obtener información sobre cómo establecer este atributo.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Habilitación de Transparent Huge Pages (THP)

La mayoría de las instalaciones de Linux deben tener esta opción activada de forma predeterminada. Se recomienda que, para obtener un rendimiento más coherente, deje habilitada esta opción de configuración.

### <a name="swapfile"></a>Archivo de intercambio

Asegúrese de que tiene un archivo de intercambio configurado correctamente para evitar problemas de memoria insuficiente. Consulte la documentación de Linux para obtener información sobre cómo crear y ajustar correctamente el tamaño de un archivo de intercambio.

### <a name="virtual-machines-and-dynamic-memory"></a>Virtual Machines y Memoria dinámica

Si ejecuta SQL Server en Linux en una máquina virtual, asegúrese de seleccionar opciones para corregir la cantidad de memoria reservada para la máquina virtual. No use características como Memoria dinámica de Hyper-V.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre características de SQL Server que mejoran el rendimiento, consulte [Introducción a las características de rendimiento](sql-server-linux-performance-get-started.md).

Para obtener más información sobre SQL Server en Linux, consulte [Introducción a SQL Server en Linux](sql-server-linux-overview.md).
