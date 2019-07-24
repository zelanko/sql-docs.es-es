---
title: referencia de plantillas de aplicaciones de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de la plantilla de aplicación de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3b257a2bacc56a7907ab0d25f492ed0ebd605543
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426335"
---
# <a name="azdata-app-template"></a>plantilla de aplicación de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos de la **plantilla de aplicación** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[lista de plantillas de aplicaciones de azdata](#azdata-app-template-list) | Capturar plantillas admitidas.
[extracción de plantilla de aplicación de azdata](#azdata-app-template-pull) | Descargar plantillas admitidas.
## <a name="azdata-app-template-list"></a>lista de plantillas de aplicaciones de azdata
Capturar plantillas admitidas en el repositorio de github de [URL] especificado.
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>Ejemplos
Recupera todas las plantillas de la ubicación predeterminada del repositorio de plantillas.
```bash
azdata app template list
```
Recupera todas las plantillas en una ubicación de repositorio diferente.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>Parámetros opcionales
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
## <a name="azdata-app-template-pull"></a>extracción de plantilla de aplicación de azdata
Descargue las plantillas compatibles en el repositorio de github de [URL] especificado.
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         [--destination -d]
```
### <a name="examples"></a>Ejemplos
Descargue todas las plantillas de la ubicación predeterminada del repositorio de plantillas.
```bash
azdata app template pull
```
Descargue todas las plantillas en una ubicación de repositorio diferente.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
Descargar plantilla individual por nombre.
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre de la plantilla. Para obtener una lista completa de la plantilla admitida namesrun`azdata app template list`
#### `--url -u`
Especifique una ubicación de repositorio de plantillas diferente. Predeterminada https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
Dónde colocar la plantilla de esqueleto de la aplicación.
`./templates`
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
