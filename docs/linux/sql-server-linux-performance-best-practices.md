---
title: Procedimientos recomendados para SQL Server en Linux | Microsoft Docs
description: En este artículo se proporcionan instrucciones y procedimientos recomendados para ejecutar SQL Server en Linux.
author: rgward
ms.author: bobward
manager: craigg
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: a9fdfb466f34e3eb40ad80d53c203f7ee8866f08
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51676912"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Procedimientos recomendados e instrucciones de configuración de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo proporcionan prácticas recomendadas y recomendaciones para maximizar el rendimiento de las aplicaciones de base de datos que se conectan a SQL Server en Linux. Estas recomendaciones son específicas que se ejecutan en la plataforma Linux. Todas las recomendaciones de SQL Server normales, como el diseño de índices, se siguen aplican.

Las instrucciones siguientes contienen recomendaciones para configurar SQL Server y el sistema operativo Linux.

## <a name="sql-server-configuration"></a>Configuración de SQL Server

Se recomienda realizar las siguientes tareas de configuración después de instalar a SQL Server en Linux para lograr un rendimiento mejor para su aplicación.

### <a name="best-practices"></a>Procedimientos recomendados

- **Usar la AFINIDAD de proceso para el nodo o la CPU**

   Se recomienda usar `ALTER SERVER CONFIGURATION` para establecer `PROCESS AFFINITY` para todos los **NUMANODEs** o las CPU que usa para SQL Server (que normalmente es para todos los nodos y CPU) en un sistema operativo de Linux. Afinidad del procesador le ayuda a mantener el comportamiento eficaz de Linux y la programación de SQL. Mediante el **NUMANODE** opción es el método más sencillo. Tenga en cuenta que debe usar **AFINIDAD de proceso** incluso si tiene un solo nodo NUMA en el equipo.  Consulte la [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) documentación para obtener más información sobre cómo establecer **AFINIDAD de proceso**.

- **Configurar varios archivos de datos de tempdb**

   Dado que un servidor SQL Server en la instalación de Linux no ofrece una opción para configurar varios archivos de tempdb, se recomienda que considere la posibilidad de crear tempdb varios archivos de datos después de la instalación. Para obtener más información, consulte las instrucciones en el artículo, [recomendaciones para reducir la contención de asignación en la base de datos de tempdb de SQL Server](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configuración avanzada

Las recomendaciones siguientes son valores de configuración opcionales que puede elegir realizar tras la instalación de SQL Server en Linux. Estas opciones se basan en los requisitos de su carga de trabajo y la configuración de su sistema operativo de Linux.

- **Establecer un límite de memoria con mssql-conf**

   Para asegurarse de que hay suficiente memoria física libre para el sistema operativo de Linux, el proceso de SQL Server usa sólo el 80% de la memoria RAM física de forma predeterminada. En algunos sistemas que gran cantidad de RAM física, el 20% podría ser un número significativo. Por ejemplo, en un sistema con 1 TB de RAM, la configuración predeterminada dejaría alrededor de 200 GB de RAM sin usar. En esta situación, es posible que desea configurar el límite de memoria en un valor superior. Consulte la documentación sobre la **mssql-conf** herramienta y el [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) configuración que controla la memoria visible para SQL Server (en unidades de MB).

   Al cambiar esta configuración, tenga cuidado de no establecer este valor demasiado alto. Si no deja suficiente memoria, puede experimentar problemas con el sistema operativo Linux y otras aplicaciones de Linux.

## <a name="linux-os-configuration"></a>Configuración del sistema operativo Linux

Considere el uso de las siguientes configuraciones del sistema operativo Linux para experimentar el mejor rendimiento para una instalación de SQL Server.

### <a name="kernel-settings-for-high-performance"></a>Configuraciones de kernel de alto rendimiento
Estos son los recomendados rendimiento relacionados con alta de configuración de sistema operativo Linux y el rendimiento para una instalación de SQL Server. Consulte la documentación del sistema operativo Linux para el proceso configurar estas opciones.



> [!Note]
> Para los usuarios de Red Hat Enterprise Linux (RHEL), el perfil de capacidad de rendimiento configurará esta configuración automáticamente (excepto para Estados de C).

En la tabla siguiente proporciona recomendaciones para la configuración de la CPU:

| Parámetro | Valor | Más información |
|---|---|---|
| Regulador de frecuencia de CPU | rendimiento | Consulte la **cpupower** comando |
| ENERGY_PERF_BIAS | rendimiento | Consulte la **x86_energy_perf_policy** comando |
| min_perf_pct | 100 | Consulte la documentación sobre el estado de p de intel |
| Estados de C | Sólo C1 | Consulte la documentación de Linux o sistema sobre cómo asegurarse de C-States está establecido en C1 solo |

En la tabla siguiente proporciona recomendaciones para la configuración de disco:

| Parámetro | Valor | Más información |
|---|---|---|
| lectura anticipada del disco | 4096 | Consulte la **blockdev** comando |
| configuración de sysctl | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>VM.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness=10 | Consulte la **sysctl** comando |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Kernel configuración automática numa equilibrio para sistemas de varios nodos NUMA

Si instala SQL Server en un nodo de múltiples **NUMA** sistemas, la siguiente **kernel.numa_balancing** kernel está habilitada de forma predeterminada. Para permitir que SQL Server para funcionar con la máxima eficacia en una **NUMA** system, deshabilitar automáticamente numa equilibrio en un sistema de varios nodo NUMA:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>Configuraciones de kernel para el espacio de direcciones virtuales

El valor predeterminado de **vm.max_map_count** (que es 65536) pueden no ser lo suficientemente alto como para una instalación de SQL Server. Cambie este valor (que es un límite superior) a 256K.

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Deshabilitar la última fecha/hora de acceso en sistemas de archivos para archivos de registro y datos de SQL Server

Use la **opción noatime tal** atributo con cualquier sistema de archivos que se usa para almacenar datos de SQL Server y los archivos de registro. Consulte la documentación de Linux sobre cómo establecer este atributo.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Deje transparente enorme páginas (THP) habilitado

La mayoría de las instalaciones de Linux deben tener esta opción en forma predeterminada. Se recomienda para que la experiencia de rendimiento más coherente dejar esta opción de configuración habilitada.

### <a name="swapfile"></a>archivo de intercambio

Asegúrese de que tener un archivo de intercambio configurado correctamente para evitar cualquier problemas de memoria insuficiente. Consulte la documentación de Linux para crear y ajustar correctamente el tamaño de un archivo de intercambio.

### <a name="virtual-machines-and-dynamic-memory"></a>Las máquinas virtuales y memoria dinámica

Si se ejecuta SQL Server en Linux en una máquina virtual, asegúrese de que seleccionar opciones para corregir la cantidad de memoria reservada para la máquina virtual. No use características como la memoria dinámica de Hyper-V.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de las características de SQL Server que mejoran el rendimiento, vea [empezar a trabajar con características de rendimiento](sql-server-linux-performance-get-started.md).

Para obtener más información acerca de SQL Server en Linux, consulte [información general de SQL Server en Linux](sql-server-linux-overview.md).
