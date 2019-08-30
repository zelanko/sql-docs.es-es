---
title: referencia de estado de HDFS de BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de estado de azdata BDC HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3853e23a0def787a65febf142de4c1d8d8216df7
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158090"
---
# <a name="azdata-bdc-hdfs-status"></a>Estado de HDFS de BDC de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artículo es un artículo de referencia para **azdata**. 

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[muestra de estado de azdata BDC HDFS](#azdata-bdc-hdfs-status-show) | Estado del servicio HDFS.
## <a name="azdata-bdc-hdfs-status-show"></a>muestra de estado de azdata BDC HDFS
Estado del servicio HDFS.
```bash
azdata bdc hdfs status show [--resource -r] 
                            [--all -a]
```
### <a name="examples"></a>Ejemplos
Obtiene el estado del servicio HDFS.
```bash
azdata bdc hdfs status show
```
Obtiene el estado del servicio HDFS con todas las instancias.
```bash
azdata bdc hdfs status show --all
```
Obtiene el estado del recurso de almacenamiento en el servicio HDFS.
```bash
azdata bdc hdfs status show --resource storage-0
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--resource -r`
Obtiene este recurso en este servicio.
#### `--all -a`
Mostrar todas las instancias de cada recurso en el servicio.
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

- Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md). 

- Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
