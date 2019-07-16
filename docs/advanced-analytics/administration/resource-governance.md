---
title: Regulación de recursos para la ejecución del script R y Python - SQL Server Machine Learning
description: Asignar memoria RAM, CPU y E/S para cargas de trabajo de R y Python en la instancia del motor de base de datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e6063f8367e5b91e7e935d6f92515a6dd452dc56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963134"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>Regulación de recursos de aprendizaje automático en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Algoritmos de aprendizaje automático y ciencia de datos son de cálculo intensivos. Dependiendo de las prioridades de la carga de trabajo, es posible que deba aumentar los recursos disponibles para la ciencia de datos o disminución de recursos si la ejecución del script de R y Python, elimina el rendimiento de otros servicios que se ejecutan simultáneamente. 

Cuando necesite volver a equilibrar la distribución de los recursos del sistema a través de varias cargas de trabajo, puede usar [del regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) para asignar la CPU, E/S física y los recursos de memoria consumidos por los tiempos de ejecución externos para R y Python. Si cambiar las asignaciones de recursos, recuerde que es posible que deba también reducen la cantidad de memoria reservada para otros servicios y cargas de trabajo. 

> [!NOTE] 
> El regulador de recursos es una característica de Enterprise Edition.

## <a name="default-allocations"></a>Asignaciones predeterminadas

De forma predeterminada, los tiempos de ejecución de scripts externos para el aprendizaje automático se limitan a no más de 20% de memoria total del equipo. Depende de su sistema, pero en general, podría encontrar este límite suficiente para realizar tareas como entrenar un modelo o la predicción del número de filas de datos de aprendizaje automático de graves. 

## <a name="use-resource-governor-to-control-resourcing"></a>Usar el regulador de recursos para controlar los recursos
 
De forma predeterminada, los procesos externos usan hasta un 20% de memoria total del host en el servidor local. Puede modificar el grupo de recursos predeterminado para realizar cambios de todo el servidor, con R y los procesos de Python utilizando independientemente de su capacidad que esté disponible para los procesos externos.

Como alternativa, puede construir personalizado *grupos de recursos externos*, con grupos de carga de trabajo asociados y clasificadores, para determinar la asignación de recursos para las solicitudes procedentes de programas específicos, hosts u otros criterios que proporcionan. Un grupo de recursos externos es un tipo de grupo de recursos que se introdujo en [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para ayudar a administrar los procesos de R y Python externos al motor de base de datos.

1. [Habilitar regulación de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (está desactivada de forma predeterminada).

2. Ejecute [CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) para crear y configurar el grupo de recursos, seguido de [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) para implementarlo.

3. Cree un grupo de cargas de trabajo para las asignaciones granulares, por ejemplo entre el entrenamiento y puntuación.

4. Crear un clasificador para interceptar las llamadas para su procesamiento externo.

5. Ejecutar consultas y procedimientos con los objetos que creó.

Para ver un tutorial, vea [cómo crear un grupo de recursos para los scripts de R y Python externos](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md) para obtener instrucciones paso a paso.

Para obtener una introducción a la terminología y conceptos generales, vea [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Procesos de regulación de recursos
  
 Puede usar un *grupo de recursos externos* para administrar los recursos utilizados por los siguientes archivos ejecutables en una instancia del motor de base de datos:

+ Rterm.exe cuando llamado localmente desde SQL Server o llamado remotamente con SQL Server como el contexto de cálculo remoto
+ Python.exe cuando llamado localmente desde SQL Server o llamado remotamente con SQL Server como el contexto de cálculo remoto
+ BxlServer.exe y procesos satélite
+ Procesos satélite iniciados por Launchpad, como PythonLauncher.dll
  
> [!NOTE]
> No se admite la administración directa del servicio Launchpad mediante el uso del regulador de recursos. LaunchPad es un servicio de confianza que puede solo los iniciadores de host proporcionados por Microsoft. Los selectores de confianza se configuran explícitamente para evitar que se consuman demasiados recursos.
  
## <a name="see-also"></a>Vea también

+ [Administrar la integración de machine learning](../r/managing-and-monitoring-r-solutions.md)
+ [Creación de grupos de recursos para el aprendizaje automático](../r/how-to-create-a-resource-pool-for-r.md)
+ [Grupos de recursos del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
