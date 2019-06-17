---
title: Grupo de búferes híbrido | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: DBArgenis
ms.author: argenisf
manager: jroth
ms.openlocfilehash: ce63196cb8a5c8791eb6440f69cf06194591f422
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785286"
---
# <a name="hybrid-buffer-pool"></a>Grupo de búferes híbrido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

El grupo de búferes híbrido permite al motor de base de datos acceder directamente a las páginas de datos de los archivos de base de datos almacenados en dispositivos de memoria persistente (PMEM). Esta característica se introdujo en [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)].

En un sistema tradicional sin PMEM, SQL Server almacena en caché las páginas de datos en el grupo de búferes basado en DRAM. Con el grupo de búferes híbrido, SQL Server omite la realización de una copia de la página en la parte basada en DRAM del grupo de búferes y, en su lugar, accede a la página directamente en el archivo de base de datos que se encuentra en un dispositivo PMEM. El acceso a archivos de datos de dispositivos PMEM para el grupo de búferes híbrido se realiza mediante E/S (MMIO) asignadas a memoria. Esto también se conoce como *esclarecimiento* de los archivos de datos de SQL Server.

En un dispositivo PMEM solo se puede acceder directamente a páginas limpias. Cuando una página se marca como con errores, se copia en el grupo de búferes basado en DRAM antes de escribirse definitivamente en el dispositivo PMEM y se vuelve a marcar como sin errores. Este proceso es algo que sucede durante las operaciones habituales de punto de control.

La característica de grupo de búferes híbrido está disponible para Windows y Linux. El dispositivo PMEM debe formatearse con un sistema de archivos que admita DAX (DirectAccess). Los sistemas XFS, EXT4 y NTFS admiten DAX. SQL Server detectará automáticamente si los archivos de datos residen en un dispositivo PMEM con el formato apropiado, y realizará una asignación de memoria al espacio del usuario. Esta asignación sucede en el inicio, cuando se adjunta, restaura o crea una base de datos nueva, o cuando se habilita la característica de grupo de búferes híbrido en una base de datos.

Para obtener más información sobre la compatibilidad de PMEM con Windows Server, vea [Deploy persistent memory on Windows Server](/windows-server/storage/storage-spaces/deploy-pmem/) (Implementación de memoria persistente en Windows Server).

Para obtener más información sobre cómo configurar servidores SQL Server en Linux para dispositivos PMEM, vea [Deploy persistent memory](../../linux/sql-server-linux-configure-pmem.md) (Implementación de memoria persistente).

## <a name="enable-hybrid-buffer-pool"></a>Habilitar el grupo de búferes híbrido

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] presenta el lenguaje dinámico de datos (DDL) para controlar el grupo de búferes híbrido.

En el ejemplo siguiente se habilita el grupo de búferes híbrido para una instancia de SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

El grupo de búferes híbrido se establece de forma predeterminada en deshabilitado en el ámbito de la instancia. Cabe decir que, para que el cambio de configuración surta efecto, debe reiniciar la instancia de SQL Server. Se requiere un reinicio para facilitar la asignación de suficientes páginas hash que den cabida a la capacidad de PMEM total en el servidor.

En el ejemplo siguiente se habilita el grupo de búferes híbrido para una base de datos específica.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

El grupo de búferes híbrido se establece de forma predeterminada en habilitado en el ámbito de la base de datos.

## <a name="disable-hybrid-buffer-pool"></a>Deshabilitar el grupo de búferes híbrido

En el ejemplo siguiente se deshabilita el grupo de búferes híbrido para una instancia de SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

El grupo de búferes híbrido se establece de forma predeterminada en deshabilitado en el ámbito de la instancia. Cabe decir que, para que el cambio de configuración surta efecto, debe reiniciar la instancia de SQL Server. Se requiere un reinicio para evitar una asignación excesiva de páginas de hash, ya que no es necesario tener en cuenta la capacidad de PMEM en el servidor.

En el ejemplo siguiente se deshabilita el grupo de búferes híbrido para una base de datos específica.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

El grupo de búferes híbrido se establece de forma predeterminada en habilitado en el ámbito de la base de datos.

## <a name="view-hybrid-buffer-pool-configuration"></a>Ver la configuración del grupo de búferes híbrido

En el ejemplo siguiente se devuelve el estado actual de la configuración del sistema del grupo de búferes híbrido de una instancia de SQL Server.

```sql
SELECT *
FROM sys.configurations
WHERE
    name = 'hybrid_buffer_pool';
```

El ejemplo siguiente devuelve dos tablas:

- En la primera se muestra el estado actual de la configuración del sistema del grupo de búferes híbrido para una instancia de SQL Server.
- En la segunda se enumeran las bases de datos y la configuración del nivel de base de datos para el grupo de búferes híbrido (`is_memory_optimized_enabled`).

```sql
SELECT * FROM sys.configurations WHERE name = 'hybrid_buffer_pool';

SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>Procedimientos recomendados para el grupo de búferes híbrido

No se recomienda habilitar el grupo de búferes híbrido en instancias con menos de 16 GB de RAM.

Al dar formato al dispositivo PMEM en Windows, use el tamaño de unidad de asignación más grande disponible para NTFS (2 MB en Windows Server 2019) y asegúrese de que el dispositivo se ha formateado para DAX (DirectAccess).

Los tamaños de archivo deben ser múltiplo de 2 MB (el módulo de 2 MB debe ser igual a cero).

Si la configuración del ámbito del servidor para el grupo de búferes híbrido se establece en deshabilitado, ninguna base de datos de usuario utilizará dicho grupo de búferes.

Si la configuración del ámbito del servidor para el búfer híbrido está habilitada, puede deshabilitar el uso del grupo de búferes híbrido en las bases de datos de usuario individuales siguiendo los pasos para deshabilitar los grupos de búferes híbridos en el ámbito de la base de datos para dichas bases de datos de usuario.
