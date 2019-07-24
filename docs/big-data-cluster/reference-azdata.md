---
title: referencia de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8136c85f8c32e08423f3d199a021d4f60353b39
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425995"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el siguiente artículo se proporciona una referencia para la herramienta **azdata** para clústeres de macrodatos de [SQL Server 2019 (versión preliminar)](big-data-cluster-overview.md). Para obtener más información sobre cómo instalar la herramienta **azdata** , consulte [instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
|[aplicación azdata](reference-azdata-app.md) | Crear, eliminar, ejecutar y administrar aplicaciones. |
|[BDC de azdata](reference-azdata-bdc.md) | Seleccionar, administrar y operar SQL Server clústeres de macrodatos. |
|[cuaderno de azdata Notebook](reference-azdata-notebook.md) | Comandos para ver, ejecutar y administrar cuadernos desde un terminal. |
[Inicio de sesión azdata](#azdata-login) | Inicie sesión en el punto de conexión del controlador del clúster.
[cierre de sesión de azdata](#azdata-logout) | Cierre la sesión del clúster.
|[SQL azdata](reference-azdata-sql.md) | La CLI de SQL DB permite al usuario interactuar con SQL Server a través de T-SQL. |
## <a name="azdata-login"></a>Inicio de sesión azdata
Una vez implementado el clúster, se mostrará el punto de conexión del controlador durante la implementación, que debe usar para iniciar sesión.  Si no conoce el punto de conexión del controlador, puede iniciar sesión con la configuración de Kube del clúster en el sistema en la ubicación predeterminada <user home>de/.Kube/config o usar la opción KUBECONFIG env var, es decir, Export KUBECONFIG = path/to/. Kube/config.
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>Ejemplos
Iniciar sesión de forma interactiva. Siempre se solicitará el nombre del clúster si no se especifica como argumento. Si tiene las variables CONTROLLER_USERNAME, CONTROLLER_PASSWORD y ACCEPT_EULA env establecidas en el sistema, no se le pedirá que lo haga. Si tiene la configuración de Kube en el sistema o usa la variable KUBECONFIG env para especificar la ruta de acceso a la configuración, la experiencia interactiva intentará en primer lugar usar la configuración y, a continuación, le preguntará si se produce un error en la configuración.
```bash
azdata login
```
Iniciar sesión (no interactivamente). Inicie sesión con el nombre de clúster, el nombre de usuario del controlador, el punto de conexión del controlador y el conjunto de aceptación del CLUF como argumentos. Debe establecerse la variable de entorno CONTROLLER_PASSWORD.  Si no desea especificar el punto de conexión del controlador, tenga la configuración de Kube en el equipo en la ubicación predeterminada de <user home>/.Kube/config o use KUBECONFIG env var, es decir, Export KUBECONFIG = path/to/. Kube/config.
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Inicie sesión con la configuración de Kube en el equipo y env var set para CONTROLLER_USERNAME, CONTROLLER_PASSWORD y ACCEPT_EULA.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--cluster-name -n`
Nombre del clúster.
#### `--controller-username -u`
Usuario de la cuenta. Si no desea utilizar este argumento, puede establecer la variable de entorno CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Punto de conexión del https://host:port controlador de clúster "". Si no desea usar este argumento, puede usar la configuración de Kube en su equipo. Asegúrese de que la configuración se encuentra en la ubicación predeterminada <user home>de/.Kube/config o use el valor de KUBECONFIG env var.
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no desea utilizar este argumento, puede establecer la variable de entorno ACCEPT_EULA en "Yes". Los términos de licencia de este producto se pueden ver https://aka.ms/azdata-eula en.
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
## <a name="azdata-logout"></a>cierre de sesión de azdata
Cierre la sesión del clúster.
```bash
azdata logout 
```
### <a name="examples"></a>Ejemplos
Cierre la sesión de este usuario.
```bash
azdata logout
```
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

Para obtener más información sobre cómo instalar la herramienta **azdata** , consulte [instalación de azdata para administrar clústeres de macrodatos SQL Server 2019](deploy-install-azdata.md).
