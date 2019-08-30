---
title: referencia de la aplicación de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos de la aplicación de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ec7e461705138905713b803e2f0f96934044d971
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155303"
---
# <a name="azdata-app"></a>aplicación de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

Este artículo es un artículo de referencia para **azdata**. 

## <a name="commands"></a>Comandos:
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
azdata app init 
```
### <a name="examples"></a>Ejemplos
Aplica scaffolding solo en el archivo `spec.yaml` de una aplicación nueva.
```bash
azdata app init --spec
```
Scaffolding un nuevo esqueleto de aplicación de aplicación de R `r` basado en la plantilla.
```bash
azdata app init --name reduce --template r
```
Scaffolding un nuevo esqueleto de aplicación de aplicación de Python `python` basado en la plantilla.
```bash
azdata app init --name reduce --template python
```
Scaffolding un nuevo esqueleto de aplicación de aplicación de SSIS `ssis` basado en la plantilla.
```bash
azdata app init --name reduce --template ssis            
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
## <a name="azdata-app-create"></a>azdata app create
Crea una aplicación.
```bash
azdata app create 
```
### <a name="examples"></a>Ejemplos
Crea una aplicación desde un directorio que contenga un archivo spec.yaml de especificación de implementación válido.
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
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
## <a name="azdata-app-update"></a>azdata app update
Actualiza una aplicación.
```bash
azdata app update 
```
### <a name="examples"></a>Ejemplos
Actualiza una aplicación existente desde un directorio que contenga un archivo spec.yaml de especificación de implementación válido.
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
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
## <a name="azdata-app-list"></a>azdata app list
Muestra una lista de aplicaciones.
```bash
azdata app list 
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
## <a name="azdata-app-delete"></a>azdata app delete
Elimina una aplicación.
```bash
azdata app delete 
```
### <a name="examples"></a>Ejemplos
Elimina aplicaciones por nombre y versión.
```bash
azdata app delete --name reduce --version v1    
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
## <a name="azdata-app-run"></a>azdata app run
Ejecuta una aplicación.
```bash
azdata app run 
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
## <a name="azdata-app-describe"></a>azdata app describe
Describe una aplicación.
```bash
azdata app describe 
```
### <a name="examples"></a>Ejemplos
Describe la aplicación.
```bash
azdata app describe --name reduce --version v1    
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

## <a name="next-steps"></a>Pasos siguientes

- Para obtener más información sobre otros comandos de **azdata**, vea la [Referencia de azdata](reference-azdata.md). 

- Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
