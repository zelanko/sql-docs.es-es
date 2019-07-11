---
title: referencia de plantillas de aplicación mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de plantilla de aplicación mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c0b9ab4dc278e04b2b112608699b9c60682de769
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728721"
---
# <a name="mssqlctl-app-template"></a>Plantilla de aplicación mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **plantilla de aplicación** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos:
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
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
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
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).