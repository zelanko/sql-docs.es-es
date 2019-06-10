---
title: referencia de clúster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 654888bc27fec43abb8a8f511b0de7a4972e4377
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779254"
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
[punto de conexión de clúster mssqlctl](reference-mssqlctl-cluster-endpoint.md) | Comandos de punto de conexión.
[estado del clúster mssqlctl](reference-mssqlctl-cluster-status.md) | Comandos de estado.
[depuración de clúster mssqlctl](reference-mssqlctl-cluster-debug.md) | Comandos de depuración.
[grupo de almacenamiento de clúster mssqlctl](reference-mssqlctl-cluster-storage-pool.md) | Administrar grupos de almacenamiento de clúster.
## <a name="mssqlctl-cluster-create"></a>crear clúster mssqlctl
Crear un clúster grande de datos de SQL Server: configuración de kube es necesaria en el sistema junto con las siguientes variables de entorno ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'DOCKER_USERNAME', 'DOCKER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'].
```bash
mssqlctl cluster create [--config-file -c] 
                        [--accept-eula -a]  
                        [--node-label -l]  
                        [--force -f]
```
### <a name="examples"></a>Ejemplos
Experiencia de implementación de clúster - guiada recibirá indicaciones para los valores necesarios.
```bash
mssqlctl cluster create
```
Implementación del clúster con argumentos.
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json
```
Implementación del clúster con los argumentos - sin mensajes se expresará como--force se utiliza la marca.
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json --force
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-file -c`
Perfil de configuración, usado para implementar el clúster del clúster: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
#### `--accept-eula -a`
¿Acepta los términos de licencia? [yes/no]. Si no desea utilizar este argumento, puede establecer la variable de entorno ACCEPT_EULA en 'Sí'
#### `--node-label -l`
Etiqueta del nodo de clúster, que se usa para designar qué nodos se deben implementar para.
#### `--force -f`
Fuerce crear, no se pedirá al usuario todos los valores y todos los problemas se imprimirá como parte de stderr.
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
Eliminar el clúster grande de datos de SQL Server: configuración de kube es necesaria en el sistema junto con las siguientes variables de entorno ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'].
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="examples"></a>Ejemplos
Eliminación del clúster donde el nombre de usuario del controlador y la contraseña ya están configurados en el entorno del sistema.
```bash
mssqlctl cluster delete --name <cluster_name>
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
