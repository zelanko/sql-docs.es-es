---
title: Referencia de azdata bdc spark statement
description: Artículo de referencia sobre los comandos de azdata bdc spark statement.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38d556944db9e8c269fb8acf8f3089050fb8b1d8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75258610"
---
# <a name="azdata-bdc-spark-statement"></a>azdata bdc spark statement

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

En el artículo siguiente se proporciona una referencia de los comandos `bdc spark statement` de la herramienta `azdata`. Para más información sobre otros comandos `azdata`, vea la [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata bdc spark statement list](#azdata-bdc-spark-statement-list) | Enumera todas las instrucciones de la sesión de Spark correspondiente.
[azdata bdc spark statement create](#azdata-bdc-spark-statement-create) | Crea una nueva instrucción de Spark en la sesión correspondiente.
[azdata bdc spark statement info](#azdata-bdc-spark-statement-info) | Obtiene información sobre la instrucción solicitada en la sesión de Spark correspondiente.
[azdata bdc spark statement cancel](#azdata-bdc-spark-statement-cancel) | Cancela una instrucción en la sesión de Spark correspondiente.
## <a name="azdata-bdc-spark-statement-list"></a>azdata bdc spark statement list
Enumera todas las instrucciones de la sesión de Spark correspondiente.
```bash
azdata bdc spark statement list --session-id -i 
              ```
### Examples
List all the session statements.
```bash
azdata spark statement list --session-id 0
```
### <a name="required-parameters"></a>Parámetros obligatorios
#### `--session-id -i`
Número de identificador de sesión de Spark.
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
## <a name="azdata-bdc-spark-statement-create"></a>azdata bdc spark statement create
Crea y ejecuta una nueva instrucción en la sesión especificada.  Si la ejecución es rápida, el resultado contiene la salida de la ejecución.  De lo contrario, el resultado se puede recuperar mediante "spark session info" una vez completada la instrucción.
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>Ejemplos
Ejecuta una instrucción.
```bash
azdata spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>Parámetros obligatorios
#### `--session-id -i`
Número de identificador de sesión de Spark.
#### `--code -c`
Cadena que contiene el código que se va a ejecutar como parte de la instrucción.
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
## <a name="azdata-bdc-spark-statement-info"></a>azdata bdc spark statement info
Obtiene el estado y los resultados de la ejecución si se ha completado la instrucción. Se devuelve el identificador de la instrucción desde "spark statement create".
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>Ejemplos
Obtiene información de instrucción de la sesión con identificador 0 e identificador de instrucción 0.
```bash
azdata spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parámetros obligatorios
#### `--session-id -i`
Número de identificador de sesión de Spark.
#### `--statement-id -s`
Número de identificador de la instrucción de Spark en el identificador de sesión especificado.
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
## <a name="azdata-bdc-spark-statement-cancel"></a>azdata bdc spark statement cancel
Cancela una instrucción en la sesión de Spark correspondiente. Se devuelve el identificador de la instrucción desde "spark statement create".
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>Ejemplos
Cancela una instrucción.
```bash
azdata spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parámetros obligatorios
#### `--session-id -i`
Número de identificador de sesión de Spark.
#### `--statement-id -s`
Número de identificador de la instrucción de Spark en el identificador de sesión especificado.
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
