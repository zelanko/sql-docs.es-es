---
title: "Prácticas recomendadas de rendimiento para SQL Server en Linux | Documentos de Microsoft"
description: En este tema se proporcionan instrucciones y procedimientos recomendados para ejecutar SQL Server 2017 en Linux.
author: rgward
ms.author: bobward
manager: jhubbard
ms.date: 09/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 18d40800ee74783b0ce3df4d9d4e0458fbb72ebb
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---

# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-2017-on-linux"></a>Prácticas recomendadas de rendimiento y directrices de configuración para SQL Server 2017 en Linux

Este tema proporciona prácticas recomendadas y recomendaciones para maximizar el rendimiento para aplicaciones de base de datos que se conectan a SQL Server en Linux. Estas recomendaciones son específicas para ejecutar en la plataforma Linux. Todas las recomendaciones normales de SQL Server, como el diseño de índices, se siguen aplican.

Las instrucciones siguientes contienen recomendaciones para configurar SQL Server y el sistema operativo Linux.

## <a name="sql-server-configuration"></a>Configuración de SQL Server

Se recomienda realizar las siguientes tareas de configuración después de instalar a SQL Server en Linux para lograr un rendimiento óptimo para la aplicación.

### <a name="best-practices"></a>Procedimientos recomendados

- **Utilizar la AFINIDAD de proceso para el nodo o CPU**

   Se recomienda usar `ALTER SERVER CONFIGURATION` para establecer `PROCESS AFFINITY` para todos los **NUMANODEs** o CPU que usa para SQL Server (que normalmente es para todos los nodos y CPU) en un sistema operativo de Linux. Afinidad del procesador le ayuda a mantener el comportamiento eficaz de Linux y la programación de SQL. Mediante el **NUMANODE** opción es el método más sencillo. Tenga en cuenta que debe usar **AFINIDAD de proceso** incluso si tiene un solo nodo NUMA en el equipo.  Consulte la [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) documentación para obtener más información sobre cómo establecer **AFINIDAD de proceso**.

- **Configurar varios archivos de datos de tempdb**

   Dado que un servidor SQL Server en la instalación de Linux no ofrece una opción para configurar varios archivos de tempdb, se recomienda que considere la posibilidad de crear tempdb varios archivos de datos después de la instalación. Para obtener más información, consulte las instrucciones del artículo [recomendaciones para reducir la contención de asignación en la base de datos de tempdb de SQL Server](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Configuración avanzada

Las recomendaciones siguientes son los valores de configuración opcionales que es posible que decida realizar después de la instalación de SQL Server en Linux. Estas opciones se basan en los requisitos de la carga de trabajo y la configuración de su sistema operativo de Linux.

- **Establecer un límite de memoria con mssql-conf**

   Para asegurarse de que hay suficiente memoria física libre para el sistema operativo de Linux, el proceso de SQL Server utiliza sólo el 80% de la RAM física de forma predeterminada. En algunos sistemas que gran cantidad de RAM física, el 20% podría ser un número significativo. Por ejemplo, en un sistema con 1 TB de RAM, el valor predeterminado se excluirán aproximadamente 200 GB de RAM sin usar. En esta situación, puede configurar el límite de memoria en un valor más alto. Vea la documentación sobre la **mssql-conf** herramienta y la [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) configuración que controla la memoria visible para SQL Server (en unidades de MB).

   Al cambiar este valor, tenga cuidado de no establecer este valor demasiado alto. Si no deja suficiente memoria, puede experimentar problemas con el sistema operativo Linux y otras aplicaciones de Linux.

## <a name="linux-os-configuration"></a>Configuración del sistema operativo Linux

Considere el uso de las siguientes opciones de configuración de sistema operativo Linux para experimentar un rendimiento óptimo con una instalación de SQL Server.

### <a name="kernel-settings-for-high-performance"></a>Configuración de kernel de alto rendimiento

Estos son los recomendados rendimiento relacionados con el máximo de configuración de sistema operativo Linux y rendimiento para una instalación de SQL Server. Consulte la documentación del sistema operativo Linux para el proceso configurar estas opciones.



> [!Note]
> Para los usuarios de Red Hat Enterprise Linux (RHEL), el perfil de rendimiento de rendimiento configurará esta configuración automáticamente (a excepción de C-estados).

En la tabla siguiente proporciona recomendaciones para la configuración de la CPU:

| Configuración | Valor | Más información |
|---|---|---|
| Regulador de frecuencia de CPU | rendimiento | Consulte la **cpupower** comando |
| ENERGY_PERF_BIAS | rendimiento | Consulte la **x86_energy_perf_policy** comando |
| min_perf_pct | 100 | Consulte la documentación de intel p-estado |
| Estados de C | Sólo C1 | Consulte la documentación de Linux o sistema acerca de cómo comprobar estados C está establecido en C1 solo |

En la tabla siguiente proporciona recomendaciones para la configuración de disco:

| Configuración | Valor | Más información |
|---|---|---|
| lectura anticipada de disco | 4096 | Consulte la **blockdev** comando |
| configuración de sysctl | kernel.sched_min_granularity_ns = 10000000.<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>VM.dirty_ratio = 40<br/>VM.dirty_background_ratio = 10<br/>VM.swappiness=10 | Consulte la **sysctl** comando |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Kernel configuración automática numa equilibrio para sistemas de varios nodos NUMA

Si instala SQL Server en un nodo varios **NUMA** sistemas, la siguiente **kernel.numa_balancing** kernel está habilitada de forma predeterminada. Para permitir que SQL Server para que funcione con la máxima eficacia en un **NUMA** sistema, deshabilitar automáticamente numa equilibrio en un sistema de varios nodo NUMA:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>Configuración de kernel para el espacio de direcciones virtuales

El valor predeterminado de **vm.max_map_count** (que es 65536) pueden no ser lo suficientemente alto como para una instalación de SQL Server. Cambie este valor (que es un límite superior) a 256K.

```bash
sysctl -w vm.max_map_count 262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Deshabilitar la última fecha/hora de acceso en sistemas de archivos para archivos de registro y datos de SQL Server

Use la **noatime** atributo con cualquier sistema de archivos que se usa para almacenar datos de SQL Server y los archivos de registro. Consulte la documentación de Linux sobre cómo establecer este atributo.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Deje transparente enorme páginas (THP) habilitado

La mayoría de las instalaciones de Linux deben tener esta opción en de forma predeterminada. Se recomienda para que la experiencia de rendimiento más coherente dejar esta opción de configuración habilitada.

### <a name="swapfile"></a>archivo de intercambio

Asegúrese de que haya un archivo de intercambio configurado correctamente para evitar cualquier problemas de memoria insuficiente. Consulte la documentación de Linux para saber cómo crear y un tamaño adecuado a un archivo de intercambio.

### <a name="virtual-machines-and-dynamic-memory"></a>Máquinas virtuales y memoria dinámica

Si se ejecuta SQL Server en Linux en una máquina virtual, asegúrese de que seleccionar opciones para corregir la cantidad de memoria reservada para la máquina virtual. No use características como la memoria dinámica de Hyper-V.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de las características de SQL Server que mejoran el rendimiento, consulte [empezar a trabajar con características de rendimiento](sql-server-linux-performance-get-started.md).

Para obtener más información acerca de SQL Server en Linux, consulte [información general de SQL Server en Linux](sql-server-linux-overview.md).

