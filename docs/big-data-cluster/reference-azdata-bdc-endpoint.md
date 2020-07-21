---
title: Referencia de azdata bdc endpoint
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos azdata bdc endpoint.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 71f52b8312518cf669751d50dcc857c3d892bd98
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588081"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc endpoint

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

En el artículo siguiente se proporciona una referencia del comando `bdc endpoint` de la herramienta `azdata`. Para más información sobre otros comandos `azdata`, vea la [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
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
