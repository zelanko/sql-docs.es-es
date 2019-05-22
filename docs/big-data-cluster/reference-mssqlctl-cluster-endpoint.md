---
title: referencia de punto de conexión de clúster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos mssqlctl de punto de conexión del clúster.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 32c0506a3394ac6ac62745901f908ba1fb725ec2
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995143"
---
# <a name="mssqlctl-cluster-endpoint"></a>punto de conexión de clúster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **punto de conexión del clúster** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[lista de puntos de conexión de clúster mssqlctl](#mssqlctl-cluster-endpoint-list) | Enumera los puntos de conexión para el clúster.
## <a name="mssqlctl-cluster-endpoint-list"></a>lista de puntos de conexión de clúster mssqlctl
Enumera los puntos de conexión para el clúster.
```bash
mssqlctl cluster endpoint list [--endpoint-name -e] 
                               
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--endpoint-name -e`
Nombre de punto de conexión del clúster.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).