---
title: referencia de SQL de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos SQL de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 90512592901fcf83e4697b5eefc80a6df7aeb032
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426025"
---
# <a name="azdata-sql"></a>SQL azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos **SQL** de la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[Shell de SQL azdata](#azdata-sql-shell) | La CLI de SQL DB permite al usuario interactuar con SQL Server a través de T-SQL.
[consulta SQL azdata](#azdata-sql-query) | El comando de consulta permite la ejecución de una consulta de T-SQL.
## <a name="azdata-sql-shell"></a>Shell de SQL azdata
La CLI de SQL DB permite al usuario interactuar con SQL Server a través de T-SQL.
```bash
azdata sql shell 
```
### <a name="examples"></a>Ejemplos
Línea de comandos de ejemplo para iniciar la experiencia interactiva.
```bash
azdata sql shell
```
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-sql-query"></a>consulta SQL azdata
El comando de consulta permite la ejecución de una consulta de T-SQL.
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>Ejemplos
Seleccione la lista de nombres de tablas.  La base de datos tiene como valor predeterminado Master.
```bash
azdata sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--database -d`
Base de datos en la que se ejecutará la consulta.  El valor predeterminado es Master.
#### `-q`
Consulta T-SQL que se va a ejecutar.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: JSON, jsonc, Table y TSV.  Valor predeterminado: JSON.
#### `--query -q`
Cadena de consulta de JMESPath. Vea [http://jmespath.org/](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo instalar la herramienta **azdata** , consulte [instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
