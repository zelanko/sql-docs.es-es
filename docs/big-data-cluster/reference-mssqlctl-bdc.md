---
title: referencia de bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de bdc mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2c16a8121f2a0ec90fe8141c78e690bf212b5f27
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394237"
---
# <a name="mssqlctl-bdc"></a>mssqlctl bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **bdc** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[mssqlctl bdc create](#mssqlctl-bdc-create) | Crear el clúster de Macrodatos.
[mssqlctl bdc delete](#mssqlctl-bdc-delete) | Eliminar clúster de Macrodatos.
[configuración de bdc mssqlctl](reference-mssqlctl-bdc-config.md) | Comandos de configuración.
[punto de conexión de bdc mssqlctl](reference-mssqlctl-bdc-endpoint.md) | Comandos de punto de conexión.
[estado de bdc mssqlctl](reference-mssqlctl-bdc-status.md) | Comandos de estado.
[mssqlctl bdc debug](reference-mssqlctl-bdc-debug.md) | Comandos de depuración.
[mssqlctl bdc storage-pool](reference-mssqlctl-bdc-storage-pool.md) | Comandos del grupo de almacenamiento.
[mssqlctl bdc control](reference-mssqlctl-bdc-control.md) | Comandos de control.
[grupo de bdc mssqlctl](reference-mssqlctl-bdc-pool.md) | Comandos del grupo.
## <a name="mssqlctl-bdc-create"></a>crear mssqlctl bdc
Crear un clúster grande de datos de SQL Server: configuración de kube es necesaria en el sistema junto con las siguientes variables de entorno ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'DOCKER_USERNAME', 'DOCKER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'].
```bash
mssqlctl bdc create [--config-profile -c] 
                    [--accept-eula -a]  
                    [--node-label -l]  
                    [--force -f]
```
### <a name="examples"></a>Ejemplos
Experiencia guiada de implementación de BDC - recibirá indicaciones para los valores necesarios.
```bash
mssqlctl bdc create
```
Implementación del BDC con argumentos.
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test
```
Implementación del BDC con argumentos - no se le concederán mensajes como--force se utiliza la marca.
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--config-profile -c`
Perfil de configuración BDC, usado para implementar el clúster: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--accept-eula -a`
¿Acepta los términos de licencia? [yes/no]. Si no desea utilizar este argumento, puede establecer la variable de entorno ACCEPT_EULA en 'Sí'
#### `--node-label -l`
Etiqueta del nodo de BDC, que se usa para designar qué nodos se deben implementar para.
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
## <a name="mssqlctl-bdc-delete"></a>eliminación de bdc mssqlctl
Eliminar el clúster grande de datos de SQL Server: configuración de kube es necesaria en el sistema junto con las siguientes variables de entorno ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'].
```bash
mssqlctl bdc delete --name -n 
                    [--force -f]
```
### <a name="examples"></a>Ejemplos
Eliminación de BDC donde el nombre de usuario del controlador y la contraseña ya están configurados en el entorno del sistema.
```bash
mssqlctl bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre BDC, usado para el espacio de nombres de kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--force -f`
Fuerce la eliminación BDC.
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
