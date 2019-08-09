---
title: Referencia de azdata bdc
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 488394cbf4b52a952ffc46ab2ec6c9a273466bd5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426045"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona referencia sobre los comandos de **bdc** de la herramienta **azdata**. Para obtener más información sobre otros comandos de **azdata**, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos

|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | Crea el clúster de macrodatos.
[azdata bdc delete](#azdata-bdc-delete) | Elimina el clúster de macrodatos.
[azdata bdc config](reference-azdata-bdc-config.md) | Comandos de configuración.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | Comandos de punto de conexión.
[azdata bdc status](reference-azdata-bdc-status.md) | Comandos de estado.
[azdata bdc debug](reference-azdata-bdc-debug.md) | Comandos de depuración.
[azdata bdc control](reference-azdata-bdc-control.md) | Comandos de control.
[azdata bdc pool](reference-azdata-bdc-pool.md) | Comandos de grupo.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | El módulo HDFS proporciona comandos para acceder a un sistema de archivos HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Los comandos de Spark permiten al usuario interactuar con el sistema de Spark mediante la creación y administración de sesiones, instrucciones y lotes.
## <a name="azdata-bdc-create"></a>azdata bdc create
Crea un clúster de macrodatos de SQL Server: se requiere kube config en el sistema junto con las siguientes variables de entorno ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'].
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>Ejemplos

Experiencia de implementación de BDC guiada: se reciben mensajes sobre los valores necesarios.

```bash
azdata bdc create
```

Implementación de BDC con argumentos.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
Implementación de BDC con nombre especificado en lugar de nombre predeterminado en el perfil.
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```

Implementación de BDC con argumentos: no se proporcionan mensajes, ya que se usa la marca --force.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```

### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre del clúster de macrodatos, se usa para espacios de nombres de kubernetes.
#### `--config-profile -c`
Perfil de configuración del clúster de macrodatos, se usa para implementar el clúster: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no quiere usar este argumento, puede establecer la variable de entorno ACCEPT_EULA en "yes". Los términos de licencia de este producto se pueden ver en https://aka.ms/azdata-eula y https://go.microsoft.com/fwlink/?LinkId=2002534.
#### `--node-label -l`
Etiqueta de nodo del clúster de macrodatos, se usa para designar los nodos en los que se va a implementar.
#### `--force -f`
Fuerza la creación, no se le pide al usuario ningún valor y todos los problemas se imprimen como parte de stderr.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="azdata-bdc-delete"></a>azdata bdc delete
Elimina el clúster de macrodatos de SQL Server: se requiere kube config en el sistema junto con las siguientes variables de entorno ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'].
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Ejemplos
Eliminación de BDC en la que el nombre de usuario y la contraseña del controlador ya están establecidos en el entorno del sistema.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre del clúster de macrodatos, se usa para el espacio de nombres de kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--force -f`
Fuerza la eliminación del clúster de macrodatos.
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre otros comandos de **azdata**, vea [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
