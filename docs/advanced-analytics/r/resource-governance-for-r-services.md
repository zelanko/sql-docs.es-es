---
title: "Regulación de recursos para R Services | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5475c2258971c48c2e19bba69d9ec962ae48be87
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="resource-governance-for-r-services"></a>Regulación de recursos para R Services
  Uno de los problemas de R es que el análisis de grandes cantidades de datos en producción requiere hardware adicional, por lo que los datos suelen moverse fuera de la base de datos a equipos que el departamento de TI no controla.  Para realizar operaciones de análisis avanzadas, los clientes quieren aprovechar los recursos de servidor de base de datos y, para proteger sus datos, requieren que tales operaciones cumplan requisitos de cumplimiento empresarial, como la seguridad y el rendimiento.  
  
 En esta sección se proporciona información sobre cómo administrar los recursos usados por el tiempo de ejecución de R y por los trabajos de R en ejecución mediante la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como contexto de cálculo.  
  
## <a name="what-is-resource-governance"></a>¿Qué es la regulación de recursos?  
 La regulación de recursos está diseñada para identificar y evitar problemas comunes en un entorno de servidor de base de datos, donde a menudo hay varias aplicaciones dependientes y varios servicios que se deben admitir y equilibrar. Para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], la regulación de recursos conlleva estas tareas:  
  
-   Identificar los scripts que usan demasiados recursos del servidor.  
  
     El administrador debe poder terminar o limitar los trabajos que consumen demasiados recursos.  
  
-   Mitigar las cargas de trabajo impredecibles.  
  
     Por ejemplo, si varios trabajos de R se ejecutan simultáneamente en el servidor y los trabajos no están aislados entre sí mediante el uso de grupos de recursos, la contención de recursos resultante podría ocasionar un rendimiento impredecible o poner en peligro la finalización de la carga de trabajo.  
  
-   Dar prioridad a las cargas de trabajo.  
  
     El administrador o el arquitecto deben poder especificar las cargas de trabajo que tienen prioridad, o garantizar que ciertas cargas de trabajo se completarán si hay contención de recursos.  
  
 En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], puede usar el [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) para administrar los recursos usados por el tiempo de ejecución de R y por los trabajos de R remotos.  
  
## <a name="how-to-use-resource-governor-to-manage-r-jobs"></a>Cómo usar el regulador de recursos para administrar trabajos de R  
 En general, para administrar los recursos asignados a trabajos de R, se crean *grupos de recursos externos* y se asignan cargas de trabajo a los grupos. Un grupo de recursos externos es un nuevo tipo de grupo de recursos incluido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que ayuda a administrar el tiempo de ejecución de R y otros procesos fuera del motor de base de datos.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ahora hay tres tipos de grupos de recursos predeterminados.  
  
-   El *grupo interno* representa los recursos usados por SQL Server y no se puede modificar ni restringir.  
  
-   El *grupo predeterminado* es un grupo de usuarios predefinido que se puede usar para modificar el uso de recursos para el servidor en su conjunto. También puede definir grupos de usuarios que pertenecen a este grupo para administrar el acceso a los recursos.  
  
-   El *grupo externo predeterminado* es un grupo de usuarios predefinido para los recursos externos. Además, puede crear grupos de recursos externos y definir los grupos de usuarios que pertenecen a este grupo.  
  
 También es posible crear *grupos de recursos definidos por el usuario* para asignar recursos al motor de base de datos o a otras aplicaciones y crear *grupos de recursos externos definidos por el usuario* para administrar R y otros procesos externos.  
  
 Encontrará una buena introducción a la terminología y los conceptos generales en [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md) (Grupo de recursos del regulador de recursos).  

  
## <a name="resource-management-using-resource-governor"></a>Administración de recursos mediante el regulador de recursos 

   Si es la primera vez que usa el regulador de recursos, en este tema se incluye un tutorial rápido sobre cómo modificar los recursos predeterminados de instancia y crear un grupo de recursos externos: [Cómo crear un grupo de recursos para R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md).   
  
 Puede usar el mecanismo del *grupo de recursos externos* para administrar los recursos usados por los siguientes ejecutables de R:  
  
-   Rterm.exe y procesos satélite  
  
-   BxlServer.exe y procesos satélite  
  
-   Procesos satélite iniciados por Launchpad  
  
 Aun así, no se admite la administración directa del servicio Launchpad mediante el regulador de recursos. Eso se debe a que [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] es un servicio de confianza que por diseño solo puede hospedar los selectores proporcionados por Microsoft. Los selectores de confianza también están configurados para impedir que se consuman demasiados recursos.  
  
 Se recomienda que administre los procesos satélite mediante el regulador de recursos y que los ajuste de modo que cumplan las necesidades de la carga de trabajo y la configuración de base de datos específicas.  Por ejemplo, se puede crear o destruir a petición cualquier proceso satélite individual durante la ejecución.  
  
## <a name="disable-external-script-execution"></a>Deshabilitar la ejecución de scripts externos  
 La compatibilidad con scripts externos es opcional en la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Incluso después de instalar [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], la capacidad de ejecutar scripts externos está desactivada de forma predeterminada y debe volver a configurar manualmente la propiedad y reiniciar la instancia para habilitar la ejecución de scripts.  
  
 Por lo tanto, si se produce un problema de recursos que se debe resolver de inmediato o un problema de seguridad, un administrador puede deshabilitar al instante cualquier ejecución de scripts externos mediante [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) y el establecimiento de la propiedad `external scripts enabled` en FALSE o 0.  
  
## <a name="see-also"></a>Vea también  
 [Administración y supervisión de soluciones en R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [Cómo crear un grupo de recursos para R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [Grupo de recursos del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  


