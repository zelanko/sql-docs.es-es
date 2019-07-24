---
title: referencia de lote de Spark para BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos del lote de Spark para BDC de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6e242b26f439b49dbf0b3cf5ab50ea46c273f45f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426165"
---
# <a name="azdata-bdc-spark-batch"></a>lote de Spark para BDC de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos del **lote de Spark de BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[creación de lotes de Spark para BDC de azdata](#azdata-bdc-spark-batch-create) | Cree un lote de Spark nuevo.
[lista de lotes de Spark de BDC de azdata](#azdata-bdc-spark-batch-list) | Enumera todos los lotes de Spark.
[información de lote de Spark de BDC de azdata](#azdata-bdc-spark-batch-info) | Obtener información acerca de un lote de Spark activo.
[registro por lotes de Spark para BDC de azdata](#azdata-bdc-spark-batch-log) | Obtiene los registros de ejecución de un lote de Spark.
[Estado de lote de Spark de BDC de azdata](#azdata-bdc-spark-batch-state) | Obtiene el estado de ejecución de un lote de Spark.
[eliminación por lotes de Spark de BDC de azdata](#azdata-bdc-spark-batch-delete) | Eliminar un lote de Spark.
## <a name="azdata-bdc-spark-batch-create"></a>creación de lotes de Spark para BDC de azdata
Esto crea un nuevo trabajo de Spark de Batch que ejecuta el código proporcionado.
```bash
azdata bdc spark batch create --file -f 
                              [--class-name -c]  
                              [--arguments -a]  
                              [--jar-files -j]  
                              [--py-files -p]  
                              [--files]  
                              [--driver-memory]  
                              [--driver-cores]  
                              [--executor-memory]  
                              [--executor-cores]  
                              [--executor-count]  
                              [--archives]  
                              [--queue -q]  
                              [--name -n]  
                              [--config]
```
### <a name="examples"></a>Ejemplos
Cree un lote de Spark nuevo.
```bash
azdata spark batch create --code "2+2"
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--file -f`
Ruta de acceso al archivo que se va a ejecutar.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--class-name -c`
Nombre de la clase que se va a ejecutar al pasar uno o varios archivos jar.
#### `--arguments -a`
Lista de argumentos.  Para pasar un código JSON de lista, codifique los valores.  Ejemplo: "[" entry1 "," entry2 "]".
#### `--jar-files -j`
Lista de rutas de acceso de archivo jar.  Para pasar un código JSON de lista, codifique los valores.  Ejemplo: "[" entry1 "," entry2 "]".
#### `--py-files -p`
Lista de rutas de acceso de archivos de Python.  Para pasar un código JSON de lista, codifique los valores.  Ejemplo: "[" entry1 "," entry2 "]".
#### `--files`
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
#### `--archives`
Lista de rutas de acceso de los archivos.  Para pasar un código JSON de lista, codifique los valores.  Ejemplo: "[" entry1 "," entry2 "]".
#### `--queue -q`
Nombre de la cola de Spark en la que se va a ejecutar la sesión.
#### `--name -n`
Nombre de la sesión de Spark.
#### `--config`
Lista de pares nombre-valor que contienen los valores de configuración de Spark.  Codificado como diccionario JSON.  Ejemplo: "{" Name ":" Value "," nombre2 ":" value2 "}".
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
## <a name="azdata-bdc-spark-batch-list"></a>lista de lotes de Spark de BDC de azdata
Enumera todos los lotes de Spark.
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>Ejemplos
Enumera todos los lotes activos.
```bash
azdata spark batch list
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
## <a name="azdata-bdc-spark-batch-info"></a>información de lote de Spark de BDC de azdata
Obtiene la información de un lote de Spark con el identificador especificado.  El identificador de lote se devuelve de ' Spark batch Create '.
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>Ejemplos
Obtiene la información de lote del lote con el identificador 0.
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--batch-id -i`
Número de ID. de lote de Spark.
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
## <a name="azdata-bdc-spark-batch-log"></a>registro por lotes de Spark para BDC de azdata
Obtiene las entradas del registro por lotes para un lote de Spark con el identificador especificado.  El identificador de lote se devuelve de ' Spark batch Create '.
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>Ejemplos
Obtiene el registro de lote del lote con el identificador 0.
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--batch-id -i`
Número de ID. de lote de Spark.
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
## <a name="azdata-bdc-spark-batch-state"></a>Estado de lote de Spark de BDC de azdata
Esto obtiene el estado de lote para un lote de Spark con el identificador especificado.  El identificador de lote se devuelve de ' Spark batch Create '.
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>Ejemplos
Obtiene el estado de lote del lote con el identificador 0.
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--batch-id -i`
Número de ID. de lote de Spark.
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
## <a name="azdata-bdc-spark-batch-delete"></a>eliminación por lotes de Spark de BDC de azdata
Esto elimina un lote de Spark. El identificador de lote se devuelve de ' Spark batch Create '.
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>Ejemplos
Eliminar un lote.
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--batch-id -i`
Número de ID. de lote de Spark.
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
