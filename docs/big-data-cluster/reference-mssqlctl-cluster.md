---
title: referencia de clúster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c69aeced2378e018376172e1fb6370d56706ecb7
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473325"
---
# <a name="mssqlctl-cluster"></a>Clúster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **clúster** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[mssqlctl cluster create](#mssqlctl-cluster-create) | Crear el clúster.
[mssqlctl cluster delete](#mssqlctl-cluster-delete) | Eliminar el clúster.
[configuración del clúster mssqlctl](reference-mssqlctl-cluster-config.md) | Comandos de configuración del clúster.
[depuración de clúster mssqlctl](reference-mssqlctl-cluster-debug.md) | Comandos de depuración.
## <a name="mssqlctl-cluster-create"></a>crear clúster mssqlctl
Crear un clúster de Macrodatos SQL Server.
```bash
mssqlctl cluster create [--config-file -f] 
                        [--accept-eula -e]  
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-file -f`
Perfil de configuración, usado para implementar el clúster del clúster: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
#### `--accept-eula -e`
¿Acepta los términos de licencia? [yes/no].
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
## <a name="mssqlctl-cluster-delete"></a>eliminación de clúster mssqlctl
Elimine el clúster de Macrodatos SQL Server.
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre del clúster, usado para el espacio de nombres de kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--force -f`
Clúster de eliminación de fuerza.
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
