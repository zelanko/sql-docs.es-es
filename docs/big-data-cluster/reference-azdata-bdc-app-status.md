---
title: Referencia de azdata bdc app status
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc app status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4435a1683b42b48e83aa2902aaba59c4b7a2ab22
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531871"
---
# <a name="azdata-bdc-app-status"></a>azdata bdc app status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

En el artículo siguiente se proporciona referencia de los comandos de `sql` de la herramienta `azdata`. Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc app status show](#azdata-bdc-app-status-show) | Estado del servicio de aplicaciones.
## <a name="azdata-bdc-app-status-show"></a>azdata bdc app status show
Estado del servicio de aplicaciones.
```bash
azdata bdc app status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>Ejemplos
Obtención del estado del servicio de aplicaciones.
```bash
azdata bdc app status show
```
Obtención del estado del servicio de aplicaciones con todas las instancias.
```bash
azdata bdc app status show --all
```
Obtención del estado del recurso appproxy en el servicio de aplicaciones.
```bash
azdata bdc app status show --resource appproxy
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--resource -r`
Obtención de este recurso en este servicio.
#### `--all -a`
Representación de todas las instancias de cada recurso en el servicio.
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
