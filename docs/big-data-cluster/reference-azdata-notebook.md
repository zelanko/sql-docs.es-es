---
title: referencia de azdata Notebook
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de azdata Notebook.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b96c5e06ec51f53964a28cac86f385d6b42c1dc4
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426015"
---
# <a name="azdata-notebook"></a>cuaderno de azdata Notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos **Notebook** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[vista de azdata Notebook](#azdata-notebook-view) | Ver un cuaderno.  Opción para detener en el primer error de ejecución de celda.
[azdata Notebook ejecutado](#azdata-notebook-run) | Ejecute un cuaderno.  La ejecución se detiene en el primer error.
## <a name="azdata-notebook-view"></a>vista de azdata Notebook
Este comando puede tomar un archivo de Bloc de notas y convertir el formato de terminal, el código y la salida en el formato de terminal de color.
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>Ejemplos
Ver Notebook.  Esto muestra todas las celdas.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
Ver Notebook.  Esto muestra todas las celdas a menos que se encuentre una celda con el error en su salida.  En ese caso, la salida se detiene.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Ruta de acceso al bloc de notas que se va a ver.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--continue-on-error -c`
Continúe mostrando celdas adicionales que omiten los errores de celda que se encuentran en la salida del Bloc de notas.  El comportamiento predeterminado es detenerse en el error.  Al detener, se facilita la visualización de la primera celda que encontró un error.
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
## <a name="azdata-notebook-run"></a>azdata Notebook ejecutado
Este comando crea un directorio temporal y ejecuta el cuaderno determinado en él como directorio de trabajo.
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]
```
### <a name="examples"></a>Ejemplos
Ejecute Notebook.
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--path -p`
Ruta de acceso del archivo al bloc de notas que se va a ejecutar.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--output-path`
Ruta de acceso al directorio que se va a usar para la salida del cuaderno.  Notebook con los datos de salida y los archivos generados por el Bloc de notas se generan en relación con este directorio.
#### `--output-html`
Marca opcional indicatingg si se debe convertir Adicionalmente el Bloc de notas de salida en formato HTML.  Crea un segundo archivo de salida.
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
