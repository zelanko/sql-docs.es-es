---
title: Referencia de azdata bdc endpoint
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos azdata bdc endpoint.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: db24ca1ca1bb6fa25ddd7486fe041ea54722276c
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426215"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc endpoint

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos **bdc endpoint** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, consulte la [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc endpoint list](#azdata-bdc-endpoint-list) | Enumera los puntos de conexión para el clúster de macrodatos.
## <a name="azdata-bdc-endpoint-list"></a>azdata bdc endpoint list
Enumera los puntos de conexión para el clúster de macrodatos.
```bash
azdata bdc endpoint list [--endpoint-name -e] 
                         
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--endpoint-name -e`
Nombre del punto de conexión del clúster de macrodatos.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle del registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y otros ejemplos, consulte [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta el nivel de detalle del registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de **azdata**, consulte la [referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata**, consulte [Instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
