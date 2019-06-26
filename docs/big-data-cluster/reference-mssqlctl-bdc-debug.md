---
title: mssqlctl bdc debug reference
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos de depuración mssqlctl bdc.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dde99490805ec0f78c9acbaa3875f1ae1406e77f
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394347"
---
# <a name="mssqlctl-bdc-debug"></a>depuración de bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **depuración bdc** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[mssqlctl bdc debug copy-logs](#mssqlctl-bdc-debug-copy-logs) | Copiar los registros.
[mssqlctl bdc debug dump](#mssqlctl-bdc-debug-dump) | Volcado del registro de desencadenador.
## <a name="mssqlctl-bdc-debug-copy-logs"></a>mssqlctl bdc debug copy-logs
Copiar los registros de depuración desde el clúster de datos grande: se requiere la configuración de kube en el sistema.
```bash
mssqlctl bdc debug copy-logs --namespace -n 
                             [--container -c]  
                             [--target-folder -d]  
                             [--pod -p]  
                             [--timeout -t]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--namespace -n`
Nombre BDC, usado para el espacio de nombres de kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--container -c`
Copiar los registros para los contenedores con un nombre similar, opcional, de forma predeterminada copia los registros para todos los contenedores. No se puede especificar varias veces. Si especifica varias veces, por última vez una se usará
#### `--target-folder -d`
Ruta de acceso de carpeta de destino para copiar los registros a. Opcional, crea el resultado en la carpeta local de forma predeterminada.  No se puede especificar varias veces. Si especifica varias veces, por última vez una se usará
#### `--pod -p`
Copiar los registros para los pods con un nombre similar. Opcional, en los registros de copias de forma predeterminada para todos los pods. No se puede especificar varias veces. Si especifica varias veces, por última vez una se usará
#### `--timeout -t`
El número de segundos que deben transcurrir para que se complete el comando. El valor predeterminado es 0, lo que es ilimitado
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
## <a name="mssqlctl-bdc-debug-dump"></a>mssqlctl bdc debug dump
Desencadenar el registro de volcado de memoria y copiarla desde el contenedor: se requiere la configuración de kube en el sistema.
```bash
mssqlctl bdc debug dump --namespace -n 
                        --container -c  
                        [--target-folder -d]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--namespace -n`
Nombre BDC, usado para el espacio de nombres de kubernetes.
#### `--container -c`
Copiar los registros para los contenedores con un nombre similar, opcional, de forma predeterminada copia los registros para todos los contenedores. No se puede especificar varias veces. Si especifica varias veces, por última vez una se usará
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--target-folder -d`
Ruta de acceso de carpeta de destino para copiar los registros a. Opcional, crea el resultado en la carpeta local de forma predeterminada.  No se puede especificar varias veces. Si especifica varias veces, por última vez una se usará `./output/dump`
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