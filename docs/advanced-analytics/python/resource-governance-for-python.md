---
title: Regulador de recursos para Python | Documentos de Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f83d62804803b2b9f3f028c48a7ec23d3f8d910
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="resource-governance-for-python"></a>Regulador de recursos para Python

Porque Python se habilita a través de la la misma arquitectura de extensibilidad que se implementó para el lenguaje R en SQL Server 2016, puede utilizar las herramientas existentes en SQL Server, como el regulador de recursos y DMV, eventos extendidos, para supervisar la ejecución de Python scripts de SQL Server.

La regulación de recursos en concreto es importante porque analizar grandes cantidades de datos de producción puede consumir muchos hardware incluso avanzada.  Para evitar que los datos se mueve fuera de la base de datos a los equipos que no puedan administrados o auditar, es importante que el Administrador de base de datos asignar suficientes recursos para las operaciones de análisis avanzado.

Esta sección proporciona información acerca de cómo puede administrar los recursos utilizados por el tiempo de ejecución de Python y supervisar el uso de los recursos Python scripts de trabajos que se ejecutan en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.

> [!NOTE]
> Compatibilidad con Python es una característica nueva de SQL Server 2017 y está en versión preliminar. Busque información más pronto.
> En general, puede supervisar los scripts externos, incluida una que se ejecutase Python, utilizando el mismo marco de trabajo que se proporcionó para la regulación de recursos de scripts de R en SQL Server 2016.

## <a name="what-is-resource-governance"></a>¿Qué es la regulación de recursos?

La regulación de recursos está diseñada para identificar y evitar problemas comunes en un entorno de servidor de base de datos, donde a menudo hay varias aplicaciones dependientes y varios servicios que se deben admitir y equilibrar. Para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], la regulación de recursos conlleva estas tareas:  

+ **Identificación de los scripts que usan recursos del servidor excesivo**. El administrador debe poder terminar o limitar los trabajos que consumen demasiados recursos.

+ **Mitigación de cargas de trabajo impredecibles**. Si varios trabajos de Python se ejecutan simultáneamente en el servidor y los trabajos no están aislados entre sí mediante el uso de grupos de recursos, la contención de recursos resultante podría dar lugar a performance impredecible o amenazan la finalización de la carga de trabajo.

+ **Dar prioridad a las cargas de trabajo**. El administrador o el arquitecto deben poder especificar las cargas de trabajo que tienen prioridad, o garantizar que ciertas cargas de trabajo se completarán si hay contención de recursos.

Puede usar [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) para administrar los recursos utilizados por los tiempos de ejecución externo. Esto incluye scripts de Python que se inician desde un equipo remoto terminal pero ejecutada con el equipo de SQL Server como el contexto de proceso.

> [!NOTE] 
> Regulador de recursos está disponible en Enterprise Edition.

## <a name="how-to-use-resource-governor-to-manage-python-execution"></a>Cómo usar el regulador de recursos para administrar la ejecución de Python

En general, administrar recursos asignados a ningún trabajo de script externo mediante la creación de un *grupo de recursos externo* y la asignación de las cargas de trabajo para el grupo. Un grupo de recursos externo es un nuevo tipo de grupo de recursos que se introdujo en SQL Server 2016, para ayudar a administrar el tiempo de ejecución de R y otros procesos externos al motor de base de datos. Se puede utilizar para supervisar trabajos de Python a partir de SQL Server 2017.

Hay tres tipos de grupos de recursos de manera predeterminada:

+ El *grupo interno* representa los recursos usados por SQL Server y no se puede modificar ni restringir.
+ El *grupo predeterminado* es un grupo de usuarios predefinido que se puede usar para modificar el uso de recursos para el servidor en su conjunto. También puede definir grupos de usuarios que pertenecen a este grupo para administrar el acceso a los recursos.
+ El *grupo externo predeterminado* es un grupo de usuarios predefinido para los recursos externos. Además, puede crear grupos de recursos externos y definir los grupos de usuarios que pertenecen a este grupo.

También es posible crear *grupos de recursos definidos por el usuario* para asignar recursos al motor de base de datos o a otras aplicaciones y crear *grupos de recursos externos definidos por el usuario* para administrar R y otros procesos externos.

Encontrará una buena introducción a la terminología y los conceptos generales en [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md) (Grupo de recursos del regulador de recursos).

## <a name="resource-management-using-resource-governor"></a>Administración de recursos mediante el regulador de recursos

Si es la primera vez que usa el regulador de recursos, en este tema se incluye un tutorial rápido sobre cómo modificar los recursos predeterminados de instancia y crear un grupo de recursos externos: [Cómo crear un grupo de recursos para R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md).

Puede usar el *grupo de recursos externo* mecanismo para administrar los recursos utilizados por los ejecutables admitidos siguientes:

+ Python35.exe cuando se llama desde SQL Server o se debe llamar de forma remota con SQL Server como el contexto de proceso remoto.
+ BxlServer.exe y procesos satélite
+ Iniciadores de iniciado por Launchpad, como PythonLauncher.dll

> [!NOTE]
> No se admite la administración directa del servicio Launchpad con el regulador de recursos. Eso se debe a que [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] es un servicio de confianza que por diseño solo puede hospedar los selectores proporcionados por Microsoft. Los selectores de confianza también están configurados para impedir que se consuman demasiados recursos.

Se recomienda que administre los procesos satélite mediante el regulador de recursos y que los ajuste de modo que cumplan las necesidades de la carga de trabajo y la configuración de base de datos específicas.  Por ejemplo, se puede crear o destruir a petición cualquier proceso satélite individual durante la ejecución.

## <a name="disable-or-enable-external-script-execution"></a>Deshabilitar o habilitar la ejecución de scripts externos

Compatibilidad con scripts externos es opcional en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación e incluso después de que el programa de instalación es la ejecución de secuencia de comandos completa, externo está establecida en OFF de forma predeterminada por motivos de seguridad. Por lo tanto, después de haber completado la instalación de uno de los idiomas y los servicios relacionados de aprendizaje automático, debe configurar de forma explícita la instancia y, a continuación, reinicie el servicio de motor de base de datos.

En el caso de las secuencias de comandos descontroladas, puede deshabilitar toda la ejecución del script. Simplemente invertir este proceso, y volver a establecer la propiedad `external scripts enabled` en FALSE ó 0, en la instancia. Esto deshabilitará inmediatamente cualquier ejecución de scripts externos. Debe reservar esta opción para los problemas de seguridad, o en situaciones en que un administrador necesita mitigar los problemas de recursos inmediatamente.

## <a name="see-also"></a>Vea también

[Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)


