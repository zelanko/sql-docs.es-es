---
title: Referencia de sql de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de los comandos sql de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b1e76076763186e2002fb3a7bbc2271b938cbf7e
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158200"
---
# <a name="azdata-sql"></a>sql de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artículo es un artículo de referencia para **azdata**. 

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
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
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
azdata sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parámetros necesarios
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
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md). 

- Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
