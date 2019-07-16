---
title: Referencia de mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5567b46376acc5aee6c42cdae19eef133c7af506
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957896"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **mssqlctl** herramienta para [clústeres de macrodatos de 2019 de SQL Server (versión preliminar)](big-data-cluster-overview.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).

## <a name="commands"></a>Comandos:
|     |     |
| --- | --- |
|[aplicación mssqlctl](reference-mssqlctl-app.md) | Crear, eliminar, ejecutar y administrar aplicaciones. |
|[mssqlctl bdc](reference-mssqlctl-bdc.md) | Seleccione, administrar y operar clústeres grandes de datos de SQL Server. |
|[mssqlctl hdfs](reference-mssqlctl-hdfs.md) | El módulo HDFS proporciona el sistema de archivos de comandos para tener acceso a un sistema HDFS. |
[inicio de sesión mssqlctl](#mssqlctl-login) | Inicie sesión en el punto de conexión de controlador del clúster.
[Cierre de sesión mssqlctl](#mssqlctl-logout) | Cerrar la sesión de clúster.
|[mssqlctl sql](reference-mssqlctl-sql.md) | La CLI de la base de datos de SQL permite al usuario interactuar con SQL Server a través de Transact-SQL. |
## <a name="mssqlctl-login"></a>inicio de sesión mssqlctl
Cuando se implementa el clúster, se mostrará el punto de conexión del controlador durante la implementación, que se debe utilizar al inicio de sesión.  Si no conoce el punto de conexión del controlador, es posible que el inicio de sesión al tener la configuración de kube de su clúster en su sistema en la ubicación predeterminada de <user home>/.kube/config o utilizar el var env KUBECONFIG, es decir, exportar KUBECONFIG=path/to/.kube/config.
```bash
mssqlctl login [--cluster-name -n] 
               [--controller-username -u]  
               [--controller-endpoint -e]  
               [--accept-eula -a]
```
### <a name="examples"></a>Ejemplos
Sesión de forma interactiva. Nombre del clúster se siempre se le solicitará si no se especifica como un argumento. Si tiene la CONTROLLER_USERNAME CONTROLLER_PASSWORD y ACCEPT_EULA env las variables establecidas en el sistema, estos no solicitará. Si tiene la configuración de kube en el sistema o usa el var env KUBECONFIG para especificar la ruta de acceso a la configuración, la experiencia interactiva intentará en primer lugar utilice la configuración y, a continuación, le pedirá que si se produce un error en la configuración.
```bash
mssqlctl login
```
Inicie sesión (de forma no interactiva). Inicie sesión con el nombre del clúster, nombre de usuario del controlador, el punto de conexión de controlador y la aceptación del CLUF establecido como argumentos. La variable de entorno se debe establecer CONTROLLER_PASSWORD.  Si no desea especificar el punto de conexión del controlador, tiene la configuración de kube en el equipo en la ubicación predeterminada de <user home>/.kube/config o utilizar el var env KUBECONFIG, es decir, exportar KUBECONFIG=path/to/.kube/config.
```bash
mssqlctl login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
Inicie sesión con la configuración de kube en equipo y var env establece para CONTROLLER_USERNAME, CONTROLLER_PASSWORD y ACCEPT_EULA.
```bash
mssqlctl login -n ClusterName
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--cluster-name -n`
Nombre del clúster.
#### `--controller-username -u`
Usuario de la cuenta. Si no desea utilizar este argumento, se puede establecer la variable de entorno CONTROLLER_USERNAME.
#### `--controller-endpoint -e`
Punto de conexión del controlador de clúster "https://host:port". Si no desea utilizar este argumento, puede usar la configuración de kube en su equipo. Asegúrese de que la configuración se encuentra en la ubicación predeterminada de <user home>/.kube/config o use el env KUBECONFIG var.
#### `--accept-eula -a`
¿Acepta los términos de licencia? [Sí/no]. Si no desea utilizar este argumento, puede establecer la variable de entorno ACCEPT_EULA en 'Sí'
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.
## <a name="mssqlctl-logout"></a>Cierre de sesión mssqlctl
Cerrar la sesión de clúster.
```bash
mssqlctl logout 
```
### <a name="examples"></a>Ejemplos
Cierra la sesión este usuario.
```bash
mssqlctl logout
```
### <a name="global-arguments"></a>Argumentos globales
#### `--debug`
Aumenta el nivel de detalle de registro para mostrar todos los registros de depuración.
#### `--help -h`
Muestra este mensaje de ayuda y sale.
#### `--output -o`
Formato de salida.  Los valores permitidos: json, jsonc, table y tsv.  Predeterminado: json.
#### `--query -q`
Cadena de consulta de JMESPath. Consulte [ http://jmespath.org/ ](http://jmespath.org/]) para obtener más información y ejemplos.
#### `--verbose`
Aumenta el nivel de detalle de registro. Use --debug para obtener registros de depuración completos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).