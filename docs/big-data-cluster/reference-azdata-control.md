---
title: referencia de control azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de control de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2ce02ef0b212070b4a52944e055404137c78c98b
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304722"
---
# <a name="azdata-control"></a>control azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artículo es un artículo de referencia para **azdata**. 

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
[creación del control azdata](#azdata-control-create) | Crear plano de control.
[eliminar control azdata](#azdata-control-delete) | Eliminar plano de control.
## <a name="azdata-control-create"></a>creación del control azdata
Se necesita la configuración de Create control plano-Kube en el sistema junto con las siguientes variables de entorno [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ', ' MSSQL_SA_PASSWORD ', ' KNOX_PASSWORD '].
```bash
azdata control create [--name -n] 
                      [--config-profile -c]  
                      [--accept-eula -a]  
                      [--node-label -l]  
                      [--force -f]
```
### <a name="examples"></a>Ejemplos
Control de la implementación.
```bash
azdata control create
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--name -n`
Nombre del plano de control, que se usa para los espacios de nombres kubernetes.
#### `--config-profile -c`
Perfil de configuración de clúster que se usa para implementar el clúster: [' AKS-dev-test ', ' kubeadm-Prod ', ' minikube-dev-test ', ' kubeadm-dev-test ']
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no quiere usar este argumento, puede establecer la variable de entorno ACCEPT_EULA en “yes”. 
#### `--node-label -l`
Etiqueta de nodo, que se usa para designar los nodos en los que se va a implementar.
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
## <a name="azdata-control-delete"></a>eliminar control azdata
Elimine el plano de control: se necesita la configuración Kube en el sistema.
```bash
azdata control delete --name -n 
                      [--force -f]
```
### <a name="examples"></a>Ejemplos
Control de la implementación.
```bash
azdata control delete
```
### <a name="required-parameters"></a>Parámetros necesarios
#### `--name -n`
Nombre del plano de control, que se usa para el espacio de nombres kubernetes.
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--force -f`
Forzar eliminación de plano de control.
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
