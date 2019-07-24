---
title: referencia de la aplicación azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de la aplicación azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 793edde26ebebf9e55c5751adbedf662142280de
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426285"
---
# <a name="azdata-app"></a>aplicación azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos de la **aplicación** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[plantilla de aplicación de azdata](reference-azdata-app-template.md) | Templa.
[azdata App init](#azdata-app-init) | Kickstart nuevo esqueleto de la aplicación.
[creación de la aplicación azdata](#azdata-app-create) | Cree la aplicación.
[actualización de la aplicación azdata](#azdata-app-update) | Actualice la aplicación.
[lista de aplicaciones de azdata](#azdata-app-list) | Enumerar las aplicaciones.
[eliminación de la aplicación azdata](#azdata-app-delete) | Eliminar aplicación.
[ejecución de la aplicación azdata](#azdata-app-run) | Ejecute la aplicación.
[Descripción de la aplicación azdata](#azdata-app-describe) | Describir aplicación.
## <a name="azdata-app-init"></a>azdata App init
Ayuda a Kickstart nuevos esqueletos de aplicación o archivos de especificación basados en entornos en tiempo de ejecución.
```bash
azdata app init [--spec -s] 
                [--name -n]  
                [--version -v]  
                [--template -t]  
                [--destination -d]  
                [--url -u]
```
### <a name="examples"></a>Ejemplos
Aplicar scaffolding a una `spec.yaml` nueva aplicación únicamente.
```bash
azdata app init --spec
```
Scaffolding un nuevo esqueleto de la aplicación de R `r` basado en la plantilla.
```bash
azdata app init --name reduce --template r
```
Scaffolding un nuevo esqueleto de la aplicación de Python `python` basado en la plantilla.
```bash
azdata app init --name reduce --template python
```
Scaffolding un nuevo esqueleto de la aplicación SSIS basado `ssis` en la plantilla.
```bash
azdata app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Genere solo una especificación de aplicación. yaml.
#### `--name -n`
Nombre de la aplicación.
#### `--version -v`
Versión de la aplicación.
#### `--template -t`
Nombre de la plantilla. Para obtener una lista completa de los nombres de plantilla admitidos, ejecute`azdata app template list`
#### `--destination -d`
Dónde colocar el esqueleto de la aplicación. Valor predeterminado: directorio de trabajo actual.
#### `--url -u`
Especifique una ubicación de repositorio de plantillas diferente. Predeterminada https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-create"></a>creación de la aplicación azdata
Cree una aplicación.
```bash
azdata app create --spec -s 
                  
```
### <a name="examples"></a>Ejemplos
Cree una nueva aplicación desde un directorio que contenga una especificación de implementación Spec. yaml válida.
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--spec -s`
Ruta de acceso a un directorio con un archivo de especificación YAML que describe la aplicación.
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
## <a name="azdata-app-update"></a>actualización de la aplicación azdata
Actualizar una aplicación.
```bash
azdata app update [--spec -s] 
                  [--yes -y]
```
### <a name="examples"></a>Ejemplos
Actualizar una aplicación existente desde un directorio que contenga una especificación de implementación Spec. yaml válida.
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Ruta de acceso a un directorio con un archivo de especificación YAML que describe la aplicación.
#### `--yes -y`
No pedir confirmación al actualizar una aplicación desde el archivo spec. yaml de CWD.
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
## <a name="azdata-app-list"></a>lista de aplicaciones de azdata
Enumerar una o más aplicaciones.
```bash
azdata app list [--name -n] 
                [--version -v]
```
### <a name="examples"></a>Ejemplos
Enumerar aplicación por nombre y versión.
```bash
azdata app list --name reduce  --version v1
```
Enumere todas las versiones de la aplicación por nombre.
```bash
azdata app list --name reduce
```
Enumere todas las versiones de la aplicación por nombre.
```bash
azdata app list
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre de la aplicación.
#### `--version -v`
Versión de la aplicación.
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
## <a name="azdata-app-delete"></a>eliminación de la aplicación azdata
Eliminar una aplicación.
```bash
azdata app delete --name -n 
                  --version -v
```
### <a name="examples"></a>Ejemplos
Elimine la aplicación por nombre y versión.
```bash
azdata app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre de la aplicación.
#### `--version -v`
Versión de la aplicación.
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
## <a name="azdata-app-run"></a>ejecución de la aplicación azdata
Ejecute una aplicación.
```bash
azdata app run --name -n 
               --version -v  
               [--inputs]
```
### <a name="examples"></a>Ejemplos
Ejecute la aplicación sin parámetros de entrada.
```bash
azdata app run --name reduce --version v1
```
Ejecute la aplicación con 1 parámetro de entrada.
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
Ejecute la aplicación con varios parámetros de entrada.
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre de la aplicación.
#### `--version -v`
Versión de la aplicación.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--inputs`
Parámetros de entrada de la aplicación `name=value` en formato CSV.
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
## <a name="azdata-app-describe"></a>Descripción de la aplicación azdata
Describir una aplicación.
```bash
azdata app describe [--spec -s] 
                    [--name -n]  
                    [--version -v]
```
### <a name="examples"></a>Ejemplos
Describir la aplicación.
```bash
azdata app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Ruta de acceso a un directorio con un archivo de especificación YAML que describe la aplicación.
#### `--name -n`
Nombre de la aplicación.
#### `--version -v`
Versión de la aplicación.
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
