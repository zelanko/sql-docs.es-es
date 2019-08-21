---
title: Referencia de azdata app template
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos azdata app template.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 265f8be659594ee549bf0aa2c5ffcf19263a2294
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653205"
---
# <a name="azdata-app-template"></a>azdata app template

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se ofrece una referencia sobre los comandos **app template** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata app template list](#azdata-app-template-list) | Capture plantillas admitidas.
[azdata app template pull](#azdata-app-template-pull) | Descargue plantillas admitidas.
## <a name="azdata-app-template-list"></a>azdata app template list
Capture plantillas admitidas en el repositorio de GitHub [URL] especificado.
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>Ejemplos
Capture todas las plantillas en la ubicación predeterminada del repositorio de plantillas.
```bash
azdata app template list
```
Capture todas las plantillas en otra ubicación del repositorio.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>Parámetros opcionales
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
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-app-template-pull"></a>azdata app template pull
Descargue plantillas admitidas en el repositorio de GitHub [URL] especificado.
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         [--destination -d]
```
### <a name="examples"></a>Ejemplos
Descargue todas las plantillas en la ubicación predeterminada del repositorio de plantillas.
```bash
azdata app template pull
```
Descargue todas las plantillas en otra ubicación del repositorio.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
Descargue una plantilla individual por nombre.
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre de plantilla. Para obtener una lista completa de nombres de plantilla admitidos, ejecute `azdata app template list`
#### `--url -u`
Especifique otra ubicación de repositorio de plantillas. Valor predeterminado: https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
Dónde colocar la plantilla de esqueleto de la aplicación.
`./templates`
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

Para obtener más información sobre otros comandos de **azdata**, vea [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata** , vea [instalar azdata para administrar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](deploy-install-azdata.md).
