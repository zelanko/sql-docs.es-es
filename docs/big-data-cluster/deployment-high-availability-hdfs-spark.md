---
title: Implementación de HDFS o Spark con alta disponibilidad
titleSuffix: Deploy HDFS or Spark with high availability
description: Obtenga información sobre cómo implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versión preliminar) con alta disponibilidad.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: afd8aa5d124e7dc6c7d37bb44c9b64129f8fa564
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532026"
---
# <a name="deploy-hdfs-name-node-and-shared-spark-services-in-a-highly-available-configuration"></a>Implementación del nodo de nombre de HDFS y de los servicios de Spark compartidos en una configuración de alta disponibilidad

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Además de implementar la instancia maestra de SQL Server en una configuración de alta disponibilidad usando grupos de disponibilidad, se pueden implementar otros servicios críticos en el clúster de macrodatos para garantizar un mayor nivel de confiabilidad. Puede configurar `HDFS name node` y los servicios de Spark compartidos agrupados en `SparkHead` con una réplica adicional. En este caso, `Zookeeper` también se implementa en el clúster de macrodatos en el servidor como coordinador de clústeres y almacén de metadatos de los siguientes servicios: 

- Nodo de nombre de HDFS
- Livy Resource Manager y Yarn Resource Manager 

El historial de Spark, el historial de trabajos y el servicio de metadatos de Hive son servicios sin estado. Zookeeper no interviene para garantizar el estado de servicio de estos componentes. 

La implementación de varias réplicas relativas a estos servicios da como resultado una escalabilidad y confiabilidad mejores, así como un equilibrio de carga de las cargas de trabajo entre las réplicas disponibles.

> [!NOTE]
> Los siguientes servicios se implementan como contenedores en el pod `sparkhead`: 
> - Livy
> - Yarn Resource Manager
> - Historial de Spark
> - Historial de trabajos
> - Servicio de metadatos de Hive  
>

En la siguiente imagen se muestra una implementación de HA de Spark en un clúster de macrodatos de SQL Server:

:::image type="content" source="media/deployment-high-availability-hdfs-spark/spark-ha.png" alt-text="spark-ha-bdc":::

En la siguiente imagen se muestra una implementación de HA de HDFS en un clúster de macrodatos de SQL Server:

:::image type="content" source="media/deployment-high-availability-hdfs-spark/hdfs-ha.png" alt-text="hdfs-ha-bdc":::

## <a name="deploy"></a>Implementar

Si el nodo de nombre o el encabezado de Spark están configurados con dos réplicas, también debe configurar el recurso de Zookeeper con tres réplicas. En una configuración de alta disponibilidad del nodo de nombre de HDFS, dos pod hospedan las dos réplicas. Los pods son `nmnode-0` y `nmnode-1`. Esta configuración es activa-pasiva: solo uno de los nodos de nombre está activo, mientras que el otro está en espera y se activa como resultado de un evento de conmutación por error. 

Puede usar los perfiles de configuración integrados `aks-dev-test-ha` o `kubeadm-prod` para empezar a personalizar la implementación del clúster de macrodatos. Estos perfiles incluyen la configuración necesaria relativa a los recursos que permiten configurar alta disponibilidad extra. Por ejemplo, aquí se muestra una sección del archivo de configuración `bdc.json` que es pertinente para implementar el nodo de nombre de HDFS, Zookeeper y recursos de Spark compartidos (`sparkhead`) con alta disponibilidad.  

```json
{
  ...
    "nmnode-0": {
        "spec": {
            "replicas": 2
        }
    },
    "sparkhead": {
        "spec": {
            "replicas": 2
        }
    },
    "zookeeper": {
        "spec": {
            "replicas": 3
        }
    },
  ...
}
```

Como procedimiento recomendado, en una implementación de producción también hay que establecer la replicación de bloque de HDFS en 3. Esta configuración ya está especificada en los perfiles `aks-dev-test-ha` y `kubeadm-prod`. Vea la sección siguiente del archivo de configuración `bdc.json`:

```json
{
  ...
  "hdfs": {
      "resources": [
          "nmnode-0",
          "zookeeper",
          "storage-0",
          "sparkhead"
      ],
      "settings": {
          "hdfs-site.dfs.replication": "3"
      }
  },
  ...
}
```

## <a name="known-limitations"></a>Restricciones conocidas

Estos son los problemas conocidos y las limitaciones concernientes a la configuración de alta disponibilidad de los servicios de Hadoop en clústeres de macrodatos de SQL Server:

- Todas las configuraciones se deben especificar en el momento de la implementación de clústeres de macrodatos. En la versión SQL Server 2019 CU1, la configuración de alta disponibilidad no se puede habilitar después de la implementación.

## <a name="next-steps"></a>Pasos siguientes

- Para más información sobre cómo usar archivos de configuración en implementaciones de clústeres de macrodatos, vea [Cómo implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Kubernetes](deployment-guidance.md#configfile).
- Para más información sobre las opciones de alta disponibilidad de instancias maestras de SQL Server en clústeres de macrodatos, vea [Implementación de una instancia maestra de SQL Server con alta disponibilidad](deployment-high-availability.md).
