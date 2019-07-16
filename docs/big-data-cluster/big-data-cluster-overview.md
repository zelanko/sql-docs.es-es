---
title: ¿Qué son los clústeres de datos de gran tamaño?
titleSuffix: SQL Server big data clusters
description: Obtenga información acerca de los clústeres de macrodatos de 2019 de SQL Server (versión preliminar) que se ejecutan en Kubernetes y proporcionan opciones de escalabilidad horizontal relacionales y datos de HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 166fa1d5b736720b8bab7dff6a8ea56c63a702fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958856"
---
# <a name="what-are-sql-server-big-data-clusters"></a>¿Qué son los clústeres de macrodatos de SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A partir de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], clústeres de macrodatos de SQL Server le permiten implementar clústeres escalables de contenedores HDFS, Spark y SQL Server que se ejecutan en Kubernetes. Estos componentes se ejecutan en paralelo para que pueda leer, escribir y procesar los datos grandes de Transact-SQL o Spark, lo que le permite fácilmente combinar y analizar los datos relacionales de gran valor con grandes volúmenes de datos grandes.

Para obtener más información acerca de las nuevas características y problemas conocidos de la versión más reciente, consulte el [notas de la versión](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Escenarios

Clústeres de macrodatos de SQL Server proporcionan flexibilidad en cómo interactuar con los datos de gran tamaño. Puede consultar los orígenes de datos externos, almacenar datos de gran tamaño en HDFS administrados por SQL Server o consultar los datos de varios orígenes de datos externos a través del clúster. A continuación, puede usar los datos para inteligencia artificial, aprendizaje automático y otras tareas de análisis. Las secciones siguientes proporcionan más información acerca de estos escenarios.

### <a name="data-virtualization"></a>Virtualización de datos

Mediante el aprovechamiento de [SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md), clústeres de macrodatos de SQL Server pueden consultar los orígenes de datos externos sin mover o copiar los datos. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] introduce nuevos conectores a orígenes de datos.

