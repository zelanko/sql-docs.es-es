---
title: Referencia de azdata bdc control status
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos azdata bdc control status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d1f7e2e5931ec55cd2fd2632072de223db252b84
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426255"
---
# <a name="azdata-bdc-control-status"></a>azdata bdc control status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se ofrece una referencia sobre los comandos **bdc control status** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
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
Aumentar el nivel de detalle del registro para mostrar todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y otros ejemplos, consulte [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumentar el nivel de detalle del registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo instalar la herramienta **azdata**, consulte [Instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
