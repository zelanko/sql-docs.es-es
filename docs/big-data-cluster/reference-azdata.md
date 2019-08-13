---
title: referencia de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de los comandos de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 24a72683c423661a2981e5a16941bcbc180ac6d1
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894003"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia de la herramienta **azdata** para [clústeres de macrodatos de SQL Server 2019 (versión preliminar)](big-data-cluster-overview.md). Para más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
|[azdata app](reference-azdata-app.md) | Para crear, eliminar, ejecutar y administrar aplicaciones. |
|[azdata bdc](reference-azdata-bdc.md) | Para seleccionar, administrar y poner en funcionamiento clústeres de macrodatos de SQL Server. |
|[azdata login](#azdata-login) | Para iniciar sesión en el punto de conexión del controlador del clúster.
|[azdata logout](#azdata-logout) | Para cerrar la sesión del clúster.

## <a name="azdata-login"></a>azdata login
Una vez implementado el clúster, se mostrará el punto de conexión del controlador durante la implementación, que debe usar para iniciar sesión.  Si no conoce el punto de conexión del controlador, puede iniciar sesión con la configuración de Kube del clúster en el sistema en la ubicación predeterminada de <user home>/.Kube/config o usar KUBECONFIG env var, es decir, Export KUBECONFIG = path/to/. Kube/config.
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
Inicie sesión (de forma no interactiva). Inicie sesión con el nombre del clúster, el nombre de usuario del controlador, el punto de conexión del controlador y el conjunto de aceptación del Contrato de licencia para el usuario final como argumentos. La variable de entorno CONTROLLER_PASSWORD debe estar establecida.  Si no desea especificar el punto de conexión del controlador, tenga la configuración Kube en el equipo en la ubicación predeterminada de <user home>/.Kube/config o use KUBECONFIG env var, es decir, Export KUBECONFIG = path/to/. Kube/config.
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
Punto de conexión del controlador de clúster "https://host:port". Si no quiere usar este argumento, puede usar el archivo kubeconfig en el equipo; Asegúrese de que la configuración se encuentra en la ubicación <user home>predeterminada de/.Kube/config o use el valor de KUBECONFIG env var.
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no quiere usar este argumento, puede establecer la variable de entorno ACCEPT_EULA en "yes". 
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Sirve para aumentar el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Sirve para mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información, [http://jmespath.org/](http://jmespath.org/]) vea para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
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
Sirve para aumentar el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Sirve para mostrar este mensaje de ayuda y salir.
#### `--output -o`
Formato de salida.  Valores permitidos: json, jsonc, table y tsv.  Valor predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Para obtener más información, [http://jmespath.org/](http://jmespath.org/]) vea para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo instalar la herramienta **azdata**, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
