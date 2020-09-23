---
title: Referencia de azdata bdc control status
titleSuffix: SQL Server big data clusters
description: Use este artículo de referencia para entender los comandos SQL en la herramienta azdata, en particular los comandos bdc control status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8550ab6fcdb5e4e808db34d0c6e3f7e738f845a2
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89734038"
---
# <a name="azdata-bdc-control-status"></a>azdata bdc control status

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

En el artículo siguiente se proporciona una referencia de los comandos `sql` de la herramienta `azdata`. Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
| Comando | Descripción |
| --- | --- |
[azdata bdc control status show](#azdata-bdc-control-status-show) | Estado del servicio de control.
## <a name="azdata-bdc-control-status-show"></a>azdata bdc control status show
Estado del servicio de control.
```bash
azdata bdc control status show [--resource -r] 
                               [--all -a]
```
### <a name="examples"></a>Ejemplos
Obtención del estado del servicio.
```bash
azdata bdc control status show
```
Obtención del estado del servicio de control con todas las instancias.
```bash
azdata bdc control status show --all
```
Obtención del estado del recurso de control en el servicio de control.
```bash
azdata bdc control status show --resource control
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

Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta `azdata`, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](../install/deploy-install-azdata.md).
