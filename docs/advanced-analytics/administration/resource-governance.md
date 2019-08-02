---
title: Regulación de recursos para la ejecución de scripts de R y Python
description: Asigne memoria RAM, CPU y e/s para cargas de trabajo de R y Python en SQL Server instancia del motor de base de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 55a83e7e63a4e43afe1168aab3307f2806a55fca
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715260"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>Regulación de recursos para machine learning en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Los algoritmos de ciencia de datos y aprendizaje automático son de cálculo intensivo. En función de las prioridades de la carga de trabajo, es posible que tenga que aumentar los recursos disponibles para la ciencia de datos o reducir el reaprovisionamiento si la ejecución de scripts de R y Python reduce el rendimiento de otros servicios que se ejecutan simultáneamente. 

Cuando necesite reequilibrar la distribución de recursos del sistema entre varias cargas de trabajo, puede usar [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para asignar recursos de CPU, e/s física y de memoria utilizados por los tiempos de ejecución externos para R y Python. Si cambia las asignaciones de recursos, recuerde que es posible que también tenga que reducir la cantidad de memoria reservada para otras cargas de trabajo y servicios. 

> [!NOTE] 
> Resource Governor es una característica de la edición Enterprise.

## <a name="default-allocations"></a>Asignaciones predeterminadas

De forma predeterminada, los tiempos de ejecución de scripts externos para el aprendizaje automático están limitados a no más del 20% de la memoria total de la máquina. Depende del sistema, pero, en general, es posible que este límite no sea adecuado para tareas de aprendizaje automático graves como el entrenamiento de un modelo o la predicción de muchas filas de datos. 

## <a name="use-resource-governor-to-control-resourcing"></a>Usar Resource Governor para controlar el reabastecimiento
 
De forma predeterminada, los procesos externos usan hasta un 20% de la memoria total del host en el servidor local. Puede modificar el grupo de recursos predeterminado para realizar cambios en todo el servidor, con procesos de R y Python que utilizan cualquier capacidad que esté disponible para los procesos externos.

Como alternativa, puede crear grupos de *recursos externos*personalizados, con clasificadores y grupos de cargas de trabajo asociados, para determinar la asignación de recursos para las solicitudes procedentes de programas específicos, hosts u otros criterios que proporcione. Un grupo de recursos externos es un tipo de grupo de recursos [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] introducido en para ayudar a administrar los procesos de R y Python externos al motor de base de datos.

1. [Habilitación del gobierno de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (está desactivado de forma predeterminada).

2. Ejecute [Crear grupo de recursos externos](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) para crear y configurar el grupo de recursos, seguido de [ALTER Resource Governor](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) para implementarlo.

3. Cree un grupo de cargas de trabajo para asignaciones pormenorizadas, por ejemplo entre entrenamiento y puntuación.

4. Cree un clasificador para interceptar las llamadas de procesamiento externo.

5. Ejecutar consultas y procedimientos con los objetos creados.

Para ver un tutorial, consulte [creación de un grupo de recursos para scripts de R y Python externos](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md) para obtener instrucciones paso a paso.

Para obtener una introducción a la terminología y los conceptos generales, vea [Resource Governor grupo de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Procesos en regulación de recursos
  
 Puede usar un *grupo de recursos externos* para administrar los recursos utilizados por los siguientes ejecutables en una instancia del motor de base de datos:

+ Rterm. exe cuando se llama localmente desde SQL Server o se llama de forma remota con SQL Server como el contexto de cálculo remoto
+ Python. exe cuando se llama localmente desde SQL Server o se llama de forma remota con SQL Server como el contexto de cálculo remoto
+ BxlServer.exe y procesos satélite
+ Procesos satélite iniciados por Launchpad, como PythonLauncher. dll
  
> [!NOTE]
> No se admite la administración directa del servicio Launchpad mediante Resource Governor. Launchpad es un servicio de confianza que solo puede hospedar iniciadores proporcionados por Microsoft. Los iniciadores de confianza se configuran explícitamente para evitar el consumo excesivo de recursos.
  
## <a name="see-also"></a>Vea también

+ [Administrar la integración de machine learning](../r/managing-and-monitoring-r-solutions.md)
+ [Creación de grupos de recursos para el aprendizaje automático](../r/how-to-create-a-resource-pool-for-r.md)
+ [Resource Governor de grupos de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
