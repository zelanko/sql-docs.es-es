---
title: referencia de sesión de Spark de BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de sesión Spark de BDC de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20b7ac3dcf72482e80278ce0f0df922026232a6d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426105"
---
# <a name="azdata-bdc-spark-session"></a>sesión de Spark de BDC de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

En el siguiente artículo se proporciona una referencia para los comandos de **sesión Spark de BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[creación de sesión Spark de BDC de azdata](#azdata-bdc-spark-session-create) | Cree una nueva sesión de Spark.
[lista de sesiones de Spark de BDC de azdata](#azdata-bdc-spark-session-list) | Enumere todas las sesiones activas en Spark.
[información de sesión de Spark de BDC de azdata](#azdata-bdc-spark-session-info) | Obtener información sobre una sesión de Spark activa.
[registro de sesión Spark de BDC de azdata](#azdata-bdc-spark-session-log) | Obtiene los registros de ejecución de una sesión de Spark activa.
[Estado de sesión de Spark de BDC de azdata](#azdata-bdc-spark-session-state) | Obtiene el estado de ejecución de una sesión de Spark activa.
[azdata eliminación de sesión Spark de BDC](#azdata-bdc-spark-session-delete) | Elimine una sesión de Spark.
## <a name="azdata-bdc-spark-session-create"></a>creación de sesión Spark de BDC de azdata
Esto crea una nueva sesión interactiva de Spark. El autor de la llamada debe especificar el tipo de sesión de Spark. Esta sesión permanece más allá de la duración de una ejecución de azdata y debe eliminarse con "eliminación de sesión de Spark"
```bash
azdata bdc spark session create [--session-kind -k] 
                                [--jar-files -j]  
                                [--py-files -p]  
                                [--files -f]  
                                [--driver-memory]  
                                [--driver-cores]  
                                [--executor-memory]  
                                [--executor-cores]  
                                [--executor-count]  
                                [--archives -a]  
                                [--queue -q]  
                                [--name -n]  
                                [--config -c]  
                                [--timeout-seconds -t]
```
### <a name="examples"></a>Ejemplos
Cree una sesión.
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--session-kind -k`
Nombre del tipo de sesión que se va a crear.  Una de Spark, pyspark, sparkr o SQL.
#### `--jar-files -j`
Lista de rutas de acceso de archivo jar.  Para pasar un código JSON de lista, codifique los valores.  Ejemplo: "[" entry1 "," entry2 "]".
#### `--py-files -p`
Lista de rutas de acceso de archivos de Python.  Para pasar un código JSON de lista, codifique los valores.  Ejemplo: "[" entry1 "," entry2 "]".
#### `--files -f`
Lista de rutas de acceso de archivo.  Para pasar un código JSON de lista, codifique los valores.  Ejemplo: "[" entry1 "," entry2 "]".
#### `--driver-memory`
Cantidad de memoria que se va a asignar al controlador.  Especifique las unidades como parte del valor.  Ejemplo de 512M o 2G.
#### `--driver-cores`
Cantidad de núcleos de CPU que se asignan al controlador.
#### `--executor-memory`
Cantidad de memoria que se va a asignar al Ejecutor.  Especifique las unidades como parte del valor.  Ejemplo de 512M o 2G.
#### `--executor-cores`
Cantidad de núcleos de CPU que se van a asignar al Ejecutor.
#### `--executor-count`
Número de instancias del Ejecutor que se va a ejecutar.
#### `--archives -a`
Lista de rutas de acceso de los archivos.  Para pasar un código JSON de lista, codifique los valores.  Ejemplo: "[" entry1 "," entry2 "]".
#### `--queue -q`
Nombre de la cola de Spark en la que se va a ejecutar la sesión.
#### `--name -n`
Nombre de la sesión de Spark.
#### `--config -c`
Lista de pares nombre-valor que contienen los valores de configuración de Spark.  Codificado como diccionario JSON.  Ejemplo: "{" Name ":" Value "," nombre2 ":" value2 "}".
#### `--timeout-seconds -t`
Tiempo de espera de inactividad de sesión en segundos.
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
## <a name="azdata-bdc-spark-session-list"></a>lista de sesiones de Spark de BDC de azdata
Enumere todas las sesiones activas en Spark.
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>Ejemplos
Enumere todas las sesiones activas.
```bash
azdata spark session list
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
## <a name="azdata-bdc-spark-session-info"></a>información de sesión de Spark de BDC de azdata
Obtiene la información de sesión de una sesión de Spark activa con el identificador especificado.  El ID. de sesión se devuelve de ' Spark Session Create '.
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>Ejemplos
Obtiene la información de la sesión de la sesión con el identificador 0.
```bash
azdata spark session info --session-id 0
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
## <a name="azdata-bdc-spark-session-log"></a>registro de sesión Spark de BDC de azdata
Obtiene las entradas del registro de sesión para una sesión de Spark activa con el identificador especificado.  El ID. de sesión se devuelve de ' Spark Session Create '.
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>Ejemplos
Obtiene el registro de sesión para la sesión con el identificador 0.
```bash
azdata spark session log --session-id 0
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
## <a name="azdata-bdc-spark-session-state"></a>Estado de sesión de Spark de BDC de azdata
Esto obtiene el estado de sesión para una sesión de Spark activa con el identificador especificado.  El ID. de sesión se devuelve de ' Spark Session Create '.
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>Ejemplos
Obtiene el estado de sesión de la sesión con el identificador 0.
```bash
azdata spark session state --session-id 0
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
## <a name="azdata-bdc-spark-session-delete"></a>azdata eliminación de sesión Spark de BDC
Esto elimina una sesión de Spark interactiva. El ID. de sesión se devuelve de ' Spark Session Create '.
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>Ejemplos
Elimina una sesión.
```bash
azdata spark session delete --session-id 0
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

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata** , consulte [instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
