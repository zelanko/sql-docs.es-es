---
title: Implementación de aplicaciones mediante azdata
titleSuffix: SQL Server big data clusters
description: Implemente un script de Python o R como una aplicación en SQL Server clúster de macrodatos de 2019 (versión preliminar).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 06b76e7eb8eec8db1993ca558a1f57355457c4ad
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419487"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>Implementación de una aplicación en SQL Server clúster de macrodatos (versión preliminar)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo implementar y administrar scripts de R y Python como una aplicación dentro de un clúster de macrodatos SQL Server 2019 (versión preliminar).

## <a name="whats-new-and-improved"></a>Novedades y mejoras

- Una única utilidad de línea de comandos para administrar el clúster y la aplicación.
- Implementación simplificada de aplicaciones al mismo tiempo que proporciona un control granular a través de los archivos de especificación
- Compatibilidad con el hospedaje de tipos de aplicación adicionales: SSIS y MLeap (novedad en CTP 2,3)
- [Extensión vs Code](app-deployment-extension.md) para administrar la implementación de aplicaciones

Las aplicaciones se implementan y `azdata` administran mediante la utilidad de línea de comandos. En este artículo se proporcionan ejemplos de cómo implementar aplicaciones desde la línea de comandos. Para obtener información sobre cómo usar esto en Visual Studio Code consulte [extensión de vs Code](app-deployment-extension.md).

Se admiten los siguientes tipos de aplicaciones:
- Aplicaciones de R y Python (funciones, modelos y aplicaciones)
- Servicio de MLeap
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos de SQL Server 2019](deployment-guidance.md)
- [utilidad de línea de comandos azdata](deploy-install-azdata.md)

## <a name="capabilities"></a>Capabilities

En SQL Server 2019 (versión preliminar), puede crear, eliminar, describir, inicializar, enumerar y actualizar la aplicación. En la tabla siguiente se describen los comandos de implementación de aplicaciones que puede usar con **azdata**.

|Comando |Descripción |
|:---|:---|
|`azdata login` | Inicio de sesión en un clúster de macrodatos SQL Server |
|`azdata app create` | Cree la aplicación. |
|`azdata app delete` | Eliminar aplicación. |
|`azdata app describe` | Describir aplicación. |
|`azdata app init` | Kickstart nuevo esqueleto de la aplicación. |
|`azdata app list` | Enumerar las aplicaciones. |
|`azdata app run` | Ejecute la aplicación. |
|`azdata app update`| Actualice la aplicación. |

Puede obtener ayuda con el `--help` parámetro, como en el ejemplo siguiente:

```bash
azdata app create --help
```

En las secciones siguientes se describen estos comandos con más detalle.

## <a name="sign-in"></a>Iniciar sesión

Antes de implementar aplicaciones o interactuar con ellas, inicie sesión primero en el SQL Server clúster de Big Data `azdata login` con el comando. Especifique la dirección IP externa del `controller-svc-external` servicio (por ejemplo: `https://ip-address:30080`) junto con el nombre de usuario y la contraseña para el clúster.

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

Si usa AKS, debe ejecutar el siguiente comando para obtener la dirección IP del `mgmtproxy-svc-external` servicio mediante la ejecución de este comando en una ventana de bash o CMD:


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm o Minikube

Si usa Kubeadm o Minikube, ejecute el siguiente comando para obtener la dirección IP para iniciar sesión en el clúster.

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Creación de una aplicación

Para crear una aplicación, use `azdata` con el `app create` comando. Estos archivos residen localmente en el equipo desde el que va a crear la aplicación.

Use la siguiente sintaxis para crear una nueva aplicación en el clúster de Big Data:

```bash
azdata app create --spec <directory containing spec file>
```

El comando siguiente muestra un ejemplo de cómo podría ser este comando:

```bash
azdata app create --spec ./addpy
```

Se supone que la aplicación está almacenada en la `addpy` carpeta. Esta carpeta también debe contener un archivo de especificación para la aplicación, `spec.yaml`denominado. Consulte [la página de implementación de la aplicación](concept-application-deployment.md) para obtener más `spec.yaml` información sobre el archivo.

Para implementar esta aplicación de ejemplo de aplicación, cree los siguientes archivos en un `addpy`directorio denominado:

- `add.py` Copie el siguiente código de Python en este archivo:
   ```py
   #add.py
   def add(x,y):
        result = x+y
        return result
    result=add(x,y)
   ```
- `spec.yaml` Copie el siguiente código en este archivo:
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
azdata app create --spec ./addpy
```

Puede comprobar si la aplicación se implementa con el comando list:

```bash
azdata app list
```

Si la implementación no se ha completado, debería ver `state` el `WaitingforCreate` programa como el ejemplo siguiente:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Una vez que la implementación se realiza correctamente, debería `state` ver el `Ready` cambio de estado:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>Mostrar una aplicación

Puede enumerar las aplicaciones que se crearon correctamente con el `app list` comando.

El siguiente comando muestra todas las aplicaciones disponibles en el clúster de Big Data:

```bash
azdata app list
```

Si especifica un nombre y una versión, se muestra la aplicación específica y su estado (creación o preparación):

```bash
azdata app list --name <app_name> --version <app_version>
```

En el ejemplo siguiente se muestra este comando:

```bash
azdata app list --name add-app --version v1
```

Debería ver una salida similar a la del ejemplo siguiente:

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

Si la aplicación está en un `Ready` estado, puede usarla mediante su ejecución con los parámetros de entrada especificados. Use la siguiente sintaxis para ejecutar una aplicación:

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

El siguiente comando de ejemplo muestra el comando ejecutar:

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

Si la ejecución se realizó correctamente, debería ver el resultado tal como se especificó al crear la aplicación. A continuación se muestra un ejemplo.

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

## <a name="create-an-app-skeleton"></a>Crear un esqueleto de la aplicación

El comando init proporciona un scaffolding con los artefactos relevantes necesarios para implementar una aplicación. En el ejemplo siguiente se crea Hello puede hacerlo mediante la ejecución del siguiente comando.

```bash
azdata app init --name hello --version v1 --template python
```

Se creará una carpeta denominada Hello.  Puede `cd` hacerlo en el directorio e inspeccionar los archivos generados en la carpeta. Spec. yaml define la aplicación, como el nombre, la versión y el código fuente. Puede editar las especificaciones para cambiar el nombre, la versión, la entrada y las salidas.

Este es un ejemplo de salida del comando init que verá en la carpeta

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>Describir una aplicación

El comando de Descripción proporciona información detallada sobre la aplicación, incluido el punto final del clúster. Normalmente, lo usa un desarrollador de aplicaciones para compilar una aplicación con el cliente de Swagger y usar el servicio WebService para interactuar con la aplicación de una manera de RESTful. Consulte uso [de aplicaciones en clústeres de Big Data](big-data-cluster-consume-apps.md) para obtener más información.

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

## <a name="delete-an-app"></a>Eliminación de una aplicación

Para eliminar una aplicación del clúster de Big Data, use la sintaxis siguiente:

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>Pasos siguientes

Explore cómo integrar aplicaciones implementadas en SQL Server clústeres de macrodatos en sus propias aplicaciones en [consumir aplicaciones en clústeres](big-data-cluster-consume-apps.md) de macrodatos para obtener más información. También puede consultar los ejemplos adicionales en [ejemplos de implementación de aplicaciones](https://aka.ms/sql-app-deploy).

Para más información sobre los clústeres de macrodatos de SQL Server, consulte [¿Qué son los clústeres de macrodatos de SQL Server 2019?](big-data-cluster-overview.md).
