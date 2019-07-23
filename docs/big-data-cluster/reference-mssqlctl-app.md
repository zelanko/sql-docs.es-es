---
title: referencia de la aplicación mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de la aplicación mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0df3e9ca007fb6546310236f4c23d1775687cc5
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388391"
---
# <a name="mssqlctl-app"></a>Aplicación mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos de la **aplicación** en la herramienta **mssqlctl** . Para obtener más información sobre otros comandos de **mssqlctl** , consulte [referencia de mssqlctl](reference-mssqlctl.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[plantilla de aplicación de mssqlctl](reference-mssqlctl-app-template.md) | Templa.
[mssqlctl App init](#mssqlctl-app-init) | Kickstart nuevo esqueleto de la aplicación.
[creación de la aplicación mssqlctl](#mssqlctl-app-create) | Cree la aplicación.
[actualización de la aplicación mssqlctl](#mssqlctl-app-update) | Actualice la aplicación.
[lista de aplicaciones de mssqlctl](#mssqlctl-app-list) | Enumerar las aplicaciones.
[eliminación de la aplicación mssqlctl](#mssqlctl-app-delete) | Eliminar aplicación.
[ejecución de la aplicación mssqlctl](#mssqlctl-app-run) | Ejecute la aplicación.
[Descripción de la aplicación mssqlctl](#mssqlctl-app-describe) | Describir aplicación.
## <a name="mssqlctl-app-init"></a>mssqlctl App init
Ayuda a Kickstart nuevos esqueletos de aplicación o archivos de especificación basados en entornos en tiempo de ejecución.
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>Ejemplos
Aplicar scaffolding a una `spec.yaml` nueva aplicación únicamente.
```bash
mssqlctl app init --spec
```
Scaffolding un nuevo esqueleto de la aplicación de R `r` basado en la plantilla.
```bash
mssqlctl app init --name reduce --template r
```
Scaffolding un nuevo esqueleto de la aplicación de Python `python` basado en la plantilla.
```bash
mssqlctl app init --name reduce --template python
```
Scaffolding un nuevo esqueleto de la aplicación SSIS basado `ssis` en la plantilla.
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Genere solo una especificación de aplicación. yaml.
#### `--name -n`
Nombre de la aplicación.
#### `--version -v`
Versión de la aplicación.
#### `--template -t`
Nombre de la plantilla. Para obtener una lista completa de los nombres de plantilla admitidos, ejecute`mssqlctl app template list`
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
## <a name="mssqlctl-app-create"></a>creación de la aplicación mssqlctl
Cree una aplicación.
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>Ejemplos
Cree una nueva aplicación desde un directorio que contenga una especificación de implementación Spec. yaml válida.
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
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
## <a name="mssqlctl-app-update"></a>actualización de la aplicación mssqlctl
Actualizar una aplicación.
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>Ejemplos
Actualizar una aplicación existente desde un directorio que contenga una especificación de implementación Spec. yaml válida.
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
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
## <a name="mssqlctl-app-list"></a>lista de aplicaciones de mssqlctl
Enumerar una o más aplicaciones.
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>Ejemplos
Enumerar aplicación por nombre y versión.
```bash
mssqlctl app list --name reduce  --version v1
```
Enumere todas las versiones de la aplicación por nombre.
```bash
mssqlctl app list --name reduce
```
Enumere todas las versiones de la aplicación por nombre.
```bash
mssqlctl app list
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
## <a name="mssqlctl-app-delete"></a>eliminación de la aplicación mssqlctl
Eliminar una aplicación.
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>Ejemplos
Elimine la aplicación por nombre y versión.
```bash
mssqlctl app delete --name reduce --version v1    
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
## <a name="mssqlctl-app-run"></a>ejecución de la aplicación mssqlctl
Ejecute una aplicación.
```bash
mssqlctl app run --name -n 
                 --version -v  
                 [--inputs]
```
### <a name="examples"></a>Ejemplos
Ejecute la aplicación sin parámetros de entrada.
```bash
mssqlctl app run --name reduce --version v1
```
Ejecute la aplicación con 1 parámetro de entrada.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
Ejecute la aplicación con varios parámetros de entrada.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6    
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
## <a name="mssqlctl-app-describe"></a>Descripción de la aplicación mssqlctl
Describir una aplicación.
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>Ejemplos
Describir la aplicación.
```bash
mssqlctl app describe --name reduce --version v1    
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

Para obtener más información sobre otros comandos de **mssqlctl** , consulte [referencia de mssqlctl](reference-mssqlctl.md). Para obtener más información sobre cómo instalar la herramienta **mssqlctl** , consulte [instalación de mssqlctl para administrar clústeres de macrodatos SQL Server 2019](deploy-install-mssqlctl.md).