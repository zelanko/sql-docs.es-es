---
title: Referencia de azdata bdc pool status
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc pool status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0a5925af4f16f2147988b2318880d9acec664c3
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426135"
---
# <a name="azdata-bdc-pool-status"></a>azdata bdc pool status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona referencia sobre los comandos de **bdc pool status** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc pool status show](#azdata-bdc-pool-status-show) | Estado del grupo.
## <a name="azdata-bdc-pool-status-show"></a>azdata bdc pool status show
Estado del grupo.
```bash
azdata bdc pool status show --kind -k 
                            [--name -n]
```
### <a name="examples"></a>Ejemplos
Obtenga el estado del grupo de almacenamiento.
```bash
azdata bdc pool status show --kind storage --name default
```
Obtenga el estado del grupo de datos.
```bash
azdata bdc pool status show --kind data --name default
```
Obtenga el estado del grupo de proceso.
```bash
azdata bdc pool status show --kind compute --name default
```
Obtenga el estado del grupo maestro.
```bash
azdata bdc pool status show --kind master --name default
```
Obtenga el estado del grupo de Spark.
```bash
azdata bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--kind -k`
Tipo de grupo del clúster de macrodatos
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre de grupo del clúster de macrodatos
`default`
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
