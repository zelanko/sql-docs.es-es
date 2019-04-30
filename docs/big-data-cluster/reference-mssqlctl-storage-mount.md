---
title: mssqlctl storage mount reference
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos de montaje del almacenamiento de mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 523253e8d1ff2d621d9f7a5ef90dbc957fba82ec
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473487"
---
# <a name="mssqlctl-storage-mount"></a>Montaje del almacenamiento mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **montaje del almacenamiento** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[mssqlctl storage mount create](#mssqlctl-storage-mount-create) | Crear montajes de almacenes remotos en HDFS.
[mssqlctl storage mount delete](#mssqlctl-storage-mount-delete) | Eliminar montajes de almacenes remotos en HDFS.
[estado de montaje del almacenamiento de mssqlctl](#mssqlctl-storage-mount-status) | Estado de mount(s).
## <a name="mssqlctl-storage-mount-create"></a>montaje del almacenamiento mssqlctl crear
Crear montajes de almacenes remotos en HDFS.
```bash
mssqlctl storage mount create --remote-uri 
                              --mount-path  
                              [--credential-file]
```
### <a name="examples"></a>Ejemplos
Para montar el contenedor "datos" en "adlsv2example" cuenta de ADLS de generación 2 en /mounts/adlsv2/data de ruta de acceso HDFS mediante la clave compartida
```bash
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data --credentials credential_file
```
Para montar un clúster HDFS remoto (hdfs://namenode1:8080 /) en local HDFS path /mounts/hdfs /
```bash
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
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
## <a name="mssqlctl-storage-mount-delete"></a>mssqlctl storage mount delete
Eliminar montajes de almacenes remotos en HDFS.
```bash
mssqlctl storage mount delete --mount-path 
                              
```
### <a name="examples"></a>Ejemplos
Eliminar montaje creado en /mounts/adlsv2/data para una cuenta de almacenamiento ADLS de generación 2.
```bash
mssqlctl storage mount delete --mount-path /mounts/adlsv2/data
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
## <a name="mssqlctl-storage-mount-status"></a>estado de montaje del almacenamiento de mssqlctl
Estado de mount(s).
```bash
mssqlctl storage mount status [--mount-path] 
                              
```
### <a name="examples"></a>Ejemplos
Obtener estado de montaje, ruta de acceso
```bash
mssqlctl storage mount status --mount-path /mounts/hdfs
```
Obtiene el estado de todos los montajes.
```bash
mssqlctl storage mount status
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