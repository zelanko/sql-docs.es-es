---
title: La regulación de recursos para el aprendizaje automático en SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: abe130ef7e465326999e0c71ce01e88dfa6269a3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>Regulación de recursos para el aprendizaje automático en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo proporciona información general sobre la regulación de recursos de características de SQL Server que le ayudan a asignar y equilibrar los recursos usados por los scripts de R y Python.

**Se aplica a:** [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)]
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] y [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]

## <a name="goals-of-resource-governance-for-machine-learning"></a>Objetivos de la regulación de recursos para el aprendizaje automático

Una dificultad conocidos con lenguajes de aprendizaje de máquina como R y Python es que los datos a menudo se mueven fuera de la base de datos a equipos no controlados por TI. Other es que R es de subproceso único, lo que significa que sólo se puede trabajar con los datos disponibles en la memoria. 

Servicios de aprendizaje de máquina de SQL Server alivia estos dos problemas y ayuda a cumple los requisitos de cumplimiento de empresa. Mantiene análisis avanzado dentro de la base de datos y es compatible con un mayor rendimiento a través de grandes conjuntos de datos a través de características como la transmisión por secuencias y operaciones de fragmentación. Sin embargo, mover R y Python cálculos dentro de las bases de datos puede afectar al rendimiento de otros servicios que usan la base de datos, incluidas las consultas de usuario normal, las aplicaciones externas y los trabajos programados de la base de datos.

Esta sección proporciona información acerca de cómo puede administrar los recursos utilizados por los tiempos de ejecución externos, como R y Python, para mitigar el impacto en otros servicios de base de datos principal. Normalmente, un entorno de servidor de base de datos es el centro de varios servicios y aplicaciones dependientes.

Puede usar [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) para administrar los recursos utilizados por los tiempos de ejecución externo para R y Python.  Para el aprendizaje automático, el regulador de recursos implica estas tareas:

+ Identificar los scripts que usan demasiados recursos del servidor.
  
     El administrador debe poder terminar o limitar los trabajos que consumen demasiados recursos.
  
+ Mitigar las cargas de trabajo impredecibles.
  
     Por ejemplo, si varios trabajos de aprendizaje de máquina se ejecutan simultáneamente en el servidor, la contención de recursos resultante podría dar lugar a performance impredecible o amenazan la finalización de la carga de trabajo. Sin embargo, si se usan grupos de recursos, se pueden aislados entre sí los trabajos.
  
-   Dar prioridad a las cargas de trabajo.
  
     El administrador o el arquitecto debe ser capaz de especificar las cargas de trabajo que deben tienen prioridad o garantizar ciertas cargas de trabajo en completarse cuando hay contención de recursos.

## <a name="how-to-use-resource-governor-to-manage-machine-learning"></a>Cómo utilizar el regulador de recursos para administrar el aprendizaje automático
 
Administrar recursos asignados a las sesiones de R o Python mediante la creación de un *grupo de recursos externo*y la asignación de las cargas de trabajo para el grupo o grupos. Un grupo de recursos externo es un nuevo tipo de grupo de recursos que se introdujo en [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para ayudar a administrar el tiempo de ejecución de R y otros procesos externos al motor de base de datos.

SQL Server admite tres tipos de grupos de recursos de manera predeterminada: 
  
-   El *grupo interno* representa los recursos usados por SQL Server y no se puede modificar ni restringir.
  
-   El *grupo predeterminado* es un grupo de usuarios predefinido que se puede usar para modificar el uso de recursos para el servidor en su conjunto. También puede definir grupos de usuarios que pertenecen a este grupo para administrar el acceso a los recursos.
  
-   El *grupo externo predeterminado* es un grupo de usuarios predefinido para los recursos externos. Además, puede crear grupos de recursos externos y definir los grupos de usuarios que pertenecen a este grupo.
  
 También es posible crear *grupos de recursos definidos por el usuario* para asignar recursos al motor de base de datos o a otras aplicaciones y crear *grupos de recursos externos definidos por el usuario* para administrar R y otros procesos externos.
  
 Encontrará una buena introducción a la terminología y los conceptos generales en [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md) (Grupo de recursos del regulador de recursos).

  
## <a name="resource-management-walkthrough-with-resource-governor"></a>Tutorial de administración de recursos con el regulador de recursos

Si tiene experiencia en el regulador de recursos, vea este tema para obtener un tutorial rápido de cómo modificar los recursos de instancia predeterminada y crear un nuevo grupo de recursos externos: [crear un grupo de recursos de scripts externos](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)
  
 Puede usar el *grupo de recursos externo* mecanismo para administrar los recursos utilizados por los siguientes archivos ejecutables que se usan en aprendizaje automático:

+ Rterm.exe y procesos satélite
+ Procesos Python.exe y satélite
+ BxlServer.exe y procesos satélite
+ Procesos satélite iniciados Launchpad
  
> [!NOTE]
> 
> No se admite la administración directa del servicio Launchpad con el regulador de recursos. Eso se debe a que [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] es un servicio de confianza que por diseño solo puede hospedar los selectores proporcionados por Microsoft. Los iniciadores de confianza se configuran para evitar que se consuman demasiados recursos.
>   
> Se recomienda que administre los procesos satélite mediante el regulador de recursos y que los ajuste de modo que cumplan las necesidades de la carga de trabajo y la configuración de base de datos específicas.  Por ejemplo, se puede crear o destruir a petición cualquier proceso satélite individual durante la ejecución.
  
## <a name="disable-external-script-execution"></a>Deshabilitar la ejecución de scripts externos

La compatibilidad con scripts externos es opcional en la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Incluso después de instalar el características de aprendizaje automático, la capacidad para ejecutar scripts externos de forma predeterminada está desactivada, y debe volver a configurar la propiedad manualmente y reiniciar la instancia para habilitar la ejecución del script.

Por lo tanto, si se produce un problema de recursos que necesita para mitigar inmediatamente, o un problema de seguridad, un administrador puede inmediatamente deshabilitar cualquier ejecución de script externo mediante el uso de [sp_configure &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) y establecer la propiedad `external scripts enabled` en FALSE o 0.
  
## <a name="see-also"></a>Vea también

[Administración y supervisión de soluciones de aprendizaje automático](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

[Creación de grupos de recursos para el aprendizaje automático](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

[Grupos de recursos del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
