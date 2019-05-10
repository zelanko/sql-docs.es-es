---
title: referencia de aplicación mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de la aplicación de mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 850964adc9cd790a27cf69e3e0f5229cdaf589c8
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775218"
---
# <a name="mssqlctl-app"></a>Aplicación mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **aplicación** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[plantilla de aplicación mssqlctl](reference-mssqlctl-app-template.md) | plantillas.
[mssqlctl aplicación init](#mssqlctl-app-init) | Nueva aplicación KickStart esqueleto.
[mssqlctl app create](#mssqlctl-app-create) | Crear la aplicación.
[mssqlctl app update](#mssqlctl-app-update) | Actualizar la aplicación.
[lista de aplicaciones mssqlctl](#mssqlctl-app-list) | Lista de aplicaciones.
[mssqlctl app delete](#mssqlctl-app-delete) | Eliminar la aplicación.
[ejecución de la aplicación mssqlctl](#mssqlctl-app-run) | Ejecutar la aplicación.
[Describir la aplicación mssqlctl](#mssqlctl-app-describe) | Describir la aplicación.
## <a name="mssqlctl-app-init"></a>mssqlctl aplicación init
Le ayuda a kickstart nueva aplicación esqueleto o archivos de especificación en función de los entornos en tiempo de ejecución.
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>Ejemplos
Aplicar scaffolding a una nueva aplicación `spec.yaml` solo.
```bash
mssqlctl app init --spec
```
Aplicar la técnica scaffolding en función de un esqueleto de aplicación de aplicación de nuevo R el `r` plantilla.
```bash
mssqlctl app init --name reduce --template r
```
Aplicar la técnica scaffolding un esqueleto de aplicación de aplicación de Python nuevo según la `python` plantilla.
```bash
mssqlctl app init --name reduce --template python
```
Aplicar la técnica scaffolding SSIS aplicación aplicación esqueleto nuevo según la `ssis` plantilla.
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Generar simplemente una spec.yaml de aplicación.
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
#### `--template -t`
Nombre de la plantilla. Para obtener una lista completa desactivar los nombres de la plantilla compatible ejecutar `mssqlctl app template list`
#### `--destination -d`
Dónde colocar el esqueleto de la aplicación. Valor predeterminado: directorio de trabajo actual.
#### `--url -u`
Especifique una ubicación de repositorio de plantillas diferentes. Valor predeterminado: https://github.com/Microsoft/SQLBDC-AppDeploy.git
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-app-create"></a>Crear aplicación mssqlctl
Crear una aplicación.
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>Ejemplos
Cree una nueva aplicación desde un directorio que contiene una especificación de implementación spec.yaml válido.
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--spec -s`
Ruta de acceso a un directorio con un archivo de YAML especificación que describe la aplicación.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-app-update"></a>mssqlctl app update
Actualización de una aplicación.
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>Ejemplos
Actualizar una aplicación existente desde un directorio que contiene una especificación de implementación spec.yaml válido.
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Ruta de acceso a un directorio con un archivo de YAML especificación que describe la aplicación.
#### `--yes -y`
No solicita confirmación al actualizar una aplicación partir spec.yaml archivo del CWD.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-app-list"></a>lista de aplicaciones mssqlctl
Una de las aplicaciones de la lista.,
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>Ejemplos
Aplicación de lista por nombre y versión.
```bash
mssqlctl app list --name reduce  --version v1
```
Enumerar todas las versiones de la aplicación por su nombre.
```bash
mssqlctl app list --name reduce
```
Enumerar todas las versiones de la aplicación por su nombre.
```bash
mssqlctl app list
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-app-delete"></a>eliminación de aplicación mssqlctl
Eliminar una aplicación.
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>Ejemplos
Eliminar la aplicación por nombre y versión.
```bash
mssqlctl app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-app-run"></a>ejecución de la aplicación mssqlctl
Ejecutar una aplicación.
```bash
mssqlctl app run --name -n 
                 --version -v  
                 [--inputs]
```
### <a name="examples"></a>Ejemplos
Ejecute la aplicación con ningún parámetro de entrada.
```bash
mssqlctl app run --name reduce --version v1
```
Ejecute la aplicación con 1 parámetro de entrada.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
Ejecutar la aplicación con varios parámetros de entrada.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--inputs`
Aplicación de parámetros de entrada en un archivo CSV `name=value` formato.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.
## <a name="mssqlctl-app-describe"></a>Describir la aplicación mssqlctl
Descripción de una aplicación.
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>Ejemplos
Descripción de la aplicación.
```bash
mssqlctl app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--spec -s`
Ruta de acceso a un directorio con un archivo de YAML especificación que describe la aplicación.
#### `--name -n`
Nombre de aplicación.
#### `--version -v`
Versión de la aplicación.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumentar el nivel de detalle de registro para mostrar que todos los registros de depuración.
#### `--help -h`
Mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumentar el nivel de detalle de registro. Use--debug para registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).