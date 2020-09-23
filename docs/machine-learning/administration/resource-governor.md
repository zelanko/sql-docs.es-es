---
title: Administración con Resource Governor
description: Obtenga información sobre cómo usar Resource Governor para administrar la asignación de recursos de CPU, E/S físicas y memoria para cargas de trabajo de Python y R en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 55fd9d7c699523856ad2623298c62d6f986904a5
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283556"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>Administración de cargas de trabajo de Python y R con Resource Governor en SQL Server Machine Learning Services
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Obtenga información sobre cómo usar [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para administrar la asignación de recursos de CPU, E/S físicas y memoria para cargas de trabajo de Python y R en SQL Server Machine Learning Services.

Los algoritmos de aprendizaje automático en Python y R usan una gran cantidad de recursos de proceso. Según sus prioridades de cargas de trabajo, puede que necesite incrementar o reducir los recursos disponibles para Machine Learning Services.

Para obtener información general, vea [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).

> [!NOTE] 
> Resource Governor es una característica de Enterprise Edition.

## <a name="default-allocations"></a>Asignaciones predeterminadas

De forma predeterminada, los tiempos de ejecución de scripts externos para aprendizaje automático están limitados a un máximo del 20 % del total de memoria de la máquina. Aunque depende del sistema, este límite suele ser inadecuado para tareas de aprendizaje automático importantes, como entrenar un modelo o realizar una predicción en varias filas de datos. 

## <a name="manage-resources-with-resource-governor"></a>Administración de recursos con Resource Governor
 
De forma predeterminada, los procesos externos usan hasta un 20 % del total de memoria del host en el servidor local. Puede modificar el grupo de recursos predeterminado para realizar cambios en todo el servidor, de forma que los procesos de R y Python usen la capacidad que configure como disponible para procesos externos.

Como opción, puede crear **grupos de recursos externos** personalizados, con clasificadores y grupos de cargas de trabajo asociados, para determinar la asignación de recursos de las solicitudes originadas desde programas o hosts específicos, o bien otros criterios que proporcione. Un grupo de recursos externos es un tipo de grupo de recursos introducido en [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para facilitar la administración de procesos de R y Python externos al motor de base de datos.

1. [Habilite la gobernanza de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (está desactivada de forma predeterminada).

2. Ejecute [CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) para crear y configurar el grupo de recursos, seguido de [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) para implementarlo.

3. Cree un grupo de cargas de trabajo para asignaciones granulares (por ejemplo, entre entrenamiento y puntuación).

4. Cree un clasificador para interceptar las llamadas de procesos externos.

5. Ejecute consultas y procedimientos con los objetos que ha creado.

Para ver un tutorial, consulte [Crear un grupo de recursos para SQL Server Machine Learning Services](create-external-resource-pool.md) para obtener instrucciones paso a paso.

Para obtener información general sobre la terminología y los conceptos generales, vea [Grupo de recursos de Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Procesos en gobernanza de recursos
  
 Puede usar un *grupo de recursos externos* para administrar los recursos usados por los siguientes ejecutables en una instancia del motor de la base de datos:

+ Rterm.exe, cuando se llama localmente desde SQL Server o de forma remota con SQL Server como el contexto de procesos remotos.
+ Python.exe, cuando se llama localmente desde SQL Server o de forma remota con SQL Server como el contexto de procesos remotos.
+ BxlServer.exe y procesos satélite
+ Procesos satélites iniciados por Launchpad, como PythonLauncher.dll
  
> [!NOTE]
> Aun así, no se admite la administración directa del servicio Launchpad mediante Resource Governor. Launchpad es un servicio de confianza que solo puede hospedar iniciadores proporcionados por Microsoft. Los iniciadores de confianza se configuran de manera explícita para evitar un uso excesivo de recursos.
  
## <a name="next-steps"></a>Pasos siguientes

+ [Creación de grupos de recursos para el aprendizaje automático](create-external-resource-pool.md)
+ [Grupos de recursos de Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
