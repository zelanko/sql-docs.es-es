---
title: Referencia de azdata bdc hdfs mount
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos azdata bdc hdfs mount.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f0b259a3ac4ac0850fa05de3867e928b035307b
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426275"
---
# <a name="azdata-bdc-hdfs-mount"></a>azdata bdc hdfs mount

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos **bdc hdfs mount** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc hdfs mount create](#azdata-bdc-hdfs-mount-create) | Cree montajes de almacenes remotos en HDFS.
[azdata bdc hdfs mount delete](#azdata-bdc-hdfs-mount-delete) | Elimine montajes de almacenes remotos en HDFS.
[azdata bdc hdfs mount status](#azdata-bdc-hdfs-mount-status) | Estado de los montajes.
[azdata bdc hdfs mount refresh](#azdata-bdc-hdfs-mount-refresh) | Actualice el contenido de un montaje en HDFS.
## <a name="azdata-bdc-hdfs-mount-create"></a>azdata bdc hdfs mount create
Cree montajes de almacenes remotos en HDFS. Las credenciales para acceder al almacén remoto, si existe, se deben especificar mediante la variable de entorno MOUNT_CREDENTIALS como una lista separada por comas de pares clave=valor. Es necesario usar un carácter de escape en las comas de las claves o los valores.
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>Ejemplos
Para montar el contenedor "data" en la cuenta "adlsv2example" de ADLS Gen2 en la ruta de acceso de HDFS /mounts/adlsv2/data mediante la clave compartida.
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
Para montar un BDC de HDFS remoto (hdfs://namenode1:8080/) en la ruta de acceso de HDFS local /mounts/hdfs/.
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--remote-uri -r`
URI del almacén remoto que se va a montar (origen del montaje).
#### `--mount-path -m`
Ruta de HDFS en la que se debe crear el montaje (destino del montaje).
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-mount-delete"></a>azdata bdc hdfs mount delete
Elimine montajes de almacenes remotos en HDFS.
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>Ejemplos
Elimine el montaje creado en /mounts/adlsv2/data para una cuenta de almacenamiento de ADLS Gen2.
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--mount-path -m`
Ruta de acceso de HDFS correspondiente al montaje que se debe eliminar.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-mount-status"></a>azdata bdc hdfs mount status
Estado de los montajes.
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>Ejemplos
Obtención del estado de montaje por ruta de acceso.
```bash
azdata bdc hdfs mount status --mount-path /mounts/hdfs
```
Obtención del estado de todos los montajes.
```bash
azdata bdc hdfs mount status
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--mount-path -m`
Ruta de acceso de montaje.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-mount-refresh"></a>azdata bdc hdfs mount refresh
Actualice el contenido de un montaje en HDFS.
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>Ejemplos
Actualización del montaje creado en /mounts/adlsv2/data.
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--mount-path -m`
Ruta de acceso de HDFS correspondiente al montaje que se debe actualizar.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
