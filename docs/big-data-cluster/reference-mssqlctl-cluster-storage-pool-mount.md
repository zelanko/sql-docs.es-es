---
title: referencia de montaje de bloque de almacenamiento de clúster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de montaje de bloque de almacenamiento de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eb527779cd844064bcabccc91f5356676e06f004
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779304"
---
# <a name="mssqlctl-cluster-storage-pool-mount"></a>Montaje del grupo de almacenamiento de clúster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **montaje del bloque de almacenamiento de clúster** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[montaje del bloque de almacenamiento de clúster mssqlctl crear](#mssqlctl-cluster-storage-pool-mount-create) | Crear montajes de almacenes remotos en HDFS.
[mssqlctl cluster storage-pool mount delete](#mssqlctl-cluster-storage-pool-mount-delete) | Eliminar montajes de almacenes remotos en HDFS.
[estado de montaje del bloque de almacenamiento de clúster de mssqlctl](#mssqlctl-cluster-storage-pool-mount-status) | Estado de mount(s).
## <a name="mssqlctl-cluster-storage-pool-mount-create"></a>montaje del bloque de almacenamiento de clúster mssqlctl crear
Crear montajes de almacenes remotos en HDFS.
```bash
mssqlctl cluster storage-pool mount create --remote-uri 
                                           --mount-path  
                                           [--credential-file]
```
### <a name="examples"></a>Ejemplos
Para montar el contenedor "datos" en "adlsv2example" cuenta de ADLS de generación 2 en /mounts/adlsv2/data de ruta de acceso HDFS mediante la clave compartida
```bash
mssqlctl cluster storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data --credentials credential_file
```
Para montar un clúster HDFS remoto (hdfs://namenode1:8080 /) en local HDFS path /mounts/hdfs /
```bash
mssqlctl cluster storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--remote-uri`
URI del almacén remoto que se va a montado (origen de montaje).
#### `--mount-path`
Ruta de acceso HDFS donde montaje se tiene que crearse (destino de montaje).
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--credential-file`
Archivo que contiene las credenciales para tener acceso al almacén remoto. Las credenciales deben especificarse como clave de pares nombre-valor con una clave = valor por línea. Cualquier igual en las claves o valores que se deban omitir. No se requieren credenciales de forma predeterminada. Las claves necesarias dependen el tipo de almacén remoto que se va a montar y el tipo de autorización que usa.
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
## <a name="mssqlctl-cluster-storage-pool-mount-delete"></a>eliminación de montaje de mssqlctl clúster grupo de almacenamiento
Eliminar montajes de almacenes remotos en HDFS.
```bash
mssqlctl cluster storage-pool mount delete --mount-path 
                                           
```
### <a name="examples"></a>Ejemplos
Eliminar montaje creado en /mounts/adlsv2/data para una cuenta de almacenamiento ADLS de generación 2.
```bash
mssqlctl cluster storage-pool mount delete --mount-path /mounts/adlsv2/data
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
## <a name="mssqlctl-cluster-storage-pool-mount-status"></a>estado de montaje del bloque de almacenamiento de clúster de mssqlctl
Estado de mount(s).
```bash
mssqlctl cluster storage-pool mount status [--mount-path] 
                                           
```
### <a name="examples"></a>Ejemplos
Obtener estado de montaje, ruta de acceso
```bash
mssqlctl cluster storage-pool mount status --mount-path /mounts/hdfs
```
Obtiene el estado de todos los montajes.
```bash
mssqlctl cluster storage-pool mount status
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