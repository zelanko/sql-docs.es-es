---
title: Referencia de azdata bdc spark session
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc spark session.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9bf2cdca204598d72f511364f59f45f551298703
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811293"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark session

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

En el siguiente artículo se proporciona una referencia sobre los comandos de **bdc spark session** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata bdc spark session create](#azdata-bdc-spark-session-create) | Cree una sesión de Spark.
[azdata bdc spark session list](#azdata-bdc-spark-session-list) | Enumere todas las sesiones activas en Spark.
[azdata bdc spark session info](#azdata-bdc-spark-session-info) | Obtenga información sobre una sesión de Spark activa.
[azdata bdc spark session log](#azdata-bdc-spark-session-log) | Obtenga los registros de ejecución de una sesión de Spark activa.
[azdata bdc spark session state](#azdata-bdc-spark-session-state) | Obtenga el estado de la ejecución de una sesión de Spark activa.
[azdata bdc spark session delete](#azdata-bdc-spark-session-delete) | Elimine una sesión de Spark.
## <a name="azdata-bdc-spark-session-create"></a>azdata bdc spark session create
Este procedimiento crea una sesión interactiva de Spark. El autor de la llamada debe especificar el tipo de la sesión de Spark. Esta sesión permanece más allá de la duración de una ejecución de azdata y debe eliminarse con "spark session delete".
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
Crear una sesión.
```bash
azdata bdc spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--session-kind -k`
Nombre del tipo de sesión que se va a crear.  spark, pyspark, sparkr o sql.
#### `--jar-files -j`
Lista de rutas de acceso de archivo jar.  Para pasarlos en una lista, JSON codifica los valores.  Ejemplo: '["entry1", "entry2"]'.
#### `--py-files -p`
Lista de rutas de acceso de archivo de Python.  Para pasarlos en una lista, JSON codifica los valores.  Ejemplo: '["entry1", "entry2"]'.
#### `--files -f`
Lista de rutas de acceso de archivo.  Para pasarlos en una lista, JSON codifica los valores.  Ejemplo: '["entry1", "entry2"]'.
#### `--driver-memory`
Cantidad de memoria que se va a asignar al controlador.  Especifique las unidades como parte del valor.  Por ejemplo, 512M o 2G.
#### `--driver-cores`
Cantidad de núcleos de CPU que se van a asignar al controlador.
#### `--executor-memory`
Cantidad de memoria que se va a asignar al ejecutor.  Especifique las unidades como parte del valor.  Por ejemplo, 512M o 2G.
#### `--executor-cores`
Cantidad de núcleos de CPU que se van a asignar al ejecutor.
#### `--executor-count`
Número de instancias del ejecutor que se van a ejecutar.
#### `--archives -a`
Lista de rutas de acceso de los archivos.  Para pasarlos en una lista, JSON codifica los valores.  Ejemplo: '["entry1", "entry2"]'.
#### `--queue -q`
Nombre de la cola de Spark en la que se va a ejecutar la sesión.
#### `--name -n`
Nombre de la sesión de Spark.
#### `--config -c`
Lista de pares nombre-valor que contienen los valores de configuración de Spark.  Cifrada como un diccionario JSON.  Ejemplo: '{"name":"value", "name2":"value2"}'.
#### `--timeout-seconds -t`
Tiempo de espera de sesión inactivo en segundos.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Sirve para aumentar el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Sirve para mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Sirve para aumentar el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-spark-session-list"></a>azdata bdc spark session list
Enumere todas las sesiones activas en Spark.
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>Ejemplos
Enumere todas las sesiones activas.
```bash
azdata bdc spark session list
```
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Sirve para aumentar el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Sirve para mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Sirve para aumentar el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark session info
Obtiene la información de una sesión de Spark activa con el identificador especificado.  El identificador de sesión se devuelve desde “spark session create”.
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>Ejemplos
Obtener la información de la sesión con el identificador 0.
```bash
azdata bdc spark session info --session-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--session-id -i`
Número de identificador de sesión de Spark.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Sirve para aumentar el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Sirve para mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Sirve para aumentar el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark session log
Obtiene las entradas del registro de una sesión de Spark activa con el identificador especificado.  El identificador de sesión se devuelve desde “spark session create”.
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>Ejemplos
Obtener el registro de la sesión con el identificador 0.
```bash
azdata bdc spark session log --session-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--session-id -i`
Número de identificador de sesión de Spark.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Sirve para aumentar el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Sirve para mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Sirve para aumentar el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark session state
Obtiene el estado de una sesión de Spark activa con el identificador especificado.  El identificador de sesión se devuelve desde “spark session create”.
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>Ejemplos
Obtener el estado de la sesión con el identificador 0.
```bash
azdata bdc spark session state --session-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--session-id -i`
Número de identificador de sesión de Spark.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Sirve para aumentar el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Sirve para mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Sirve para aumentar el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark session delete
Este procedimiento elimina una sesión de Spark interactiva. El identificador de sesión se devuelve desde “spark session create”.
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>Ejemplos
Eliminar una sesión.
```bash
azdata bdc spark session delete --session-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--session-id -i`
Número de identificador de sesión de Spark.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Sirve para aumentar el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Sirve para mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Sirve para aumentar el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
