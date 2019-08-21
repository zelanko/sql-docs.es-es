---
title: Referencia de azdata bdc control status
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos azdata bdc control status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c30fa0bdb9e74941387393a7dffeaadcae05b303
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653212"
---
# <a name="azdata-bdc-control-status"></a>azdata bdc control status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se ofrece una referencia sobre los comandos **bdc control status** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata bdc control status show](#azdata-bdc-control-status-show) | Estado de control.
## <a name="azdata-bdc-control-status-show"></a>azdata bdc control status show
Estado de control.
```bash
azdata bdc control status show 
```
### <a name="examples"></a>Ejemplos
Obtención del estado de control.
```bash
azdata bdc control status show
```
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

Para obtener más información sobre cómo instalar la herramienta **azdata** , vea [instalar azdata para administrar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](deploy-install-azdata.md).
