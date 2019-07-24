---
title: referencia de depuración de BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de depuración de BDC de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38c327287273ae6596326d88d9e0d67c8e014d47
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426235"
---
# <a name="azdata-bdc-debug"></a>depuración de BDC de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos de depuración de **BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[copia de depuración de BDC de azdata: registros](#azdata-bdc-debug-copy-logs) | Copiar registros.
[volcado de depuración de BDC de azdata](#azdata-bdc-debug-dump) | Volcado de registro del desencadenador.
## <a name="azdata-bdc-debug-copy-logs"></a>copia de depuración de BDC de azdata: registros
Copie los registros de depuración del clúster de Big Data-Kube config es necesario en el sistema.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--namespace -n`
Nombre del clúster de Big Data, que se usa para el espacio de nombres kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--container -c`
Copie los registros de los contenedores con un nombre similar, opcional; de forma predeterminada, copia los registros de todos los contenedores. No se puede especificar varias veces. Si se especifica varias veces, se usará la última
#### `--target-folder -d`
Ruta de acceso de la carpeta de destino en la que copiar registros. Opcional, crea el resultado en la carpeta local de forma predeterminada.  No se puede especificar varias veces. Si se especifica varias veces, se usará la última
#### `--pod -p`
Copie los registros de los pods con un nombre similar. Opcional, copia de forma predeterminada los registros para todos los pods. No se puede especificar varias veces. Si se especifica varias veces, se usará la última
#### `--timeout -t`
Número de segundos que se va a esperar a que se complete el comando. El valor predeterminado es 0, que es ilimitado.
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
## <a name="azdata-bdc-debug-dump"></a>volcado de depuración de BDC de azdata
Desencadenar el volcado de registro y copiarlo desde la configuración de Container-Kube es necesaria en el sistema.
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--namespace -n`
Nombre del clúster de Big Data, que se usa para el espacio de nombres kubernetes.
#### `--container -c`
Copie los registros de los contenedores con un nombre similar, opcional; de forma predeterminada, copia los registros de todos los contenedores. No se puede especificar varias veces. Si se especifica varias veces, se usará la última
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target-folder -d`
Ruta de acceso de la carpeta de destino en la que copiar registros. Opcional, crea el resultado en la carpeta local de forma predeterminada.  No se puede especificar varias veces. Si se especifica varias veces, se usará la última`./output/dump`
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
