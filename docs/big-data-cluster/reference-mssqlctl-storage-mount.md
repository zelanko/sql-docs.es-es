---
title: mssqlctl storage mount reference
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de almacenamiento mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3ad8a97bac1f708dcf01612368c76d584fa39f5c
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860296"
---
# <a name="mssqlctl-storage-mount"></a>Montaje del almacenamiento mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **montaje del almacenamiento** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [crear](#create) | Crear montajes de almacenes remotos en HDFS. |
| [eliminar](#delete) | Eliminar montajes de almacenes remotos en HDFS. |
| [status](#status) | Estado de mount(s). |

## <a id="create"></a> mssqlctl storage mount create

Crear montajes de almacenes remotos en HDFS.

```
mssqlctl storage mount create
   --local-path
   --remote-uri
   [--credential-file]
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--local-path** | Ruta de acceso HDFS que tiene el montaje se cree (destino de montaje). Requerido. |
| **--remote-uri** | URI del almacén remoto que se va a montado (origen de montaje). Requerido. |
| **--credential-file** | Archivo que contiene las credenciales para tener acceso al almacén remoto. Las credenciales deben especificarse como clave de pares nombre-valor con una clave = valor por línea. Cualquier igual en las claves o valores que se deban omitir. No se requieren credenciales de forma predeterminada. Las claves necesarias dependen el tipo de almacén remoto que se va a montar y el tipo de autorización que usa. |

### <a name="examples"></a>Ejemplos

Para montar "datos" del contenedor en la cuenta de ADLS de generación 2 "adlsv2example" en la ruta de acceso HDFS `/mounts/adlsv2/data` mediante la clave compartida:

```
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/ --local-path /mounts/adlsv2/data --credentials credential_file
```

Para montar un clúster HDFS remoto (`hdfs://namenode1:8080/`) en la ruta de acceso HDFS local `/mounts/hdfs/`:

```
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --local-path /mounts/hdfs/
```

## <a id="delete"></a> mssqlctl storage mount delete

Eliminar montajes de almacenes remotos en HDFS.

```
mssqlctl storage mount delete
   --local-path
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--local-path** | La ruta de acceso HDFS correspondiente para el montaje en la que se va a eliminar. Requerido. |

### <a name="examples"></a>Ejemplos

Eliminar montaje creado en /mounts/adlsv2/data para una cuenta de almacenamiento ADLS de generación 2.

```
mssqlctl storage mount delete --local-path /mounts/adlsv2/data
```

## <a id="status"></a> estado de montaje del almacenamiento de mssqlctl

Estado de mount(s).

```
mssqlctl storage mount status
   --local-path
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--mount-path** | Ruta de acceso de montaje. Requerido. |

### <a name="examples"></a>Ejemplos

Obtener estado de montaje, ruta de acceso

```
mssqlctl storage mount status --mount-path /mounts/hdfs
```

Obtiene el estado de todos los montajes.

```
mssqlctl storage mount status
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).