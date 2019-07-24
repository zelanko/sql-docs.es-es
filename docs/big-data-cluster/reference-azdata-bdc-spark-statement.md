---
title: referencia de la instrucción Spark de BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de la instrucción Spark de BDC de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 778980ac6b93e7db79d59182fbd18ab4cfdb8b75
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426095"
---
# <a name="azdata-bdc-spark-statement"></a>azdata BDC Spark (instrucción)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

En el siguiente artículo se proporciona una referencia para los comandos de la **instrucción Spark de BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[lista de instrucciones de azdata BDC Spark](#azdata-bdc-spark-statement-list) | Enumere todas las instrucciones de la sesión de Spark determinada.
[azdata de la instrucción Spark de BDC](#azdata-bdc-spark-statement-create) | Cree una nueva instrucción de Spark en la sesión especificada.
[azdata información de la instrucción de Spark BDC](#azdata-bdc-spark-statement-info) | Obtiene información sobre la instrucción solicitada en la sesión de Spark determinada.
[cancelación de la instrucción azdata de BDC](#azdata-bdc-spark-statement-cancel) | Cancela una instrucción dentro de la sesión de Spark dada.
## <a name="azdata-bdc-spark-statement-list"></a>lista de instrucciones de azdata BDC Spark
Enumere todas las instrucciones de la sesión de Spark determinada.
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>Ejemplos
Enumere todas las instrucciones de sesión.
```bash
azdata spark statement list --session-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--session-id -i`
Número de ID. de sesión de Spark.
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
## <a name="azdata-bdc-spark-statement-create"></a>azdata de la instrucción Spark de BDC
Esto crea y ejecuta una nueva instrucción en la sesión especificada.  Si la ejecución es rápida, el resultado contiene la salida de la ejecución.  De lo contrario, el resultado se puede recuperar mediante ' información de sesión de Spark ' una vez completada la instrucción.
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>Ejemplos
Ejecutar una instrucción.
```bash
azdata spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--session-id -i`
Número de ID. de sesión de Spark.
#### `--code -c`
Cadena que contiene el código que se va a ejecutar como parte de la instrucción.
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
## <a name="azdata-bdc-spark-statement-info"></a>azdata información de la instrucción de Spark BDC
Esto obtiene el estado de ejecución y los resultados de la ejecución si se ha completado la instrucción. El identificador de instrucción se devuelve de ' Spark Statement Create '.
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>Ejemplos
Obtiene la información de la instrucción de la sesión con el identificador 0 y el identificador de instrucción 0.
```bash
azdata spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--session-id -i`
Número de ID. de sesión de Spark.
#### `--statement-id -s`
Número de ID. de la instrucción de Spark en el ID. de sesión especificado.
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
## <a name="azdata-bdc-spark-statement-cancel"></a>cancelación de la instrucción azdata de BDC
Esto cancela una instrucción dentro de la sesión de Spark dada. El identificador de instrucción se devuelve de ' Spark Statement Create '.
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>Ejemplos
Cancela una instrucción.
```bash
azdata spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--session-id -i`
Número de ID. de sesión de Spark.
#### `--statement-id -s`
Número de ID. de la instrucción de Spark en el ID. de sesión especificado.
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

Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata** , consulte [instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
