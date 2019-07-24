---
title: referencia de BDC de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos BDC de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 488394cbf4b52a952ffc46ab2ec6c9a273466bd5
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426045"
---
# <a name="azdata-bdc"></a>BDC de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para los comandos de **BDC** en la herramienta **azdata** . Para obtener más información sobre otros comandos de **azdata** , consulte [referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos:

|     |     |
| --- | --- |
[creación de BDC de azdata](#azdata-bdc-create) | Cree un clúster de Big Data.
[eliminación de BDC de azdata](#azdata-bdc-delete) | Elimine el clúster de Big Data.
[configuración de azdata BDC](reference-azdata-bdc-config.md) | Comandos de configuración.
[extremo de BDC de azdata](reference-azdata-bdc-endpoint.md) | Comandos del extremo.
[Estado de BDC de azdata](reference-azdata-bdc-status.md) | Comandos de estado.
[depuración de BDC de azdata](reference-azdata-bdc-debug.md) | Comandos de depuración.
[control de BDC de azdata](reference-azdata-bdc-control.md) | Comandos de control.
[Grupo de BDC de azdata](reference-azdata-bdc-pool.md) | Comandos de grupo.
[azdata BDC HDFS](reference-azdata-bdc-hdfs.md) | El módulo HDFS proporciona comandos para tener acceso a un sistema de archivos HDFS.
[azdata BDC Spark](reference-azdata-bdc-spark.md) | Los comandos de Spark permiten al usuario interactuar con el sistema de Spark mediante la creación y administración de sesiones, instrucciones y lotes.
## <a name="azdata-bdc-create"></a>creación de BDC de azdata
Cree un clúster de macrodatos SQL Server-Kube config es necesario en el sistema junto con las siguientes variables de entorno [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ', ' MSSQL_SA_PASSWORD ', ' KNOX_PASSWORD '].
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>Ejemplos

Experiencia de implementación de BDC guiada: recibirá mensajes sobre los valores necesarios.

```bash
azdata bdc create
```

Implementación de BDC con argumentos.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
Implementación de BDC con el nombre especificado en lugar del nombre predeterminado en el perfil.
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```

Implementación de BDC con argumentos: no se proporcionarán mensajes, ya que se usa la marca--Force.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```

### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre del clúster de Big Data, que se usa para los espacios de nombres kubernetes.
#### `--config-profile -c`
Perfil de configuración del clúster de Big Data, que se usa para implementar el clúster: [' AKS-dev-test ', ' kubeadm-dev-test ', ' minikube-dev-test ']
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no desea utilizar este argumento, puede establecer la variable de entorno ACCEPT_EULA en "Yes". Los términos de licencia de este producto se pueden ver https://aka.ms/azdata-eula en https://go.microsoft.com/fwlink/?LinkId=2002534 y.
#### `--node-label -l`
Etiqueta de nodo del clúster de Big Data, que se usa para designar los nodos en los que se va a implementar.
#### `--force -f`
Forzar la creación, no se le pedirá al usuario ningún valor y todos los problemas se imprimirán como parte de stderr.
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
## <a name="azdata-bdc-delete"></a>eliminación de BDC de azdata
Elimine el clúster de macrodatos de SQL Server: Kube config es necesario en el sistema junto con las siguientes variables de entorno [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD '].
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
Nombre del clúster de Big Data, que se usa para el espacio de nombres kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--force -f`
Fuerce la eliminación del clúster de Big Data.
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
