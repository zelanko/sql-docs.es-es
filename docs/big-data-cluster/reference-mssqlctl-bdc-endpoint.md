---
title: referencia de punto de conexión de bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de punto de conexión de bdc mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 74065a075e4a2a80e3ab5455b7ac99e5a055f66a
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727457"
---
# <a name="mssqlctl-bdc-endpoint"></a>punto de conexión de bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **punto de conexión de bdc** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[mssqlctl bdc endpoint list](#mssqlctl-bdc-endpoint-list) | Enumera los puntos de conexión para el clúster grande de datos.
## <a name="mssqlctl-bdc-endpoint-list"></a>lista de puntos de conexión de bdc mssqlctl
Enumera los puntos de conexión para el clúster grande de datos.
```bash
mssqlctl bdc endpoint list [--endpoint-name -e] 
                           
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--endpoint-name -e`
Nombre del punto de conexión BDC.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).