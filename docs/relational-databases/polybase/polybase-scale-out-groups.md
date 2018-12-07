---
title: Grupos de escalado horizontal de PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a145b7ae7194720c8366f0c647a511e086fe4a2d
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52412642"
---
# <a name="polybase-scale-out-groups"></a>Grupos de escalado horizontal de PolyBase

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Una instancia de SQL Server independiente con PolyBase puede convertirse en un cuello de botella de rendimiento cuando se trabaja con grandes conjuntos de datos en Hadoop o Almacenamiento de blobs de Azure. La característica de grupos de PolyBase permite crear un clúster de instancias de SQL Server para procesar grandes conjuntos de datos a partir de orígenes de datos externos, como Hadoop o Almacenamiento de blobs de Azure, en un modo de escalado horizontal para mejorar el rendimiento de las consultas. Ahora puede escalar la capacidad de proceso de SQL Server para satisfacer las demandas de rendimiento de la carga de trabajo. Los grupos de escalado horizontal de PolyBase, un grupo de instancias de SQL Server, permiten procesar grandes conjuntos de datos externos en una arquitectura de procesamiento en paralelo. El rendimiento de las consultas y la carga de datos puede aumentar linealmente a medida que agrega más instancias de SQL Server al grupo. 
  
Vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md) y [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md).
  
![Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/media/polybase-scale-out-groups.png "Grupos de escalado horizontal de PolyBase")  
  
## <a name="head-node"></a>Nodo principal  

El nodo principal contiene la instancia de SQL Server a la que se envían las consultas PolyBase. Cada grupo de PolyBase solo puede tener un nodo principal. Un nodo principal es un grupo lógico del motor de base de datos de SQL, el motor de PolyBase y el servicio de movimiento de datos de PolyBase de la instancia de SQL Server.
  
## <a name="compute-node"></a>Nodo de ejecución  

Un nodo de ejecución contiene la instancia de SQL Server que ayuda a escalar horizontalmente el procesamiento de las consultas de los datos externos. Un nodo de ejecución es un grupo lógico de SQL Server y el servicio de movimiento de datos de PolyBase de la instancia de SQL Server. Un grupo de PolyBase puede tener varios nodos de ejecución. El nodo principal y los nodos de ejecución deben ejecutar la misma versión de SQL Server.

## <a name="scale-out-reads"></a>Lecturas de escalabilidad horizontal

Al consultar instancias externas de SQL Server, Oracle o Teradata, las tablas con particiones se beneficiarán de las lecturas de escalabilidad horizontal. Cada nodo de un grupo de escalado horizontal de PolyBase puede poner en marcha hasta 8 lectores con el fin de leer los datos externos. Y cada lector se asigna a una partición para leer en la tabla externa. 

Por ejemplo, supongamos que tiene una tabla externa de SQL Server con 12 particiones mensuales y un grupo de escalado horizontal de PolyBase de 3 nodos. Cada nodo usará 4 lectores de PolyBase para procesar cada una de las 12 particiones. Este ejemplo se ilustra en la siguiente imagen. 

> [!NOTE]
 Y es diferente de las lecturas de escalabilidad horizontal a través de Hadoop. 

![Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/media/polybase-scale-out-groups2.png "Grupos de escalado horizontal de PolyBase")
  
## <a name="distributed-query-processing"></a>Procesamiento de consultas distribuidas  

Las consultas de PolyBase se envían a SQL Server en el nodo principal. La parte de la consulta que hace referencia a las tablas externas se entregan al motor de PolyBase.
  
El motor de PolyBase es el componente principal que está detrás de las consultas de PolyBase. Analiza la consulta en los datos externos, genera el plan de consulta y distribuye el trabajo al servicio de movimiento de datos de los nodos de ejecución para ejecutarlos. Tras finalizar el trabajo, recibe los resultados de los nodos de ejecución y los envía a SQL Server para procesarlos y devolverlos al cliente.
  
El servicio de movimiento de datos de PolyBase recibe instrucciones del motor de PolyBase y transfiere los datos entre HDFS y SQL Server, y entre las instancias de SQL Server de los nodos principal y de ejecución.
  
## <a name="editions-availability"></a>Disponibilidad de ediciones  

Después de instalar SQL Server, la instancia puede designarse como nodo principal o de ejecución. La elección dependerá de qué versión de SQL Server PolyBase se esté ejecutando. En una instalación de Enterprise Edition, la instancia se puede designar como nodo principal o de ejecución. En Standard Edition, la instancia solo puede designarse como nodo de ejecución.

## <a name="next-steps"></a>Pasos siguientes

Para configurar un grupo de escalado horizontal de PolyBase, consulte la guía siguiente:

[Improve PolyBase scale-out groups on Windows](configure-scale-out-groups-windows.md) (mejora de los grupos de escalado horizontal de PolyBase en Windows)
