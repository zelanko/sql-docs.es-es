---
title: Referencia de azdata bdc debug
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc debug.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e14528baf80d08841f6e9e17a0476dfa81fd48d
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153199"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artículo es un artículo de referencia para **azdata**. 

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata bdc debug copy-logs](#azdata-bdc-debug-copy-logs) | Copie registros.
[azdata bdc debug dump](#azdata-bdc-debug-dump) | Desencadene el volcado de registros.
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug copy-logs
Copie los registros de depuración del clúster de Big Data: la configuración Kubernetes es necesaria en el sistema.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--namespace -n`
Nombre del clúster de macrodatos; se usa para el espacio de nombres de Kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--container -c`
Copie los registros de los contenedores con un nombre similar. Opcional, de forma predeterminada, copia los registros de todos los contenedores. No se puede especificar varias veces. Si se especifica varias veces, se usará la última.
#### `--target-folder -d`
Ruta de acceso de la carpeta de destino en la que copiar los registros. Opcional, de forma predeterminada, crea el resultado en la carpeta local.  No se puede especificar varias veces. Si se especifica varias veces, se usará la última.
#### `--pod -p`
Copie los registros de los pods con un nombre similar. Opcional, de forma predeterminada copia los registros de todos los pods. No se puede especificar varias veces. Si se especifica varias veces, se usará la última.
#### `--timeout -t`
Número de segundos que se debe esperar a que se complete el comando. El valor predeterminado es 0, es decir, sin límite.
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
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
Desencadenar el volcado de registro y copiarlo desde la configuración de Container-Kubernetes es necesaria en el sistema.
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--namespace -n`
Nombre del clúster de macrodatos; se usa para el espacio de nombres de Kubernetes.
#### `--container -c`
Copie los registros de los contenedores con un nombre similar. Opcional, de forma predeterminada, copia los registros de todos los contenedores. No se puede especificar varias veces. Si se especifica varias veces, se usará la última.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target-folder -d`
Ruta de acceso de la carpeta de destino en la que copiar los registros. Opcional, de forma predeterminada, crea el resultado en la carpeta local.  No se puede especificar varias veces. Si se especifica varias veces, la última se usará `./output/dump`.
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
