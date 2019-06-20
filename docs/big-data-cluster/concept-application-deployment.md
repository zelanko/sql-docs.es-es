---
title: ¿Qué es la implementación de aplicaciones?
titleSuffix: SQL Server 2019 big data clusters
description: Este artículo describe la implementación de aplicaciones en un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: jterh
ms.author: jroth
manager: jroth
ms.date: 03/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1a6ba9caed2b01abc50e16e34d1a13413af2d0ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801856"
---
# <a name="what-is-application-deployment-on-a-sql-server-2019-big-data-cluster"></a>¿Qué es la implementación de aplicaciones en un clúster de macrodatos de 2019 de SQL Server?

Implementación de aplicaciones permite la implementación de aplicaciones en el clúster de macrodatos, ya que proporciona interfaces para crear, administrar y ejecutar aplicaciones. Las aplicaciones implementadas en el clúster de macrodatos beneficiarán de la potencia de cálculo del clúster y pueden tener acceso a los datos que está disponibles en el clúster. Esto aumenta la escalabilidad y rendimiento de las aplicaciones, al administrar las aplicaciones donde residen los datos.
Las secciones siguientes describen la arquitectura y la funcionalidad de implementación de la aplicación.

## <a name="application-deployment-architecture"></a>Arquitectura de implementación de aplicación

Implementación de la aplicación consta de un controlador y controladores de tiempo de ejecución de la aplicación. Al crear una aplicación, un archivo de especificación (`spec.yaml`) se proporciona. Esto `spec.yaml` archivo contiene todo lo que el controlador necesita saber para implementar correctamente la aplicación. El siguiente es un ejemplo del contenido para `spec.yaml`:

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

Inspecciona el controlador de la `runtime` especificado en el `spec.yaml` de archivo y llama al controlador de tiempo de ejecución correspondiente. El controlador de tiempo de ejecución crea la aplicación. En primer lugar, un Kubernetes ReplicaSet se crea que contiene uno o varios pods, cada uno de los cuales contiene la aplicación para su implementación. El número de pods que se define mediante el `replicas` parámetro establecido el `spec.yaml` archivo para la aplicación. Cada pod puede tener uno de los grupos más. El número de grupos se define mediante el `poolsize` parámetro establecido el `spec.yaml` archivo.

Esta configuración tiene un impacto en la cantidad de solicitudes que puede controlar la implementación en paralelo. El número máximo de solicitudes en un momento dado es igual a `replicas` veces `poolsize`. Si tiene 5 réplicas y 2 grupos por réplica de la implementación puede controlar 10 solicitudes en paralelo. Consulte la siguiente imagen para una representación gráfica de `replicas` y `poolsize`:

![TamañoDeGrupo y réplicas](media/big-data-cluster-create-apps/poolsize-vs-replicas.png)

Después de que se ha creado el ReplicaSet y se han iniciado los pods, se crea un trabajo cron si un `schedule` se estableció el `spec.yaml` archivo. Por último, se crea un Kubernetes Service que puede usarse para administrar y ejecutar la aplicación (ver abajo).

Cuando se ejecuta una aplicación, el servicio de Kubernetes para los servidores proxy de aplicación las solicitudes a una réplica y devuelve los resultados.

## <a name="how-to-work-with-application-deployment"></a>Cómo trabajar con la implementación de aplicaciones

Las dos interfaces principales para la implementación de aplicación son: 
- [Interfaz de línea de comandos `mssqlctl`](big-data-cluster-create-apps.md)
- [Extensión de Visual Studio Code y Azure Data Studio](app-deployment-extension.md)

También es posible que una aplicación se ejecute mediante un servicio web RESTful. Para obtener más información, consulte [consumir las aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo crear y ejecutar aplicaciones en clústeres de macrodatos de SQL Server, consulte lo siguiente:

- [Implementar aplicaciones con mssqlctl](big-data-cluster-create-apps.md)
- [Implementar aplicaciones con la extensión de la implementación de aplicaciones](app-deployment-extension.md)
- [Consumir las aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md)

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, consulte la información general siguiente:

- [¿Qué son los clústeres de macrodatos de 2019 de SQL Server?](big-data-cluster-overview.md)
