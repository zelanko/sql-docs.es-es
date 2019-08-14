---
title: Cómo configurar la memoria persistente (PMEM) para SQL Server en Linux
description: Este artículo sirve de tutorial para configurar PMEM en Linux.
author: DBArgenis
ms.author: argenisf
ms.reviewer: vanto
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 4ed705b1b26193585a6278508ac98666d069418a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077561"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>Cómo configurar la memoria persistente (PMEM) para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describe cómo configurar la memoria persistente (PMEM) para SQL Server en Linux. La compatibilidad con PMEM en Linux se incorporó en la versión preliminar de SQL Server 2019.

## <a name="overview"></a>Información general

SQL Server 2016 incorporó compatibilidad con DIMM no volátiles y una optimización denominada [Tail of the Log Caching on NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/) (Almacenamiento en caché del final del registro en NVDIMM). Estas optimizaciones reducen el número de operaciones necesarias para proteger un búfer de registro en un almacenamiento persistente. Esto aprovecha el acceso directo de Windows Server a un dispositivo de memoria persistente en modo DAX.

La versión preliminar de SQL Server 2019 agrega compatibilidad con dispositivos de memoria persistente (PMEM) para Linux, con lo que se facilita la optimización total de los archivos de registro de transacciones y datos colocados en PMEM. La optimización se refiere al método de acceso al dispositivo de almacenamiento con operaciones `memcpy()` de espacio del usuario eficientes. En lugar de pasar por el sistema de archivos y la pila de almacenamiento, SQL Server aprovecha la compatibilidad con DAX en Linux para colocar datos directamente en los dispositivos, lo que reduce la latencia.

## <a name="enable-enlightenment-of-database-files"></a>Habilitación de la optimización de archivos de base de datos
Para habilitar la optimización de archivos de base de datos en SQL Server en Linux, siga estos pasos:

1. Configuración de los dispositivos.

  En Linux, use la utilidad `ndctl`.

  - Instale `ndctl` para configurar el dispositivo PMEM. Puede encontrarlo [aquí](https://docs.pmem.io/getting-started-guide/installing-ndctl).
  - Use [ndctl] crear un espacio de nombres.

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >Si usa una versión de `ndctl` inferior a 59, use `--mode=memory`.

  Use `ndctl` para comprobar el espacio de nombres. La salida de ejemplo es la siguiente:

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

  - Creación y montaje del dispositivo PMEM

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

  Una vez que el dispositivo se haya configurado con ndctl, formateado y montado, puede colocar archivos de base de datos en él. También puede crear una base de datos. 

1. Dado que los dispositivos PMEM son aptos para O_DIRECT, habilite la marca de seguimiento 3979 para deshabilitar el mecanismo de vaciado forzado. Esta marca de seguimiento es una marca de seguimiento de inicio y, como tal, debe habilitarse mediante la utilidad mssql-conf. Tenga en cuenta que se trata de un cambio de configuración de todo el servidor y no debe usar esta marca de seguimiento si tiene algún dispositivo O_DIRECT no compatible que necesite el mecanismo de vaciado forzado para garantizar la integridad de los datos. Para obtener más información, consulte https://support.microsoft.com/en-us/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux

1. Reinicie SQL Server.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre SQL Server en Linux, consulte [SQL Server en Linux](sql-server-linux-overview.md).
