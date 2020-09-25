---
title: Referencia de azdata bdc sql status
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc sql status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 70cdacef1949842157e0c6679565aaf3837f3566
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914569"
---
# <a name="azdata-bdc-sql-status"></a>azdata bdc sql status

Se aplica a `azdata`

En el siguiente artículo se proporciona una referencia de los comandos **sql** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos

|Comando|Descripción|
| --- | --- |
[azdata bdc sql status show](#azdata-bdc-sql-status-show) | Estado del servicio SQL Server.
## <a name="azdata-bdc-sql-status-show"></a>azdata bdc sql status show
Estado del servicio SQL Server.
```bash
azdata bdc sql status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>Ejemplos
Obtenga el estado del servicio SQL.
```bash
azdata bdc sql status show
```
Obtenga el estado del servicio SQL con todas las instancias.
```bash
azdata bdc sql status show --all
```
Obtenga el estado del recurso maestro dentro del servicio SQL.
```bash
azdata bdc sql status show --resource master
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
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de **azdata**, vea [Referencia de azdata](reference-azdata.md). 

Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata](..\install\deploy-install-azdata.md).

