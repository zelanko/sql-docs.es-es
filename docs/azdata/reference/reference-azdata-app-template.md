---
title: Referencia de azdata app template
titleSuffix: SQL Server big data clusters
description: Use este artículo de referencia para entender los comandos SQL en la herramienta azdata, en particular los comandos app template.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 37371ec8d909115aedf1eb745a78fec7af427cc4
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2020
ms.locfileid: "89734059"
---
# <a name="azdata-app-template"></a>azdata app template

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

En el artículo siguiente se proporciona una referencia de los comandos `sql` de la herramienta `azdata`. Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
| Comando | Descripción |
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
Especifique otra ubicación de repositorio de plantillas. Predeterminado: https://github.com/Microsoft/SQLBDC-AppDeploy.git
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org).
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
Nombre de la plantilla. Para obtener una lista completa de nombres de plantilla admitidos, ejecute `azdata app template list`
#### `--url -u`
Especifique otra ubicación de repositorio de plantillas. Predeterminado: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta `azdata`, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](../install/deploy-install-azdata.md).
