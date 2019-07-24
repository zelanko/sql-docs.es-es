---
title: referencia de estado del grupo de BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de estado del grupo de BDC de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0a5925af4f16f2147988b2318880d9acec664c3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426135"
---
# <a name="azdata-bdc-pool-status"></a>Estado del grupo de BDC de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos de **Estado del grupo de BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata de estado del grupo de BDC](#azdata-bdc-pool-status-show) | Estado del grupo.
## <a name="azdata-bdc-pool-status-show"></a>azdata de estado del grupo de BDC
Estado del grupo.
```bash
azdata bdc pool status show --kind -k 
                            [--name -n]
```
### <a name="examples"></a>Ejemplos
Obtiene el estado del bloque de almacenamiento.
```bash
azdata bdc pool status show --kind storage --name default
```
Obtiene el estado del grupo de datos.
```bash
azdata bdc pool status show --kind data --name default
```
Obtiene el estado del grupo de proceso.
```bash
azdata bdc pool status show --kind compute --name default
```
Obtiene el estado del grupo principal.
```bash
azdata bdc pool status show --kind master --name default
```
Obtiene el estado del grupo de Spark.
```bash
azdata bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--kind -k`
Tipo de grupo de clústeres de Big Data.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre del grupo de clústeres de Big Data.
`default`
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

Para obtener más información sobre cómo instalar la herramienta **azdata** , consulte [instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
