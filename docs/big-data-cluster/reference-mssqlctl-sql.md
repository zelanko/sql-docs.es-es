---
title: referencia de sql mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de sql mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 844ea94e9df18132fd0729745ff154783b578fc1
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728510"
---
# <a name="mssqlctl-sql"></a>mssqlctl sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **sql** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[mssqlctl sql shell](#mssqlctl-sql-shell) | La CLI de la base de datos de SQL permite al usuario interactuar con SQL Server a través de Transact-SQL.
[consulta de sql mssqlctl](#mssqlctl-sql-query) | El comando de consulta permite la ejecución de una consulta de Transact-SQL.
## <a name="mssqlctl-sql-shell"></a>mssqlctl sql shell
La CLI de la base de datos de SQL permite al usuario interactuar con SQL Server a través de Transact-SQL.
```bash
mssqlctl sql shell 
```
### <a name="examples"></a>Ejemplos
Línea de comandos de ejemplo para iniciar la experiencia interactiva.
```bash
mssqlctl sql shell
```
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
## <a name="mssqlctl-sql-query"></a>consulta de sql mssqlctl
El comando de consulta permite la ejecución de una consulta de Transact-SQL.
```bash
mssqlctl sql query --database -d 
                   -q
```
### <a name="examples"></a>Ejemplos
Seleccione la lista de nombres de tablas.  El valor predeterminado es master de la base de datos.
```bash
mssqlctl sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--database -d`
Para ejecutar la consulta base de datos.  Valor predeterminado es master.
#### `-q`
Consulta de Transact-SQL para ejecutar.
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