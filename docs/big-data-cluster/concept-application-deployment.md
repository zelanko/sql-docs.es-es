---
title: ¿Qué es la implementación de aplicaciones?
titleSuffix: SQL Server 2019 big data clusters
description: En este artículo se describe la implementación de aplicaciones en un clúster de macrodatos SQL Server 2019 (versión preliminar).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d8cc44862af21c54bdbd0e4adbb35db912c3f7c9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419408"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>¿Qué es la implementación de aplicaciones en un clúster de macrodatos SQL Server 2019?

La implementación de aplicaciones permite la implementación de aplicaciones en el clúster de Big Data proporcionando interfaces para crear, administrar y ejecutar aplicaciones. Las aplicaciones implementadas en el clúster de macrodatos se benefician de la capacidad de cálculo del clúster y pueden tener acceso a los datos que están disponibles en el clúster. Esto aumenta la escalabilidad y el rendimiento de las aplicaciones, al tiempo que se administran las aplicaciones en las que residen los datos.
En las secciones siguientes se describe la arquitectura y la funcionalidad de la implementación de aplicaciones.

## <a name="application-deployment-architecture"></a>Arquitectura de implementación de aplicaciones

La implementación de la aplicación consta de un controlador y controladores de tiempo de ejecución de la aplicación. Al crear una aplicación, se proporciona un archivo`spec.yaml`de especificación (). Este `spec.yaml` archivo contiene todo lo que el controlador necesita saber para implementar correctamente la aplicación. A continuación se muestra un ejemplo del contenido de `spec.yaml`:

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

El controlador inspecciona el `runtime` especificado en el `spec.yaml` archivo y llama al controlador en tiempo de ejecución correspondiente. El controlador en tiempo de ejecución crea la aplicación. En primer lugar, se crea una Kubernetes ReplicaSet que contiene uno o varios pods, cada uno de los cuales contiene la aplicación que se va a implementar. El número de pods se define mediante el `replicas` parámetro establecido en el `spec.yaml` archivo de la aplicación. Cada Pod puede tener uno o más grupos. El número de grupos se define mediante el `poolsize` parámetro establecido en el `spec.yaml` archivo.

Esta configuración afecta a la cantidad de solicitudes que la implementación puede controlar en paralelo. El número máximo de solicitudes en un momento dado es igual a `replicas` veces. `poolsize` Si tiene 5 réplicas y 2 grupos por réplica, la implementación puede administrar 10 solicitudes en paralelo. Vea la imagen siguiente para obtener una representación gráfica `replicas` de `poolsize`y:

![Agrupar las réplicas y](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Una vez que se ha creado el ReplicaSet y se han iniciado los pods, se crea un trabajo `schedule` cron si se ha `spec.yaml` establecido un en el archivo. Por último, se crea un servicio de Kubernetes que se puede usar para administrar y ejecutar la aplicación (consulte a continuación).

Cuando se ejecuta una aplicación, el servicio Kubernetes de la aplicación realiza el proxy de las solicitudes a una réplica y devuelve los resultados.

## <a name="how-to-work-with-application-deployment"></a>Cómo trabajar con la implementación de aplicaciones

Las dos interfaces principales para la implementación de aplicaciones son: 
- [Interfaz de línea de comandos`azdata`](big-data-cluster-create-apps.md)
- [Extensión de Visual Studio Code y Azure Data Studio](app-deployment-extension.md)

También es posible ejecutar una aplicación mediante un servicio web RESTful. Para más información, consulte [consumo de aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo crear y ejecutar aplicaciones en SQL Server clústeres de macrodatos, vea lo siguiente:

- [Implementación de aplicaciones mediante azdata](big-data-cluster-create-apps.md)
- [Implementación de aplicaciones con la extensión de implementación de aplicaciones](app-deployment-extension.md)
- [Consumo de aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md)

Para obtener más información acerca de los clústeres de macrodatos SQL Server, consulte la siguiente información general:

- [¿Qué son los clústeres de macrodatos SQL Server 2019?](big-data-cluster-overview.md)
