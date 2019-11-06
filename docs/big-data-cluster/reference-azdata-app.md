---
title: referencia de la aplicación de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos de la aplicación de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 371321c8b91d3d7c56ac2721deb29a664209f004
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531905"
---
# <a name="azdata-app"></a>aplicación de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

En el artículo siguiente se proporciona una referencia de los comandos `sql` de la herramienta `azdata`. Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata app template](reference-azdata-app-template.md) | Plantillas.
[azdata app init](#azdata-app-init) | Inicio rápido de un nuevo esqueleto de la aplicación.
[azdata app create](#azdata-app-create) | Crea una aplicación.
[azdata app update](#azdata-app-update) | Actualiza una aplicación.
[azdata app list](#azdata-app-list) | Muestra una lista de aplicaciones.
[azdata app delete](#azdata-app-delete) | Elimina una aplicación.
[azdata app run](#azdata-app-run) | Ejecuta una aplicación.
[azdata app describe](#azdata-app-describe) | Describe una aplicación.
## <a name="azdata-app-init"></a>azdata app init
Le permite iniciar rápidamente un nuevo esqueleto de la aplicación o archivos de especificaciones basados en entornos de ejecución.
```bash
azdata app init [--spec -s] 
                [--name -n]  
                [--version -v]  
                [--template -t]  
                [--destination -d]  
                [--url -u]
```
### <a name="examples"></a>Ejemplos
Aplica scaffolding solo en el archivo `spec.yaml` de una aplicación nueva.
```bash
azdata app init --spec
```
Aplica scaffolding en un nuevo esqueleto de aplicación de R en función de la plantilla de `r`.
```bash
azdata app init --name reduce --template r
```
Aplica scaffolding en un nuevo esqueleto de aplicación de Python en función de la plantilla de `python`.
```bash
azdata app init --name reduce --template python
```
Aplica scaffolding en un nuevo esqueleto de aplicación de SSIS en función de la plantilla de `ssis`.
```bash
azdata app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Generar solo un archivo spec.yaml de la aplicación.
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
#### `--template -t`
Nombre de la plantilla. Para obtener la lista completa de nombres de plantillas admitidos, ejecute `azdata app template list`.
#### `--destination -d`
Dónde colocar el esqueleto de la aplicación. Valor predeterminado: directorio de trabajo actual.
#### `--url -u`
Especifique otra ubicación de repositorio de plantillas. Valor predeterminado: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-create"></a>azdata app create
Crea una aplicación.
```bash
azdata app create --spec -s 
```
### <a name="examples"></a>Ejemplos
Crea una aplicación desde un directorio que contenga un archivo spec.yaml de especificación de implementación válido.
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--spec -s`
Ruta a un directorio con un archivo de especificación de YAML en el que se describe la aplicación.
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
## <a name="azdata-app-update"></a>azdata app update
Actualiza una aplicación.
```bash
azdata app update [--spec -s] 
                  [--yes -y]
```
### <a name="examples"></a>Ejemplos
Actualiza una aplicación existente desde un directorio que contenga un archivo spec.yaml de especificación de implementación válido.
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Ruta a un directorio con un archivo de especificación de YAML en el que se describe la aplicación.
#### `--yes -y`
No pide la confirmación al actualizar una aplicación desde el archivo spec.yaml de CWD.
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
## <a name="azdata-app-list"></a>azdata app list
Muestra una lista de aplicaciones.
```bash
azdata app list [--name -n] 
                [--version -v]
```
### <a name="examples"></a>Ejemplos
Muestra las aplicaciones por nombre y versión.
```bash
azdata app list --name reduce  --version v1
```
Muestra una lista de todas las versiones de la aplicación por nombre.
```bash
azdata app list --name reduce
```
Muestra una lista de todas las versiones de la aplicación por nombre.
```bash
azdata app list
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
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
## <a name="azdata-app-delete"></a>azdata app delete
Elimina una aplicación.
```bash
azdata app delete --name -n 
                  --version -v
```
### <a name="examples"></a>Ejemplos
Elimina aplicaciones por nombre y versión.
```bash
azdata app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
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
## <a name="azdata-app-run"></a>azdata app run
Ejecuta una aplicación.
```bash
azdata app run --name -n 
               --version -v  
               [--inputs]
```
### <a name="examples"></a>Ejemplos
Ejecuta una aplicación sin parámetros de entrada.
```bash
azdata app run --name reduce --version v1
```
Ejecuta una aplicación con un parámetro de entrada.
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
Ejecuta una aplicación con varios parámetros de entrada.
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--inputs`
Parámetros de entrada de la aplicación en formato `name=value` de CSV.
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
## <a name="azdata-app-describe"></a>azdata app describe
Describe una aplicación.
```bash
azdata app describe [--spec -s] 
                    [--name -n]  
                    [--version -v]
```
### <a name="examples"></a>Ejemplos
Describe la aplicación.
```bash
azdata app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Ruta a un directorio con un archivo de especificación de YAML en el que se describe la aplicación.
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
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
