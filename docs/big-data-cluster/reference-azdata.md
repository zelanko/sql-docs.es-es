---
title: referencia de azdata
titleSuffix: SQL Server big data clusters
description: Artículo de referencia de los comandos de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4ef2ba9c68f3586e159c326863ef76ba231f01b9
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531650"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

En el artículo siguiente se proporciona una referencia de los comandos de `sql` de la herramienta `azdata`. Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
|[azdata bdc](reference-azdata-bdc.md) | Para seleccionar, administrar y poner en funcionamiento clústeres de macrodatos de SQL Server. |
|[azdata app](reference-azdata-app.md) | Para crear, eliminar, ejecutar y administrar aplicaciones. |
[azdata login](#azdata-login) | Inicie sesión en el punto de conexión del controlador del clúster y establezca su espacio de nombres como su contexto activo. Para usar una contraseña en el inicio de sesión, debe establecer la variable de entorno AZDATA_PASSWORD.
[azdata logout](#azdata-logout) | Para cerrar la sesión del clúster.
|[azdata context](reference-azdata-context.md) | Comandos de administración de contexto. |
|[azdata control](reference-azdata-control.md) | Cree, elimine y administre planos de control. |
|[azdata sql](reference-azdata-sql.md) | La CLI de SQL DB permite al usuario interactuar con SQL Server mediante T-SQL. |
|[azdata notebook](reference-azdata-notebook.md) | Comandos para ver, ejecutar y administrar cuadernos desde un terminal. |
## <a name="azdata-login"></a>azdata login
Una vez implementado el clúster, mostrará el punto de conexión del controlador durante la implementación que se debe usar para iniciar sesión.  Si no conoce el punto de conexión del controlador, puede iniciar sesión teniendo el archivo kubeconfig del clúster en el sistema en la ubicación predeterminada, <user home>/.kube/config, o usar la variable de entorno KUBECONFIG, esto es, export KUBECONFIG=path/to/.kube/config.  Al iniciar sesión, el espacio de nombres de este clúster se establecerá en el contexto activo.
```bash
azdata login [--auth] 
             [--endpoint -e]  
             [--accept-eula -a]  
             [--namespace -n]  
             [--username -u]  
             [--principal -p]
```
### <a name="examples"></a>Ejemplos
Iniciar sesión mediante la autenticación básica.
```bash
azdata login --auth basic --username johndoe --endpoint https://<ip or domain name>:30080            
```
Iniciar sesión mediante Active Directory.
```bash
azdata login --auth ad --endpoint https://<ip or domain name>:30080                
```
Iniciar sesión mediante Active Directory con una entidad de seguridad explícita.
```bash
azdata login --auth ad --principal johndoe@COSTOSO.COM --endpoint https://<ip or domain name>:30080
```
Iniciar sesión de forma interactiva. Siempre se le pedirá el nombre del clúster si no lo especifica como argumento. Si tiene las variables de entorno AZDATA_USERNAME, AZDATA_PASSWORD y ACCEPT_EULA establecidas en el sistema, no se le pedirá que lo haga. Si tiene el archivo kubeconfig en el sistema o usa la variable de entorno KUBECONFIG para especificar la ruta de acceso a la configuración, la experiencia interactiva intentará usar la configuración en primer lugar y, si falla, le preguntará.
```bash
azdata login
```
Inicie sesión (de forma no interactiva). Inicie sesión con el nombre del clúster, el nombre de usuario del controlador, el punto de conexión del controlador y el conjunto de aceptación del Contrato de licencia para el usuario final como argumentos. La variable de entorno AZDATA_PASSWORD debe estar establecida.  Si no quiere especificar el punto de conexión del controlador, coloque el archivo kubeconfig en el equipo, en la ubicación predeterminada, <user home>/.kube/config, o use la variable de entorno KUBECONFIG, esto es, export KUBECONFIG=path/to/.kube/config.
```bash
azdata login --namespace ClusterName --username johndoe@contoso.com  --endpoint https://<ip or domain name>:30080 --accept-eula yes
```
Inicie sesión con kubeconfig en la máquina y con las variables de entorno AZDATA_USERNAME, AZDATA_PASSWORD y ACCEPT_EULA. establecidas.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>Parámetros opcionales
#### `--auth`
Estrategia de autenticación. Autenticación básica o de Active Directory. La autenticación básica es la predeterminada.
#### `--endpoint -e`
Punto de conexión del controlador de clúster "https://host:port". Si no quiere usar este argumento, puede usar el archivo kubeconfig en el equipo; asegúrese de que está en la ubicación predeterminada, <user home>de/.Kube/config, o use la variable de entorno KUBECONFIG.
#### `--accept-eula -a`
¿Acepta los términos de licencia? [sí/no]. Si no quiere usar este argumento, puede establecer la variable de entorno ACCEPT_EULA en “yes”. Los términos de licencia de este producto se pueden ver en https://aka.ms/eula-azdata-en.
#### `--namespace -n`
Espacio de nombres del plano de control del clúster.
#### `--username -u`
Usuario de la cuenta. Si no quiere usar este argumento, puede establecer la variable de entorno AZDATA_USERNAME.
#### `--principal -p`
Dominio Kerberos. En la mayoría de casos, el dominio Kerberos es el nombre de dominio, en letras mayúsculas.
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

Para obtener más información sobre otros comandos de `azdata`, vea [Referencia de azdata](reference-azdata.md). Para obtener más información sobre cómo instalar la herramienta `azdata`, vea [Instalación de azdata para administrar clústeres de macrodatos de SQL Server 2019](deploy-install-azdata.md).
