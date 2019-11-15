---
title: ¿Qué es la implementación de la aplicación?
titleSuffix: Big Data Clusters for SQL Server 2019
description: En este artículo se describe la implementación de la aplicación en clústeres de macrodatos para SQL Server 2019.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: da497f8d7c435a807ba530ae619ff91a6f2dff71
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653003"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>¿Qué es la implementación de la aplicación en un clúster de macrodatos de SQL Server 2019?

La implementación de la aplicación permite la implementación de aplicaciones en el clúster de macrodatos proporcionando interfaces para crear, administrar y ejecutar aplicaciones. Las aplicaciones implementadas en el clúster de macrodatos se benefician de la capacidad de cálculo del clúster y pueden tener acceso a los datos que están disponibles en el clúster. Esto aumenta la escalabilidad y el rendimiento de las aplicaciones, al tiempo que se administran las aplicaciones en las que residen los datos.
En las secciones siguientes se describe la arquitectura y funcionalidad de la implementación de la aplicación.

## <a name="application-deployment-architecture"></a>Arquitectura de implementación de la aplicación

La implementación de la aplicación consta de un controlador y controladores de tiempo de ejecución de la aplicación. Al crear una aplicación, se proporciona un archivo de especificación (`spec.yaml`). Este archivo `spec.yaml` contiene todo lo que el controlador necesita saber para implementar correctamente la aplicación. A continuación se muestra un ejemplo del contenido de `spec.yaml`:

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

El controlador inspecciona el `runtime` especificado en el archivo `spec.yaml` y llama al controlador en tiempo de ejecución correspondiente. El controlador en tiempo de ejecución crea la aplicación. En primer lugar, se crea un conjunto ReplicaSet de Kubernetes que contiene uno o varios pods, cada uno de los cuales contiene la aplicación que se va a implementar. El número de pods se define mediante el parámetro `replicas` establecido en el archivo `spec.yaml` de la aplicación. Cada pod puede tener uno o más grupos. El número de grupos se define mediante el parámetro `poolsize` establecido en el archivo `spec.yaml`.

Esta configuración afecta a la cantidad de solicitudes que la implementación puede controlar en paralelo. El número máximo de solicitudes en un momento dado es igual a `replicas` veces `poolsize`. Si tiene 5 réplicas y 2 grupos por réplica, la implementación puede administrar 10 solicitudes en paralelo. Vea la imagen a continuación para obtener una representación gráfica de `replicas` y `poolsize`:

![Poolsize y replicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Una vez que se ha creado el conjunto ReplicaSet y se han iniciado los pods, se crea un trabajo cron si se ha establecido `schedule` en el archivo `spec.yaml`. Por último, se crea un servicio de Kubernetes que se puede usar para administrar y ejecutar la aplicación (consulte a continuación).

Cuando se ejecuta una aplicación, el servicio Kubernetes de la aplicación envía por proxy las solicitudes a una réplica y devuelve los resultados.

## <a name="how-to-work-with-application-deployment"></a>Cómo trabajar con la implementación de la aplicación

Las dos interfaces principales de la implementación de la aplicación son: 
- [Interfaz de línea de comandos`azdata`](big-data-cluster-create-apps.md)
- [Extensión de Visual Studio Code y Azure Data Studio](app-deployment-extension.md)

También es posible ejecutar una aplicación mediante un servicio web de RESTful. Para más información, consulte [Consumo de aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo crear y ejecutar aplicaciones en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vea lo siguiente:

- [Implementar aplicaciones con azdata](big-data-cluster-create-apps.md)
- [Implementación de aplicaciones con la extensión de implementación de la aplicación](app-deployment-extension.md)
- [Consumo de aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md)

Para obtener más información sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vea la siguiente introducción:

- [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
