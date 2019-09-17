---
title: referencia de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de los comandos de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 66b5d00e8f920aca9435fca7f05037184f75f130
ms.sourcegitcommit: 49f3d12c0a46d98b82513697a77a461340f345e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70391948"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
|[azdata notebook](reference-azdata-notebook.md) | Comandos para ver, ejecutar y administrar cuadernos desde un terminal. |
|[azdata sql](reference-azdata-sql.md) | La CLI de SQL DB permite al usuario interactuar con SQL Server mediante T-SQL. |
|[azdata app](reference-azdata-app.md) | Para crear, eliminar, ejecutar y administrar aplicaciones. |
|[azdata bdc](reference-azdata-bdc.md) | Para seleccionar, administrar y poner en funcionamiento clústeres de macrodatos de SQL Server. |
|[control azdata](reference-azdata-control.md) | Crear, eliminar y administrar los planos de control. |
[azdata login](#azdata-login) | Para iniciar sesión en el punto de conexión del controlador del clúster.
[azdata logout](#azdata-logout) | Para cerrar la sesión del clúster.
## <a name="azdata-login"></a>azdata login
Una vez implementado el clúster, mostrará el punto de conexión del controlador durante la implementación que se debe usar para iniciar sesión.  Si no conoce el punto de conexión del controlador, puede iniciar sesión teniendo el archivo kubeconfig del clúster en el sistema en la ubicación predeterminada, <user home>/.kube/config, o usar la variable de entorno KUBECONFIG, esto es, export KUBECONFIG=path/to/.kube/config.
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>Ejemplos
Iniciar sesión de forma interactiva. Siempre se le pedirá el nombre del clúster si no lo especifica como argumento. Si tiene las variables de entorno CONTROLLER_USERNAME, CONTROLLER_PASSWORD y ACCEPT_EULA establecidas en el sistema, no se le pedirá que lo haga. Si tiene el archivo kubeconfig en el sistema o usa la variable de entorno KUBECONFIG para especificar la ruta de acceso a la configuración, la experiencia interactiva intentará usar la configuración en primer lugar y, si falla, le preguntará.
```bash
azdata login
```
Inicie sesión (de forma no interactiva). Inicie sesión con el nombre del clúster, el nombre de usuario del controlador, el punto de conexión del controlador y el conjunto de aceptación del Contrato de licencia para el usuario final como argumentos. La variable de entorno CONTROLLER_PASSWORD debe estar establecida.  Si no quiere especificar el punto de conexión del controlador, coloque el archivo kubeconfig en el equipo, en la ubicación predeterminada, <user home>/.kube/config, o use la variable de entorno KUBECONFIG, esto es, export KUBECONFIG=path/to/.kube/config.
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Inicie sesión con kubeconfig en el equipo y con las variables de entorno CONTROLLER_USERNAME, CONTROLLER_PASSWORD y ACCEPT_EULA establecidas.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--cluster-name -n`
Nombre del clúster.
#### `--controller-username -u`
Usuario de la cuenta. Si no quiere usar este argumento, puede establecer la variable de entorno CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Punto de conexión del controlador de clúster "https://host:port". Si no quiere usar este argumento, puede usar el archivo kubeconfig en el equipo; asegúrese de que está en la ubicación predeterminada, <user home>de/.Kube/config, o use la variable de entorno KUBECONFIG.
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no quiere usar este argumento, puede establecer la variable de entorno ACCEPT_EULA en “yes”. 
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
## <a name="azdata-logout"></a>azdata logout
Para cerrar la sesión del clúster.
```bash
azdata logout 
```
### <a name="examples"></a>Ejemplos
Cierre la sesión de este clúster.
```bash
azdata logout
```
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumente el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestre este mensaje de ayuda y salga.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información y ejemplos, vea [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumente el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

- Para más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
