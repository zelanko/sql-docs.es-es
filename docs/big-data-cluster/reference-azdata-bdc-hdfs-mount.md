---
title: referencia de montaje de HDFS de BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de montaje de HDFS de azdata BDC.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f0b259a3ac4ac0850fa05de3867e928b035307b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426275"
---
# <a name="azdata-bdc-hdfs-mount"></a>montaje de HDFS de BDC de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos de **montaje de HDFS de BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[creación del montaje de HDFS de BDC de azdata](#azdata-bdc-hdfs-mount-create) | Cree montajes de almacenes remotos en HDFS.
[eliminación de azdata BDC HDFS](#azdata-bdc-hdfs-mount-delete) | Eliminar montajes de almacenes remotos en HDFS.
[Estado de montaje de HDFS de BDC de azdata](#azdata-bdc-hdfs-mount-status) | Estado de montaje (s).
[actualización de montaje de HDFS de BDC de azdata](#azdata-bdc-hdfs-mount-refresh) | Actualice el contenido de un montaje en HDFS.
## <a name="azdata-bdc-hdfs-mount-create"></a>creación del montaje de HDFS de BDC de azdata
Cree montajes de almacenes remotos en HDFS. Las credenciales para tener acceso al almacén remoto, si existe, se deben especificar mediante la variable de entorno MOUNT_CREDENTIALS como una lista separada por comas de pares clave = valor. Las comas de las claves o los valores deben ser de escape.
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>Ejemplos
Para montar "Data" del contenedor en la cuenta de ADLS Gen 2 "adlsv2example" en la ruta de acceso de HDFS/mounts/adlsv2/Data mediante la clave compartida
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
Para montar un BDC de HDFS remoto (hdfs://namenode1:8080/) en la ruta de acceso de HDFS local/mounts/HDFS/
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--remote-uri -r`
URI del almacén remoto que se va a montar (origen de montaje).
#### `--mount-path -m`
Ruta de HDFS en la que se debe crear el montaje (destino del montaje).
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-mount-delete"></a>eliminación de azdata BDC HDFS
Eliminar montajes de almacenes remotos en HDFS.
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>Ejemplos
Elimine el montaje creado en/mounts/adlsv2/Data para una cuenta de almacenamiento de ADLS Gen 2.
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--mount-path -m`
la ruta de acceso HDFS correspondiente al montaje que se debe eliminar.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-mount-status"></a>Estado de montaje de HDFS de BDC de azdata
Estado de montaje (s).
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>Ejemplos
Obtención del estado de montaje por ruta de acceso
```bash
azdata bdc hdfs mount status --mount-path /mounts/hdfs
```
Obtiene el estado de todos los montajes.
```bash
azdata bdc hdfs mount status
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--mount-path -m`
Ruta de montaje.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-hdfs-mount-refresh"></a>actualización de montaje de HDFS de BDC de azdata
Actualice el contenido de un montaje en HDFS.
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>Ejemplos
El montaje de la actualización se creó en/mounts/adlsv2/Data.
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--mount-path -m`
Ruta HDFS correspondiente al montaje que se debe actualizar.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata** , consulte [instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
