---
title: Implementar aplicaciones con mssqlctl
titleSuffix: SQL Server big data clusters
description: Implementar un script de Python o R como una aplicación en clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 6c8f4aea32ba409a00dd1d8f3fb5487e2a4a9d90
ms.sourcegitcommit: 32dce314bb66c03043a93ccf6e972af455349377
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2019
ms.locfileid: "66743975"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>Cómo implementar una aplicación en clúster de macrodatos de SQL Server (versión preliminar)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo implementar y administrar el script de R y Python como una aplicación dentro de un clúster de macrodatos de 2019 de SQL Server (versión preliminar).

## <a name="whats-new-and-improved"></a>¿Qué es nuevo y mejorado

- Una única utilidad de línea de comandos para administrar el clúster y la aplicación.
- Implementación de aplicaciones simplificada al tiempo que proporciona un control granular a través de los archivos de especificación.
- Admite el hospedaje de tipos de aplicación adicionales: SSIS y MLeap (novedad en CTP 2.3)
- [Extensión de VS Code](app-deployment-extension.md) para administrar la implementación de aplicaciones

Las aplicaciones se implementan y administran mediante `mssqlctl` utilidad de línea de comandos. En este artículo se proporciona ejemplos de cómo implementar aplicaciones desde la línea de comandos. Para obtener información sobre cómo usar esto en Visual Studio Code consulte [extensión de VS Code](app-deployment-extension.md).

Se admiten los siguientes tipos de aplicaciones:
- Aplicaciones de R y Python (funciones, modelos y aplicaciones)
- MLeap Servers
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos de SQL Server 2019](deployment-guidance.md)
- [mssqlctl command-line utility](deploy-install-mssqlctl.md)

## <a name="capabilities"></a>Capabilities

En SQL Server 2019 CTP 3.0 (versión preliminar) puede crear, eliminar, describir, inicializar, lista ejecutar y actualizar la aplicación. En la tabla siguiente se describe los comandos de implementación de aplicación que puede usar con **mssqlctl**.

|Comando |Descripción |
|:---|:---|
|`mssqlctl login` | Inicie sesión en un clúster de macrodatos de SQL Server |
|`mssqlctl app create` | Crear la aplicación. |
|`mssqlctl app delete` | Eliminar la aplicación. |
|`mssqlctl app describe` | Describir la aplicación. |
|`mssqlctl app init` | Nueva aplicación KickStart esqueleto. |
|`mssqlctl app list` | Lista de aplicaciones. |
|`mssqlctl app run` | Ejecutar la aplicación. |
|`mssqlctl app update`| Actualizar la aplicación. |

También puede obtener ayuda con la `--help` parámetro como en el ejemplo siguiente:

```bash
mssqlctl app create --help
```

Las secciones siguientes describen estos comandos en más detalle.

## <a name="sign-in"></a>Iniciar sesión

Antes de implementar o interactuar con las aplicaciones, primero inicie sesión en un clúster de macrodatos con SQL Server la `mssqlctl login` comando. Especifique la dirección IP externa de la `controller-svc-external` servicio (por ejemplo: `https://ip-address:30080`) junto con el nombre de usuario y la contraseña para el clúster.

