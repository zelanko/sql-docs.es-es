---
title: Referencia de sql de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de los comandos sql de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9965c6805cb8e12e6a5a2990a43bb7bf7c937fe1
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733949"
---
# <a name="azdata-sql"></a>sql de azdata

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

En el artículo siguiente se proporciona una referencia de los comandos `sql` de la herramienta `azdata`. Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
| Comando | Descripción |
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | La CLI de SQL Database permite al usuario interactuar con SQL Server mediante T-SQL.
[azdata sql query](#azdata-sql-query) | El comando de consulta permite ejecutar una consulta T-SQL.
## <a name="azdata-sql-shell"></a>azdata sql shell
La CLI de SQL Database permite al usuario interactuar con SQL Server mediante T-SQL.
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
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-sql-query"></a>azdata sql query
El comando de consulta permite ejecutar una consulta T-SQL.
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>Ejemplos
Seleccione la lista de nombres de tablas.  De forma predeterminada, la base de datos es maestra.
```bash
azdata sql query "SELECT name FROM SYS.TABLES"
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
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta `azdata`, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](../install/deploy-install-azdata.md).
