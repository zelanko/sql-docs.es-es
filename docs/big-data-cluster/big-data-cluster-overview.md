---
title: ¿Qué son los clústeres de Big Data?
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre los clústeres de macrodatos de SQL Server 2019 (versión preliminar) que se ejecutan en Kubernetes y proporcionan opciones de escalado horizontal para datos relacionales y HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0beb4ea57ba6c2591e5b2c06a7775fc2d7e8b26c
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419497"
---
# <a name="what-are-sql-server-big-data-clusters"></a>¿Qué son los clústeres de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A partir [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]de, SQL Server los clústeres de macrodatos permiten implementar clústeres escalables de SQL Server, Spark y contenedores HDFS que se ejecutan en Kubernetes. Estos componentes se ejecutan en paralelo para que pueda leer, escribir y procesar macrodatos de Transact-SQL o Spark, lo que le permite combinar y analizar fácilmente los datos relacionales de alto valor con grandes volúmenes de datos.

Para obtener más información sobre las nuevas características y los problemas conocidos de la versión más reciente, consulte las notas de la [versión](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Escenarios

SQL Server los clústeres de macrodatos proporcionan flexibilidad a la hora de interactuar con los macrodatos. Puede consultar orígenes de datos externos, almacenar Big Data in HDFS administrados por SQL Server o consultar datos de varios orígenes de datos externos a través del clúster. Después, puede usar los datos para las tareas de análisis, aprendizaje automático y de inteligencia artificial. En las secciones siguientes se proporciona más información acerca de estos escenarios.

### <a name="data-virtualization"></a>Virtualización de datos

Al aprovechar [SQL Server polybase](../relational-databases/polybase/polybase-guide.md), los clústeres de macrodatos SQL Server pueden consultar orígenes de datos externos sin mover o copiar los datos. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]introduce nuevos conectores en los orígenes de datos.

![Virtualización de datos](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

Un clúster de macrodatos SQL Server incluye un *grupo de almacenamiento*de HDFS escalable. Se puede usar para almacenar datos de gran tamaño, que se pueden ingerir de varios orígenes externos. Una vez que los macrodatos se almacenan en HDFS en el clúster de Big Data, puede analizar y consultar los datos y combinarlos con los datos relacionales.

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>data mart de escalado horizontal

SQL Server los clústeres de macrodatos proporcionan almacenamiento y proceso de escalado horizontal para mejorar el rendimiento del análisis de los datos. Los datos de diversos orígenes se pueden ingerir y distribuir en los nodos del *grupo de datos* como una memoria caché para su posterior análisis.

![Data Mart](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>Integrated AI y Machine Learning

SQL Server los clústeres de macrodatos permiten realizar tareas de aprendizaje automático y de inteligencia artificial en los datos almacenados en grupos de almacenamiento de HDFS y en los grupos de datos. Puede usar Spark y las herramientas de inteligencia artificial integradas en SQL Server, con R, Python, Scala o Java.

![AI y ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Administración y supervisión

La administración y la supervisión se proporcionan a través de una combinación de herramientas de línea de comandos, API, portales y vistas de administración dinámica.

Puede usar Azure Data Studio para realizar diversas tareas en el clúster de Big Data. Esta opción está habilitada por la nueva **extensión SQL Server 2019 (versión preliminar)** . Esta extensión proporciona:

- Fragmentos de código integrados para las tareas de administración comunes.
- Capacidad de examinar HDFS, cargar archivos, obtener una vista previa de los archivos y crear directorios.
- Capacidad para crear, abrir y ejecutar notebooks compatibles con Jupyter.
- Asistente para la virtualización de datos para simplificar la creación de orígenes de datos externos.

## <a id="architecture"></a>Arquitectura

Un clúster de macrodatos SQL Server es un clúster de contenedores de Linux organizados por [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Conceptos de Kubernetes

Kubernetes es un orquestador de contenedor de código abierto, que puede escalar las implementaciones de contenedores según sea necesario. En la tabla siguiente se define alguna terminología importante de Kubernetes:

|||
|:--|:--|
| **Cluster** | Un clúster de Kubernetes es un conjunto de equipos, conocidos como nodos. Un nodo controla el clúster y se designa como nodo maestro. los nodos restantes son nodos de trabajo. El maestro Kubernetes es responsable de distribuir el trabajo entre los trabajadores y de supervisar el estado del clúster. |
| **Node** | Un nodo ejecuta aplicaciones en contenedor. Puede ser un equipo físico o una máquina virtual. Un clúster de Kubernetes puede contener una mezcla de máquinas físicas y nodos de máquinas virtuales. |
| **Caja** | Un POD es la unidad de implementación atómica de Kubernetes. Un POD es un grupo lógico de uno o más contenedores, y recursos asociados, necesarios para ejecutar una aplicación. Cada Pod se ejecuta en un nodo; un nodo puede ejecutar uno o varios pods. El maestro de Kubernetes asigna Pod automáticamente a los nodos del clúster. |
| &nbsp; ||

En los clústeres de macrodatos de SQL Server, Kubernetes es responsable del estado de los clústeres de macrodatos SQL Servers; Kubernetes compila y configura los nodos del clúster, asigna pods a los nodos y supervisa el estado del clúster.

### <a name="big-data-clusters-architecture"></a>Arquitectura de clústeres de Big Data

En el diagrama siguiente se muestran los componentes de un clúster de Big Data para SQL Server.

![Información general sobre la arquitectura](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a>Módem

El controlador proporciona seguridad y administración para el clúster. Contiene el servicio cntrol, el almacén de configuración y otros servicios en el nivel de clúster, como Kibana, Grafana y búsqueda elástica.

### <a id="computeplane"></a>Grupo de proceso

El grupo de proceso proporciona recursos de cálculo al clúster. Contiene nodos que ejecutan SQL Server en Linux pods. Los pods del grupo de proceso se dividen en instancias de proceso de *SQL* para tareas de procesamiento específicas. 

### <a id="dataplane"></a>Grupo de datos

El grupo de datos se usa para la persistencia y el almacenamiento en caché de datos. El grupo de datos consta de uno o varios pods que se ejecutan SQL Server en Linux. Se usa para ingerir datos de consultas SQL o trabajos de Spark. SQL Server Data Marts del clúster de macrodatos se guardan en el grupo de datos. 

### <a name="storage-pool"></a>Grupo de almacenamiento

El bloque de almacenamiento consta de los pods del grupo de almacenamiento compuestos por SQL Server en Linux, Spark y HDFS. Todos los nodos de almacenamiento de un clúster de macrodatos SQL Server son miembros de un clúster de HDFS.

> [!TIP]
> Para obtener una visión detallada de la arquitectura y la instalación del clúster de Big [Data, consulte Workshop: Microsoft SQL Server arquitectura](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)de clústeres de macrodatos.

## <a name="next-steps"></a>Pasos siguientes

SQL Server clústeres de macrodatos está disponible primero como una versión preliminar pública limitada a través del programa de adopción temprana SQL Server 2019. Para solicitar acceso, Regístrese [aquí](https://aka.ms/eapsignup)y especifique su interés para probar los clústeres de Big Data. Microsoft evaluará todas las solicitudes y responderá lo antes posible.
