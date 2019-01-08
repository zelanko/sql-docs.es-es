---
title: Cómo configurar memoria persistente (PMEM) para SQL Server en Linux | Microsoft Docs
description: En este artículo se proporciona un ejemplo paso a paso para configurar PMEM en Linux.
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b11b3154162fafdfc717e9785fb65e59dc45799c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510824"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Cómo configurar memoria persistente (PMEM) para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describe cómo configurar la memoria persistente (PMEM) para SQL Server en Linux. Compatibilidad PMEM en Linux se introdujo en la versión preliminar de SQL Server 2019.

## <a name="overview"></a>Información general

SQL Server 2016 introdujo la compatibilidad con DIMM no volátil y una optimización denominada [final del registro de almacenamiento en caché en NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/). Estas optimizaciones reducción el número de operaciones necesarias para reforzar un búfer de registro en un almacenamiento persistente. Esto aprovecha el acceso directo de Windows Server a un dispositivo de memoria persistente en modo DAX.

Vista previa de SQL Server 2019 amplía la compatibilidad con memoria persistente dispositivos (PMEM) para Linux, que proporciona iluminación completa de archivos de registro de transacciones y de datos colocados en PMEM. Iluminación hace referencia al método de acceso al dispositivo de almacenamiento con espacio de usuario eficaz `memcpy()` operaciones. En lugar de pasar por la pila de almacenamiento y del sistema de archivos, SQL Server aprovecha la compatibilidad DAX en Linux para colocar directamente los datos en los dispositivos, lo que reduce la latencia.

## <a name="enable-enlightenment-of-database-files"></a>Habilitar la sensación de archivos de base de datos
Para habilitar la sensación de archivos de base de datos de SQL Server en Linux, siga los pasos siguientes:

1. Configurar los dispositivos.

  En Linux, use el `ndctl` utilidad.

  - Instalar `ndctl` para configurar el dispositivo PMEM. Puede encontrarlo [aquí](https://docs.pmem.io/getting-started-guide/installing-ndctl).
  - Use [ndctl] para crear un espacio de nombres.

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >Si usas `ndctl` versión inferior a 59, use `--mode=memory`.

  Use `ndctl` para comprobar el espacio de nombres. La salida de ejemplo siguiente:

```bash
ndctl list
[
  {
    "dev":"namespace0.0",
    "mode":"memory",
    "size":1099511627776,
    "blockdev":"pmem0",
    "numa_node":0
  }
]
```

  - Crear y montar PMEM dispositivo

    Por ejemplo, con XFS

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    Por ejemplo, con EXT4

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    ```

  Una vez que el dispositivo se ha configurado con ndctl, con el formato y montado, puede colocar los archivos de base de datos en ella. También puede crear una nueva base de datos 

1. Habilitar la sensación de archivo de base de datos de SQL Server mediante la marca de seguimiento 3979. Esta marca de seguimiento es una marca de seguimiento de inicio y, por lo tanto debe habilitarse mediante la utilidad mssql-conf.

1. Reinicie SQL Server.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server en Linux, consulte [SQL Server en Linux](sql-server-linux-overview.md).
