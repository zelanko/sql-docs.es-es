---
title: Referencia de azdata bdc status
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 712a5ac51f13450fe5cf6b8cc13400d5666eb4a0
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155194"
---
# <a name="azdata-bdc-status"></a>azdata bdc status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artículo es un artículo de referencia para **azdata**. 

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata bdc status show](#azdata-bdc-status-show) | Muestra el estado del BDC.
## <a name="azdata-bdc-status-show"></a>azdata bdc status show
Muestra el estado del BDC.
```bash
azdata bdc status show [--resource -r] 
                       [--all -a]
```
### <a name="examples"></a>Ejemplos
Estado del clúster de macrodatos en el que ha iniciado sesión el usuario.
```bash
azdata bdc status show
```
Estado de BDC con todas las instancias de los recursos incluidos.
```bash
azdata bdc status show --all
```
Estado de BDC de los servicios que incluyen el recurso de control.
```bash
azdata bdc status show --resource control
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--resource -r`
Obtiene los servicios asociados a este recurso.
#### `--all -a`
Mostrar todas las instancias de cada recurso dentro de los servicios.
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
