---
title: mssqlctl bdc storage-pool mount reference
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de montaje de mssqlctl bdc bloque de almacenamiento.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cf6012b6c700afd6ee0eca763df0961f088a3be4
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394247"
---
# <a name="mssqlctl-bdc-storage-pool-mount"></a>montaje de bloque de almacenamiento de bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **montaje del bloque de almacenamiento de bdc** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[mssqlctl bdc storage-pool mount create](#mssqlctl-bdc-storage-pool-mount-create) | Crear montajes de almacenes remotos en HDFS.
[mssqlctl bdc storage-pool mount delete](#mssqlctl-bdc-storage-pool-mount-delete) | Eliminar montajes de almacenes remotos en HDFS.
[estado de montaje de bloque de almacenamiento de bdc mssqlctl](#mssqlctl-bdc-storage-pool-mount-status) | Estado de mount(s).
## <a name="mssqlctl-bdc-storage-pool-mount-create"></a>montaje de bloque de almacenamiento de bdc mssqlctl crear
Crear montajes de almacenes remotos en HDFS. Deben especificar las credenciales para tener acceso al almacén remoto, si hay alguno, mediante la variable de entorno MOUNT_CREDENTIALS como una lista separada por comas de clave de pares nombre-valor. Las comas de las claves o valores deben ser de escape.
```bash
mssqlctl bdc storage-pool mount create --remote-uri 
                                       --mount-path
```
### <a name="examples"></a>Ejemplos
Para montar el contenedor "datos" en "adlsv2example" cuenta de ADLS de generación 2 en /mounts/adlsv2/data de ruta de acceso HDFS mediante la clave compartida
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
mssqlctl bdc storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
Para montar un BDC HDFS remoto (hdfs://namenode1:8080 /) en local HDFS path /mounts/hdfs /
```bash
mssqlctl bdc storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--remote-uri`
URI del almacén remoto que se va a montado (origen de montaje).
#### `--mount-path`
Ruta de acceso HDFS donde montaje se tiene que crearse (destino de montaje).
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-bdc-storage-pool-mount-delete"></a>mssqlctl bdc storage-pool mount delete
Eliminar montajes de almacenes remotos en HDFS.
```bash
mssqlctl bdc storage-pool mount delete --mount-path 
                                       
```
### <a name="examples"></a>Ejemplos
Eliminar montaje creado en /mounts/adlsv2/data para una cuenta de almacenamiento ADLS de generación 2.
```bash
mssqlctl bdc storage-pool mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--mount-path`
La ruta de acceso HDFS correspondiente para el montaje en la que se va a eliminar.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-bdc-storage-pool-mount-status"></a>estado de montaje de bloque de almacenamiento de bdc mssqlctl
Estado de mount(s).
```bash
mssqlctl bdc storage-pool mount status [--mount-path] 
                                       
```
### <a name="examples"></a>Ejemplos
Obtener estado de montaje, ruta de acceso
```bash
mssqlctl bdc storage-pool mount status --mount-path /mounts/hdfs
```
Obtiene el estado de todos los montajes.
```bash
mssqlctl bdc storage-pool mount status
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--mount-path`
Ruta de acceso de montaje.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).