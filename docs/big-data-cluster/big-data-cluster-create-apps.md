---
title: Cómo implementar una aplicación
titleSuffix: SQL Server 2019 big data clusters
description: Implementar un script de Python o R como una aplicación en clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 12/11/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f37267083e0e56dd6e3c0e06c1d80ed79c0d9969
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241936"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>Cómo implementar una aplicación en clúster de macrodatos de 2019 de SQL Server (versión preliminar)

En este artículo se describe cómo implementar y administrar el script de R y Python como una aplicación dentro de un clúster de macrodatos de 2019 de SQL Server (versión preliminar).

R y Python aplicaciones se implementan y administran con el **mssqlctl pre** utilidad de línea de comandos que se incluye en CTP 2.2. En este artículo se proporciona ejemplos de cómo implementar estos scripts de R y Python, como las aplicaciones de la línea de comandos.

## <a name="prerequisites"></a>Requisitos previos

Debe tener un clúster de macrodatos de SQL Server 2019 configurado. Para obtener más información, consulte [cómo implementar SQL Server al clúster de macrodatos en Kubernetes](deployment-guidance.md). 

## <a name="installation"></a>Instalación

El **mssqlctl pre** se proporciona una utilidad de línea de comandos para obtener una vista previa de la característica de implementación de aplicación de Python y R. Use el siguiente comando para instalar la utilidad:

```cmd
pip install -r https://private-repo.microsoft.com/python/ctp-2.2/mssqlctlpre/mssqlctlpre.txt --trusted-host https://private-repo.microsoft.com
```

## <a name="capabilities"></a>Capabilities

En CTP 2.2 que puede crear, eliminar, enumerar y ejecutar una aplicación de R o Python. En la tabla siguiente se describe los comandos de implementación de aplicación que puede usar con **mssqlctl pre**.

| Comando | Descripción |
|---|---|
| `mssqlctl-pre login` | Inicie sesión en un clúster de macrodatos de SQL Server |
| `mssqlctl-pre app create` | Creación de una aplicación |
| `mssqlctl-pre app list` | Lista de las aplicaciones implementadas |
| `mssqlctl-pre app delete` | Eliminar una aplicación |
| `mssqlctl-pre app run` | Lista de aplicaciones en ejecución |

También puede obtener ayuda con la `--help` parámetro como en el ejemplo siguiente:

```bash
mssqlctl-pre app create --help
```

Las secciones siguientes describen estos comandos en más detalle.

## <a name="log-in"></a>Inicia sesión

Antes de configurar las aplicaciones de R y Python, primero inicie sesión en un clúster de macrodatos con SQL Server la `mssqlctl-pre login` comando. Especifique la dirección IP externa de la `service-proxy-lb` o `service-proxy-nodeport` servicios (por ejemplo: `https://ip-address:30777`) junto con el nombre de usuario y la contraseña para el clúster.

Puede obtener la dirección IP de la **proxy-service-lb** o **proxy-service-nodeport** servicio, ejecute este comando en una ventana cmd o bash:

```bash 
kubectl get svc service-proxy-lb -n <name of your cluster>
```

```bash
mssqlctl-pre login -e https://<ip-address-of-service-proxy-lb>:30777 -u <user-name> -p <password>
```

## <a name="create-an-app"></a>Creación de una aplicación

Para crear una aplicación, pasa los archivos de código Python o R para **mssqlctl pre** con el `app create` comando. Estos archivos residen localmente en el equipo que va a crear la aplicación.

Use la sintaxis siguiente para crear una nueva aplicación en el clúster de macrodatos:

```bash
mssqlctl-pre app create -n <app_name> -v <version_number> -r <runtime> -i <path_to_code_init> -c <path_to_code> --inputs <input_params> --outputs <output_params> 
```

El comando siguiente muestra un ejemplo del aspecto que podría tener este comando:

```py
#add.py
def add(x,y):
        result = x+y
        return result;
result=add(x,y)
```
Para probar esto, guarde las líneas de código anteriores en su directorio local como `add.py` y ejecute el siguiente comando

```bash
mssqlctl-pre app create --name add-app --version v1 --runtime Python --code ./add.py  --inputs x=int,y=int --outputs result=int 
```

Puede comprobar si la aplicación se implementa mediante el comando de lista:

```bash
mssqlctl-pre app list
```

Si no se ha completado la implementación debería ver "estado" Mostrar "Crear": 

```
[
  {
    "name": "add-app",
    "state": "Creating",
    "version": "v1"
  }
]
```

Después de la implementación sea correcta, verá el "estado" cambiar a un estado "Listo":

```
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>Publicar una aplicación

Puede enumerar las aplicaciones que se crearon correctamente con el `app list` comando.

El siguiente comando enumera todas las aplicaciones disponibles en el clúster de macrodatos:

```bash
mssqlctl-pre app list
```

Si especifica un nombre y versión, mostrará esa aplicación específica y su estado (creación o listo):

```bash
mssqlctl-pre app list --name <app_name> --version <app_version>
```

El ejemplo siguiente muestra este comando:

```bash
mssqlctl-pre app list --name add-app --version v1
```

Debería ver resultados similares al ejemplo siguiente:

```
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>Ejecutar una aplicación

Si la aplicación está en un estado "Listo", puede usarlo si lo ejecuta con los parámetros de entrada especificados. Use la siguiente sintaxis para ejecutar una aplicación:

```bash
mssqlctl-pre app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

El comando de ejemplo siguiente muestra el comando run:

```bash
mssqlctl-pre app run --name add-app --version v1 --inputs x=1,y=2
```

Si la ejecución se realizó correctamente, debería ver la salida que especificó cuando creó la aplicación. A continuación se muestra un ejemplo.

```
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="delete-an-app"></a>Eliminar una aplicación

Para eliminar una aplicación desde el clúster de macrodatos, use la sintaxis siguiente:

```bash
mssqlctl-pre app delete --name add-app --version v1
```

## <a name="next-steps"></a>Pasos siguientes

También puede consultar ejemplos adicionales en [ https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster). 

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
