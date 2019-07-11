---
title: referencia de estado de grupo mssqlctl bdc
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos de estado del grupo de mssqlctl bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 818773708087927b5c2f3ccea44ba52cd77e7a71
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728569"
---
# <a name="mssqlctl-bdc-pool-status"></a>estado del grupo de bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **estado del grupo de bdc** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[Mostrar estado de mssqlctl bdc grupo](#mssqlctl-bdc-pool-status-show) | Estado del grupo.
## <a name="mssqlctl-bdc-pool-status-show"></a>Mostrar estado de mssqlctl bdc grupo
Estado del grupo.
```bash
mssqlctl bdc pool status show --kind -k 
                              [--name -n]
```
### <a name="examples"></a>Ejemplos
Obtiene el estado del grupo de almacenamiento.
```bash
mssqlctl bdc pool status show --kind storage --name default
```
Obtiene el estado de la agrupación de datos.
```bash
mssqlctl bdc pool status show --kind data --name default
```
Obtiene el estado del grupo de proceso.
```bash
mssqlctl bdc pool status show --kind compute --name default
```
Obtiene el estado del grupo principal.
```bash
mssqlctl bdc pool status show --kind master --name default
```
Obtiene el estado del grupo de spark.
```bash
mssqlctl bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--kind -k`
Tipo de grupo BDC.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre del grupo de BDC.
`default`
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

Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).