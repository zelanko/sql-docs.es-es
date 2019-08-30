---
title: Referencia de azdata bdc
titleSuffix: SQL Server big data clusters
description: Artículo de referencia sobre los comandos de azdata bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 408b3c2d55d5e2515a2df979cd54b380a0d54704
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155139"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artículo es un artículo de referencia para **azdata**. 

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | Crea el clúster de macrodatos.
[azdata bdc delete](#azdata-bdc-delete) | Elimina el clúster de macrodatos.
[azdata bdc config](reference-azdata-bdc-config.md) | Comandos de configuración.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | Comandos de punto de conexión.
[azdata bdc debug](reference-azdata-bdc-debug.md) | Comandos de depuración.
[azdata bdc status](reference-azdata-bdc-status.md) | Comandos de estado de BDC.
[azdata bdc control](reference-azdata-bdc-control.md) | Comandos de control de servicio.
[SQL BDC azdata](reference-azdata-bdc-sql.md) | Comandos del servicio SQL.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Comandos del servicio HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Comandos del servicio Spark.
[puerta de enlace de BDC de azdata](reference-azdata-bdc-gateway.md) | Comandos del servicio de puerta de enlace.
[aplicación de BDC de azdata](reference-azdata-bdc-app.md) | Comandos de App Service.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | El módulo HDFS proporciona comandos para acceder a un sistema de archivos HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Los comandos de Spark permiten al usuario interactuar con el sistema de Spark mediante la creación y administración de sesiones, instrucciones y lotes.
## <a name="azdata-bdc-create"></a>azdata bdc create
Cree un clúster de macrodatos de SQL Server: la configuración Kubernetes es necesaria en el sistema junto con las siguientes variables de entorno [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ', ' MSSQL_SA_PASSWORD ', ' KNOX_PASSWORD '].
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
Perfil de configuración del clúster de Big Data, que se usa para implementar el clúster: [' AKS-dev-test ', ' kubeadm-Prod ', ' minikube-dev-test ', ' kubeadm-dev-test ']
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no quiere usar este argumento, puede establecer la variable de entorno ACCEPT_EULA en "yes". Los términos de licencia de este producto se pueden ver en https://aka.ms/azdata-eula y https://go.microsoft.com/fwlink/?LinkId=2002534.
#### `--node-label -l`
Etiqueta de nodo del clúster de macrodatos, se usa para designar los nodos en los que se va a implementar.
#### `--force -f`
Fuerza la creación, no se le pide al usuario ningún valor y todos los problemas se imprimen como parte de stderr.
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
## <a name="azdata-bdc-delete"></a>azdata bdc delete
Elimine el SQL Server clúster de macrodatos: la configuración Kubernetes es necesaria en el sistema.
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Ejemplos
Eliminación de BDC.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre del clúster de macrodatos; se usa para el espacio de nombres de Kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--force -f`
Fuerza la eliminación del clúster de macrodatos.
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
