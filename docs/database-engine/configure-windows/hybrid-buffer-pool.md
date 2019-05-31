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
manager: craigg
ms.openlocfilehash: 5e36363347d9d491f541715dffa3cce731cc1efc
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993556"
---
# <a name="hybrid-buffer-pool"></a>Grupo de búferes híbrido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

El grupo de búferes híbrido permite al motor de base de datos acceder directamente a las páginas de datos de los archivos de base de datos almacenados en dispositivos de memoria persistente (PMEM). Esta característica se introdujo en [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)].

En un sistema tradicional sin PMEM, SQL Server almacena en caché las páginas de datos en el grupo de búferes. Con el grupo de búferes híbrido, SQL Server omite la realización de una copia de la página en la parte basada en DRAM del grupo de búferes y, en su lugar, accede a la página directamente en el archivo de base de datos que se encuentra en un dispositivo PMEM. El acceso a archivos de datos de dispositivos PMEM para el grupo de búferes híbrido se realiza mediante E/S (MMIO) asignadas a memoria. Esto también se conoce como *esclarecimiento* de los archivos de datos de SQL Server.

En un dispositivo PMEM solo se puede acceder directamente a páginas limpias. Cuando una página se marca como con errores, se copia en el grupo de búferes DRAM antes de escribirse definitivamente en el dispositivo PMEM y se vuelve a marcar como sin errores. Esto ocurrirá durante las operaciones de punto de control regulares.

La característica de grupo de búferes híbrido está disponible para Windows y Linux. El dispositivo PMEM debe formatearse con un sistema de archivos que admita DAX (DirectAccess). Los sistemas XFS, EXT4, NTFS y ReFS admiten DAX. SQL Server detectará automáticamente si los archivos de datos residen en un dispositivo PMEM con el formato apropiado y realizará una asignación de memoria al espacio del usuario al inicio, cuando se adjunta, restaura o crea una base de datos nueva, o cuando se habilita la característica de grupo de búferes híbrido.

Para obtener más información sobre la compatibilidad de PMEM con Windows Server, que también se conoce como “memoria de clase de almacenamiento” (SCM), vea [implementar la memoria persistente en Windows Server](/windows-server/storage/storage-spaces/deploy-pmem/).

Para obtener más información sobre cómo configurar SQL Server en Linux para dispositivos PMEM, vea [implementar la memoria persistente](../../linux/sql-server-linux-configure-pmem.md).

## <a name="enable-hybrid-buffer-pool"></a>Habilitar el grupo de búferes híbrido

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] presenta el lenguaje dinámico de datos (DDL) para controlar el grupo de búferes híbrido.

En el ejemplo siguiente se habilita el grupo de búferes híbrido para una instancia de SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

De forma predeterminada, el grupo de búferes híbrido se establece en deshabilitado en el ámbito de la instancia.

En el ejemplo siguiente se habilita el grupo de búferes híbrido para una base de datos específica.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

De forma predeterminada, el grupo de búferes híbrido se establece en habilitado en el ámbito de la base de datos.

## <a name="disable-hybrid-buffer-pool"></a>Deshabilitar el grupo de búferes híbrido

En el ejemplo siguiente se deshabilita el grupo de búferes híbrido para una instancia de SQL Server:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

De forma predeterminada, el grupo de búferes híbrido se establece en deshabilitado en el ámbito de la instancia.

En el ejemplo siguiente se deshabilita el grupo de búferes híbrido para una base de datos específica.

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

De forma predeterminada, el grupo de búferes híbrido se establece en habilitado en el ámbito de la base de datos.

## <a name="view-hybrid-buffer-pool-configuration"></a>Ver la configuración del grupo de búferes híbrido

En el ejemplo siguiente se devuelve el estado actual de la configuración del sistema del grupo de búferes híbrido para una instancia de SQL Server.

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

Al dar formato al dispositivo PMEM en Windows, use el tamaño de unidad de asignación más grande disponible para NTFS o ReFS (2 MB en Windows Server 2019) y asegúrese de que el dispositivo se ha formateado para DAX (DirectAccess).

Si la configuración del ámbito del servidor para el grupo de búferes híbrido se establece en deshabilitado, ninguna base de datos de usuario utilizará dicho grupo de búferes.

Si la configuración del ámbito del servidor para el búfer híbrido está habilitada, puede deshabilitar el uso del grupo de búferes híbrido en las bases de datos de usuario individuales siguiendo los pasos para deshabilitar los grupos de búferes híbridos en el ámbito de la base de datos para dichas bases de datos de usuario.