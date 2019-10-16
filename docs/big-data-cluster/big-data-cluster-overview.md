---
title: ¿Qué son los clústeres de Big Data?
titleSuffix: SQL Server Big Data Clusters
description: Obtenga información sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versión preliminar) que se ejecuta en Kubernetes y proporcione opciones de escalado horizontal para datos relacionales y de HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cffb1bcf353932183703f810c876b6adacaa7bbf
ms.sourcegitcommit: 873504573569546eb7223d3afefd89bb3d422d6f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359530"
---
# <a name="what-are-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>¿Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A partir de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] permiten implementar clústeres escalables de contenedores SQL Server, Spark y HDFS que se ejecutan en Kubernetes. Estos componentes se ejecutan en paralelo con objeto de que se puedan leer, escribir y procesar macrodatos de Transact-SQL o Spark, lo que permite combinar y analizar fácilmente los datos relacionales de alto valor con grandes volúmenes de datos.

Para obtener más información sobre las nuevas características y los problemas conocidos de la versión más reciente, consulte las [notas de la versión](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Escenarios

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] proporcionan flexibilidad en la forma de interactuar con los macrodatos. Puede consultar orígenes de datos externos, almacenar macrodatos en HDFS administrados por SQL Server o consultar datos de varios orígenes de datos externos a través del clúster. Luego puede usar los datos en tareas de inteligencia artificial, aprendizaje automático y otras tareas de análisis. En las secciones siguientes se proporciona más información sobre estos escenarios.

### <a name="data-virtualization"></a>Virtualización de datos

Al aprovechar [SQL Server polybase](../relational-databases/polybase/polybase-guide.md), [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] puede consultar orígenes de datos externos sin mover o copiar los datos. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] introduce nuevos conectores para orígenes de datos.

![Virtualización de datos](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

Un clúster de macrodatos de SQL Server incluye un *bloque de almacenamiento* de HDFS escalable. Se puede usar para almacenar macrodatos, que pueden ingerirse de varios orígenes externos. Una vez que los macrodatos se almacenan en HDFS en el clúster de macrodatos, se puede analizar y consultar los datos y combinarlos con los datos relacionales.

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>DataMart de escalabilidad horizontal

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] proporcionan almacenamiento y proceso de escalado horizontal para mejorar el rendimiento del análisis de los datos. Se pueden ingerir y distribuir datos procedentes de diversos orígenes en varios nodos de *grupo de datos* como caché para su análisis posterior.

![DataMart](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>IA y Machine Learning integradas

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] habilita las tareas de inteligencia artificial y aprendizaje automático en los datos almacenados en grupos de almacenamiento de HDFS y en los grupos de datos. Puede usar Spark y las herramientas de inteligencia artificial integradas en SQL Server, con R, Python, Scala o Java.

![IA y ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Administración y supervisión

Se ofrece administración y supervisión mediante una combinación de herramientas de línea de comandos, interfaces API, portales y vistas de administración dinámica.

Puede usar Azure Data Studio para realizar diversas tareas en el clúster de macrodatos. Esto es posible gracias a la nueva **extensión SQL Server 2019 (versión preliminar)** . Esta extensión proporciona:

- Fragmentos de código integrados para las tareas de administración comunes.
- Capacidad de examinar HDFS, cargar archivos, obtener una vista previa de los archivos y crear directorios.
- Capacidad para crear, abrir y ejecutar cuadernos compatibles con Jupyter.
- Asistente para la virtualización de datos para simplificar la creación de orígenes de datos externos.

## <a id="architecture"></a> Arquitectura

Un clúster de macrodatos SQL Server es un clúster de contenedores de Linux organizados por [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Conceptos de Kubernetes

Kubernetes es un orquestador de contenedores de código abierto, que puede escalar las implementaciones de contenedores según sea necesario. En la tabla siguiente se define alguna terminología importante de Kubernetes:

|||
|:--|:--|
| **Cluster** | Un clúster de Kubernetes es un conjunto de máquinas, conocidas como nodos. Un nodo controla el clúster y se designa como nodo maestro; los nodos restantes son nodos de trabajo. El maestro de Kubernetes es responsable de distribuir el trabajo entre los nodos de trabajo y de supervisar el estado del clúster. |
| **Node** | Un nodo ejecuta aplicaciones en contenedores. Puede ser una máquina física o una máquina virtual. Un clúster de Kubernetes puede contener una combinación de nodos de máquina física y de máquina virtual. |
| **Pod** | Un pod es la unidad de implementación atómica de Kubernetes. Un pod es un grupo lógico de uno o más contenedores y recursos asociados necesarios para ejecutar una aplicación. Cada pod se ejecuta en un nodo; un nodo puede ejecutar uno o varios pods. El maestro de Kubernetes asigna pods automáticamente a los nodos del clúster. |
| &nbsp; ||

En [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], Kubernetes es responsable del estado del [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]; Kubernetes compila y configura los nodos del clúster, asigna pods a los nodos y supervisa el estado del clúster.

### <a name="big-data-clusters-architecture"></a>Arquitectura de clústeres de macrodatos

En el diagrama siguiente se muestran los componentes de un clúster de macrodatos para SQL Server.

![Información general sobre la arquitectura](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a> Controlador

El controlador proporciona seguridad y administración para el clúster. Contiene el servicio de control, el almacén de configuración y otros servicios de nivel de clúster como Kibana, Grafana y búsqueda elástica.

### <a id="computeplane"></a> Grupo de proceso

El grupo de proceso proporciona recursos de cálculo al clúster. Contiene nodos que ejecutan SQL Server en pods de Linux. Los pods del grupo de proceso se dividen en *instancias de proceso de SQL* para tareas de procesamiento específicas. 

### <a id="dataplane"></a> Grupo de datos

El grupo de datos se usa para el almacenamiento en caché y la persistencia de datos. El grupo de datos consta de uno o varios pods que ejecutan SQL Server en Linux. Se usa para ingerir datos de consultas SQL o trabajos de Spark. Los data marts del clúster de macrodatos de SQL Server se guardan en el grupo de datos. 

### <a name="storage-pool"></a>Grupo de almacenamiento

El grupo de almacenamiento consiste en módulos de almacenamiento que se componen de SQL Server en Linux, Spark y HDFS. Todos los nodos de almacenamiento de un clúster de macrodatos de SQL Server son miembros de un clúster de HDFS.

> [!TIP]
> Para obtener una visión detallada de la arquitectura y la instalación del clúster de Big Data, consulte [Workshop: arquitectura de Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo implementar clústeres de macrodatos SQL Server, consulte Introducción [a los clústeres de macrodatos de SQL Server](deploy-get-started.md).