![Virtualización de datos](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Lago de datos

Un clúster de macrodatos de SQL Server incluye un HDFS escalable *bloque de almacenamiento*. Esto puede usarse para almacenar datos grandes, potencialmente introducidos desde varios orígenes externos. Una vez que los datos de gran tamaño se almacenan en HDFS en el clúster de macrodatos, puede analizar y consultar los datos y combinarlos con los datos relacionales.

![Lago de datos](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Escalabilidad horizontal data mart.

Clústeres de macrodatos de SQL Server proporcionan el proceso de escalado horizontal y el almacenamiento para mejorar el rendimiento de análisis de los datos. Datos desde una variedad de orígenes pueden ingeridos y distribuirse entre *grupo datos* nodos como una memoria caché para su posterior análisis.

![Data Mart.](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>Inteligencia artificial integrada y el aprendizaje automático

Clústeres de macrodatos de SQL Server permiten la inteligencia artificial y tareas en los datos almacenados en bloques de almacenamiento HDFS y los grupos de datos de aprendizaje automático. Puede usar Spark, así como herramientas de inteligencia artificial integradas en SQL Server con R, Python, Java o Scala.

![Inteligencia artificial y aprendizaje automático](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Administración y supervisión

Administración y supervisión se proporcionan a través de una combinación de herramientas de línea de comandos, API, portales y vistas de administración dinámica.

Puede usar Azure Data Studio para realizar diversas tareas en el clúster de macrodatos. Esta opción está habilitada por el nuevo **2019 extensión (versión preliminar) de SQL Server**. Esta extensión ofrece:

- Fragmentos de código integrados para tareas comunes de administración.
- Capacidad de examinar HDFS, cargar archivos, archivos de vista previa y crear directorios.
- Capacidad de crear, abrir y ejecutar blocs de notas de Jupyter compatible con.
- Asistente para la virtualización de datos para simplificar la creación de orígenes de datos externos.

## <a id="architecture"></a> Arquitectura

Un clúster de macrodatos de SQL Server es un clúster de contenedores de Linux organizados por [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Conceptos de Kubernetes

Kubernetes es un orquestador de contenedores de código abierto, que se puede escalar las implementaciones de contenedor según necesidad. La siguiente tabla define algunos términos importantes de Kubernetes:

|||
|:--|:--|
| **Cluster** | Un clúster de Kubernetes es un conjunto de equipos, conocidos como nodos. Un nodo controla el clúster y se designa el nodo maestro; los nodos restantes son nodos de trabajo. El maestro de Kubernetes es responsable de distribuir el trabajo entre los trabajadores y para supervisar el estado del clúster. |
| **Node** | Un nodo ejecuta aplicaciones en contenedores. Puede ser una máquina física o una máquina virtual. Un clúster de Kubernetes puede contener una mezcla de los nodos físicos de máquina y la máquina virtual. |
| **pod** | Un pod es la unidad atómica de implementación de Kubernetes. Un pod es un grupo lógico de uno o varios contenedores- y asociadas a los recursos necesarios para ejecutar una aplicación. Cada pod se ejecuta en un nodo; un nodo puede ejecutar uno o varios pods. El maestro de Kubernetes asigna automáticamente los pods a los nodos del clúster. |
| &nbsp; ||

En los clústeres de SQL Server macrodatos, Kubernetes es responsables del estado de los clústeres grandes de datos de SQL Server; Kubernetes crea y configura los nodos del clúster, asigna los pods a nodos y supervisa el estado del clúster.

### <a name="big-data-clusters-architecture"></a>arquitectura de clústeres de macrodatos

Nodos del clúster se organizan en tres planos lógicos: el plano de control, el plano de proceso y el plano de datos. Cada plano tiene responsabilidades diferentes en el clúster. Todos los nodos Kubernetes en un clúster de macrodatos de SQL Server hospeda pods para los componentes de menos a un plano.

![Información general sobre la arquitectura](media/big-data-cluster-overview/architecture-diagram-planes.png)

### <a id="controlplane"></a> Plano de control

El plano de control proporciona administración y seguridad para el clúster. Contiene el patrón de Kubernetes, el *instancia principal de SQL Server*y otros servicios de nivel de clúster como el controlador de Spark y Hive Metastore.

### <a id="computeplane"></a> Plano de proceso

El plano de compute proporciona recursos informáticos para el clúster. Contiene los nodos que ejecutan SQL Server en Linux pods. Los pods en el plano de compute se dividen en *grupos de proceso* específica para las tareas de procesamiento. Un grupo de proceso puede actuar como un [PolyBase](../relational-databases/polybase/polybase-guide.md) grupo de escalabilidad horizontal para las consultas distribuidas a través de datos diferentes orígenes esto como HDFS, Oracle, MongoDB o Teradata.

### <a id="dataplane"></a> Plano de datos

El plano de datos se utiliza para la persistencia de datos y almacenamiento en caché. Contiene el grupo de datos SQL y el grupo de almacenamiento.  El grupo de datos SQL consta de uno o varios pods ejecutando SQL Server en Linux. Se utiliza para introducir datos desde las consultas SQL o trabajos de Spark. Datos de gran tamaño en SQL Server data marts se conservan en el grupo de datos del clúster. El bloque de almacenamiento consta de los pods de grupo de almacenamiento consta de SQL Server en Linux, Spark y HDFS. Todos los nodos de almacenamiento en un clúster de macrodatos de SQL Server son miembros de un clúster de HDFS.

> [!TIP]
> Para obtener información detallada sobre en arquitectura de clúster de macrodatos y la instalación, consulte [taller: Arquitectura de clústeres de macrodatos de Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters).

## <a name="next-steps"></a>Pasos siguientes

Clústeres de macrodatos de SQL Server en primer lugar está disponible como una versión preliminar pública limitada a través del programa de adopción temprana de SQL Server de 2019. Para solicitar acceso, registrar [aquí](https://aka.ms/eapsignup)y especifique su interés para probar los clústeres de datos de gran tamaño. Microsoft todas las solicitudes de evaluación de prioridades y responder tan pronto como sea posible.
