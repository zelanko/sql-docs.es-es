---
title: Referencia de sql de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de los comandos sql de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f8fa1ca8df7f4d72c6df9b252d639f8771dee30c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "74908737"
---
# <a name="azdata-sql"></a>sql de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

En el artículo siguiente se proporciona una referencia de los comandos `sql` de la herramienta `azdata`. Para más información sobre otros comandos `azdata`, vea la [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | La CLI de SQL DB permite al usuario interactuar con SQL Server mediante T-SQL.
[azdata sql query](#azdata-sql-query) | El comando de consulta permite ejecutar una consulta T-SQL.
## <a name="azdata-sql-shell"></a>azdata sql shell
La CLI de SQL DB permite al usuario interactuar con SQL Server mediante T-SQL.
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
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-sql-query"></a>azdata sql query
El comando de consulta permite ejecutar una consulta T-SQL.
```bash
azdata sql query -q --database -d
```
### <a name="examples"></a>Ejemplos
Seleccione la lista de nombres de tablas.  De forma predeterminada, la base de datos es maestra.
```bash
azdata sql query -q 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parámetros obligatorios
#### `--database -d`
Base de datos en la que se ejecutará la consulta.  De forma predeterminada, es maestra.
#### `-q`
Consulta T-SQL que se va a ejecutar.
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
