---
title: Referencia de azdata bdc status
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 974b9587f506e11ccf80d3ea9af04bc1dfa0be86
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531702"
---
# <a name="azdata-bdc-status"></a>azdata bdc status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

En el artículo siguiente se proporciona una referencia de los comandos de `sql` de la herramienta `azdata`. Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc status show](#azdata-bdc-status-show) | Muestra el estado del clúster de macrodatos.
## <a name="azdata-bdc-status-show"></a>azdata bdc status show
Muestra el estado del clúster de macrodatos.
```bash
azdata bdc status show [--resource -r] 
                       [--all -a]
```
### <a name="examples"></a>Ejemplos
Estado del clúster de macrodatos en el que ha iniciado sesión el usuario.
```bash
azdata bdc status show
```
Estado del clúster de macrodatos con todas las instancias de los recursos incluidos.
```bash
azdata bdc status show --all
```
Estado del clúster de macrodatos de los servicios que incluyen el recurso de control.
```bash
azdata bdc status show --resource control
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--resource -r`
Obtenga los servicios asociados a este recurso.
#### `--all -a`
Muestre todas las instancias de cada recurso en los servicios.
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

Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta `azdata`, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
