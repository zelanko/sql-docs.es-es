---
title: Referencia de azdata bdc spark status
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de los comandos azdata bdc status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 59dee7b9c7262233ec6e80097105b1fbd6b4d7ea
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531752"
---
# <a name="azdata-bdc-spark-status"></a>azdata bdc spark status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

En el siguiente artículo encontrará referencias de los comandos `sql` de la herramienta `azdata`. Para más información sobre otros comandos `azdata`, vea la [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc spark status show](#azdata-bdc-spark-status-show) | Estado del servicio de Spark.
## <a name="azdata-bdc-spark-status-show"></a>azdata bdc spark status show
Estado del servicio de Spark.
```bash
azdata bdc spark status show [--resource -r] 
                             [--all -a]
```
### <a name="examples"></a>Ejemplos
Obtenga el estado del servicio de Spark.
```bash
azdata bdc spark status show
```
Obtenga el estado del servicio de Spark con todas las instancias.
```bash
azdata bdc spark status show --all
```
Obtenga el estado del recurso de almacenamiento dentro del servicio de Spark.
```bash
azdata bdc spark status show --resource storage-0
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--resource -r`
Obtenga este recurso en este servicio.
#### `--all -a`
Muestre todas las instancias de cada recurso en el servicio.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre otros comandos `azdata`, vea la [referencia de azdata](reference-azdata.md). Para más información sobre cómo instalar la herramienta `azdata`, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