```bash
mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

Si usa AKS, deberá ejecutar el comando siguiente para obtener la dirección IP de la `mgmtproxy-svc-external` servicio, ejecute este comando en una ventana cmd o bash:


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm o Minikube

Si usas Kubeadm o Minikube, ejecute el siguiente comando para obtener la dirección IP para el inicio de sesión en el clúster

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Creación de una aplicación

Para crear una aplicación, utilice `mssqlctl` con el `app create` comando. Estos archivos residen localmente en el equipo que va a crear la aplicación.

Use la sintaxis siguiente para crear una nueva aplicación en clúster de macrodatos:

```bash
mssqlctl app create --spec <directory containing spec file>
```

El comando siguiente muestra un ejemplo del aspecto que podría tener este comando:

```bash
mssqlctl app create --spec ./addpy
```

Esto supone que tiene la aplicación que se almacenan en el `addpy` carpeta. Esta carpeta también debe contener un archivo de especificación de la aplicación, llamada llamado `spec.yaml`. Consulte [la página de implementación de aplicaciones](concept-application-deployment.md) para obtener más información sobre la `spec.yaml` archivo.

Para implementar esta aplicación de ejemplo de aplicación, cree los siguientes archivos en un directorio llamado `addpy`:

- `add.py` Copie el siguiente código de Python en este archivo:
   ```py
   #add.py
   def add(x,y):
        result = x+y
        return result
    result=add(x,y)
   ```
- `spec.yaml` Copie el código siguiente en este archivo:
   ```yaml
   #spec.yaml
   name: add-app #name of your python script
   version: v1  #version of the app
   runtime: Python #the language this app uses (R or Python)
   src: ./add.py #full path to the location of the app
   entrypoint: add #the function that will be called upon execution
   replicas: 1  #number of replicas needed
   poolsize: 1  #the pool size that you need your app to scale
   inputs:  #input parameters that the app expects and the type
     x: int
     y: int
   output: #output parameter the app expects and the type
     result: int
   ```

A continuación, ejecute el siguiente comando:

```bash
mssqlctl app create --spec ./addpy
```

Puede comprobar si la aplicación se implementa mediante el comando de lista:

```bash
mssqlctl app list
```

Si no se ha completado la implementación debería ver el `state` mostrar `WaitingforCreate` como en el ejemplo siguiente:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Después de la implementación es correcta, debería ver el `state` cambie a `Ready` estado:

```json
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
mssqlctl app list
```

Si especifica un nombre y versión, se enumeran esa aplicación específica y su estado (creación o listo):

```bash
mssqlctl app list --name <app_name> --version <app_version>
```

El ejemplo siguiente muestra este comando:

```bash
mssqlctl app list --name add-app --version v1
```

Debería ver resultados similares al ejemplo siguiente:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>Ejecutar una aplicación

Si la aplicación está en un `Ready` de estado, puede usarlo si lo ejecuta con los parámetros de entrada especificados. Use la siguiente sintaxis para ejecutar una aplicación:

```bash
mssqlctl app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

El comando de ejemplo siguiente muestra el comando run:

```bash
mssqlctl app run --name add-app --version v1 --inputs x=1,y=2
```

Si la ejecución se realizó correctamente, debería ver la salida que especificó cuando creó la aplicación. A continuación se muestra un ejemplo.

```json
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

## <a name="create-an-app-skeleton"></a>Creación de un esqueleto de la aplicación

El comando init proporciona una plantilla scaffold con los artefactos relevantes que es necesaria para implementar una aplicación. El ejemplo siguiente crea hello puede hacerlo ejecutando el comando siguiente.

```bash
mssqlctl app init --name hello --version v1 --template python
```

Esto creará una carpeta denominada hello.  También puede `cd` en el directorio e inspeccionar los archivos generados en la carpeta. spec.yaml define la aplicación, como nombre, versión y el código fuente. Puede editar la especificación para cambiar el nombre, versión, entradas y salidas.

Esta es una salida de ejemplo del comando init que ve en la carpeta

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>Describe una aplicación

El comando descripción proporciona información detallada acerca de la aplicación, incluido el punto final en el clúster. Esto se usa normalmente por un desarrollador de aplicaciones para compilar una aplicación mediante el cliente de swagger y usar el servicio Web para interactuar con la aplicación de forma RESTful. Consulte [consumir las aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md) para obtener más información.

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30777/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30777/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>Eliminar una aplicación

Para eliminar una aplicación desde el clúster de macrodatos, use la sintaxis siguiente:

```bash
mssqlctl app delete --name add-app --version v1
```

## <a name="next-steps"></a>Pasos siguientes

Explore cómo integrar las aplicaciones implementadas en SQL Server, clústeres de macrodatos en sus propias aplicaciones en [consumir las aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md) para obtener más información. También puede consultar ejemplos adicionales en [ejemplos de implementación de aplicaciones](https://aka.ms/sql-app-deploy).

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
