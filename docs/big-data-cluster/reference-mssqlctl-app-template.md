---
title: referencia de plantillas de aplicación mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de plantilla de aplicación mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e73b0ddf9e30c5e38fd54d34ab93526213fe061
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800972"
---
# <a name="mssqlctl-app-template"></a>Plantilla de aplicación mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **plantilla de aplicación** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[lista de plantillas de aplicación mssqlctl](#mssqlctl-app-template-list) | Obtener plantillas compatibles.
[incorporación de cambios de plantilla de aplicación de mssqlctl](#mssqlctl-app-template-pull) | Descargue plantillas compatibles.
## <a name="mssqlctl-app-template-list"></a>lista de plantillas de aplicación mssqlctl
Obtener plantillas compatibles en el repositorio de github [URL] especificado.
```bash
mssqlctl app template list [--url -u] 
                           
```
### <a name="examples"></a>Ejemplos
Capturar todas las plantillas en la ubicación predeterminada del repositorio de plantillas.
```bash
mssqlctl app template list
```
Capturar todas las plantillas en una ubicación de otro repositorio.
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>Parámetros opcionales
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
## <a name="mssqlctl-app-template-pull"></a>incorporación de cambios de plantilla de aplicación de mssqlctl
Descargue plantillas compatibles en el repositorio de github [URL] especificado.
```bash
mssqlctl app template pull [--name -n] 
                           [--url -u]  
                           [--destination -d]
```
### <a name="examples"></a>Ejemplos
Descargar todas las plantillas en la ubicación predeterminada del repositorio de plantillas.
```bash
mssqlctl app template pull
```
Descargar todas las plantillas en una ubicación de otro repositorio.
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
Descargar plantilla individual por nombre.
```bash
mssqlctl app template pull --name ssis            
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre de la plantilla. Para obtener una lista completa Desactivar namesrun plantilla compatible `mssqlctl app template list`
#### `--url -u`
Especifique una ubicación de repositorio de plantillas diferentes. Valor predeterminado: https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
Dónde colocar la plantilla de aplicación esqueleto.
`./templates`
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