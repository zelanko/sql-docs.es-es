---
title: referencia de depuración de clúster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de comandos de depuración de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4eafc3838d153a2616e34e98aed041374c04292d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779398"
---
# <a name="mssqlctl-cluster-debug"></a>Depuración de clúster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **depuración clúster** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[depuración mssqlctl copia-registros de clúster](#mssqlctl-cluster-debug-copy-logs) | Copiar los registros.
[volcado de depuración de clúster mssqlctl](#mssqlctl-cluster-debug-dump) | Volcado del registro de desencadenador.
## <a name="mssqlctl-cluster-debug-copy-logs"></a>depuración mssqlctl copia-registros de clúster
Copiar los registros de depuración desde el clúster: se requiere la configuración de kube en el sistema.
```bash
mssqlctl cluster debug copy-logs --namespace -n 
                                 [--container -c]  
                                 [--target-folder -d]  
                                 [--pod -p]  
                                 [--timeout -t]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--namespace -n`
Nombre del clúster, usado para el espacio de nombres de kubernetes.
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
## <a name="mssqlctl-cluster-debug-dump"></a>volcado de depuración de clúster mssqlctl
Desencadenar el registro de volcado de memoria y copiarla desde el contenedor: se requiere la configuración de kube en el sistema.
```bash
mssqlctl cluster debug dump --namespace -n 
                            --container -c  
                            [--target-folder -d]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--namespace -n`
Nombre del clúster, usado para el espacio de nombres de kubernetes.
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