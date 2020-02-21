---
title: Machine Learning Services (Python, R)
titleSuffix: SQL Server Big Data Clusters
description: Obtenga información sobre ejecutar scripts de Python y R en la instancia maestra de clústeres de macrodatos de SQL Server con Machine Learning Services.
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
ms.openlocfilehash: e16304765e5f4a51feed4d3d59e790505baa740d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252023"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>Ejecución de scripts de Python y R con Machine Learning Services en clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Se pueden ejecutar scripts de Python y R en la instancia maestra de [clústeres de macrodatos de SQL Server](big-data-cluster-overview.md) con [Machine Learning Services](../advanced-analytics/index.yml).

> [!NOTE]
> También se puede ejecutar código Java en esa instancia maestra con [extensiones de lenguaje de SQL Server](../language-extensions/language-extensions-overview.md). Si sigue los pasos que se indican aquí, también se habilitarán las extensiones de lenguaje.

## <a name="enable-machine-learning-services"></a>Habilitar Machine Learning Services

Machine Learning Services se instala de forma predeterminada en clústeres de macrodatos y no precisa de una instalación independiente.

Para habilitar Machine Learning Services, ejecute esta instrucción en la instancia maestra:

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

## <a name="enable-always-on-availability-groups"></a>Habilitación de grupos de disponibilidad AlwaysOn

Si usa clústeres de macrodatos de SQL Server con [Grupos de disponibilidad Always On](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md), deberá realizar algunos pasos más para habilitar Machine Learning Services.

1. Conéctese a la instancia maestra y ejecute esta instrucción:

    ```sql
    SELECT @@SERVERNAME
    ```

    Anote el nombre del servidor. En este ejemplo, el nombre del servidor de la instancia maestra es **master-2**.

1. En cada réplica del grupo de disponibilidad Always On del Clúster de macrodatos, ejecute estos comandos `kubectl`:

    ```
    kubectl -n bdc expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer

    kubectl -n bdc expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer

    kubectl -n bdc expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer
    ```

    Debería aparecer una salida similar a la siguiente:
    
    ```
    service/mymaster-0 exposed

    service/mymaster-1 exposed

    service/mymaster-2 exposed
    ```

1. Conéctese a cada punto de conexión de réplica principal y habilite la ejecución del script.

    Ejecute esta instrucción:

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

Ya está listo para ejecutar scripts de Python y R en la instancia maestra de clústeres de macrodatos. Vea las siguientes guías de inicio rápido para ejecutar su primer script.

## <a name="next-steps"></a>Pasos siguientes

+ [Inicio rápido: Crear y ejecutar scripts de Python simples con SQL Server Machine Learning Services](../advanced-analytics/tutorials/quickstart-python-create-script.md)
+ [Inicio rápido: Crear y puntuar un modelo predictivo en Python con SQL Server Machine Learning Services](../advanced-analytics/tutorials/quickstart-python-train-score-model.md)
+ [Inicio rápido: Crear y ejecutar scripts de R sencillos con SQL Server Machine Learning Services](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Inicio rápido: Crear y puntuar un modelo predictivo en R con SQL Server Machine Learning Services](../advanced-analytics/tutorials/quickstart-r-train-score-model.md)
