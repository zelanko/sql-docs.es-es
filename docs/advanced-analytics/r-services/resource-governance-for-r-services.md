---
title: "Regulador de recursos para servicios de R | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Regulador de recursos para servicios de R
  Una dificultad con R es que analizar grandes cantidades de datos de producción requiere hardware adicional y datos a menudo se mueven fuera de la base de datos a equipos no controlados por TI.  Para realizar operaciones de análisis avanzado, los clientes desean aprovechar los recursos de servidor de base de datos y para proteger sus datos, que requieren que tales operaciones cumplen los requisitos de cumplimiento de normas de nivel empresarial, como la seguridad y rendimiento.  
  
 Esta sección proporciona información acerca de cómo administrar los recursos utilizados por el tiempo de ejecución de R y trabajos de R que se ejecutan utilizando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia como el contexto del proceso.  
  
## ¿Qué es el regulador de recursos?  
 Regulador de recursos está diseñado para identificar y evitar los problemas que son comunes en un entorno de servidor de base de datos, donde a menudo hay varias aplicaciones dependientes y varios servicios para admitir y equilibrar. Para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], gobierno de recursos conlleva estas tareas:  
  
-   Identificación de los scripts que usan demasiados recursos del servidor.  
  
     El administrador debe poder terminar o limitar los trabajos que se consuman demasiados recursos.  
  
-   Mitigación de cargas de trabajo impredecibles.  
  
     Por ejemplo, si varios trabajos de R se ejecutan simultáneamente en el servidor y los trabajos no están aislados entre sí mediante el uso de grupos de recursos, la contención de recursos resultante puede ocasionar performance impredecible o amenazar la finalización de la carga de trabajo.  
  
-   Dar prioridad a las cargas de trabajo.  
  
     El administrador o el arquitecto debe ser capaz de especificar las cargas de trabajo que tienen prioridad, o garantizar ciertas cargas de trabajo para completar si hay contención de recursos.  
  
 En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], puede utilizar [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) para administrar los recursos utilizados por el runtime de R y trabajos de R remoto.  
  
## Trabajos de R administrar cómo para utilizar el regulador de recursos  
 En general, administra los recursos asignados a trabajos de R creando *grupos de recursos externos* y asignar las cargas de trabajo para el grupo o grupos. Un grupo de recursos externos es un nuevo tipo de grupo de recursos que se introdujo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], para ayudar a administrar el tiempo de ejecución de R y otros procesos externos al motor de base de datos.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ahora hay tres tipos de grupos de recursos predeterminado.  
  
-   El *grupo interno* representa los recursos utilizados por el propio SQL Server y no se modifica o restringidos.  
  
-   El *predeterminado grupo* es un grupo de usuarios predefinidos que puede utilizar para modificar el uso de recursos para el servidor como un todo. También puede definir grupos de usuarios que pertenecen a este grupo para administrar el acceso a los recursos.  
  
-   El *predeterminado grupo externo* es un grupo de usuarios predefinidos para recursos externos. Además, puede crear nuevos grupos de recursos externos y definir los grupos de usuario que pertenezca a este grupo.  
  
 Además, puede crear *grupos de recursos definidos por el usuario* para asignar recursos a otras aplicaciones o el motor de base de datos y crear *grupos de recursos externos definidos por el usuario* Administrar R y otros procesos externos.  
  
 Para obtener una introducción a la terminología y conceptos generales, consulte [grupo de recursos regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
> [!NOTE]  
>  Actualmente las nuevas propiedades del regulador de recursos están disponibles a través de instrucciones DDL o secuencias de comandos; no se puede crear grupos de recursos externos mediante la interfaz de usuario en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## Administración de recursos mediante el regulador de recursos 

   Si es nuevo en el regulador de recursos, vea este tema para obtener un tutorial rápido de cómo modificar los recursos predeterminados de instancia y crear un nuevo grupo de recursos externos:  [Cómo: crear un grupo de recursos para R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 Puede usar el *grupo de recursos externos* mecanismo para administrar los recursos utilizados por los archivos ejecutables de R siguientes:  
  
-   Procesos Rterm.exe y satélite  
  
-   Procesos BxlServer.exe y satélite  
  
-   Procesos de satélite iniciados por LaunchPad  
  
 Sin embargo, no se admite la administración directa del servicio Launchpad mediante el regulador de recursos. Eso es porque el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] es un servicio de confianza puede por diseño hospedar solo los iniciadores que proporcionan Microsoft. También se configuran los iniciadores de confianza para evitar que se consuman demasiados recursos.  
  
 Se recomienda que administrar procesos de satélite mediante el regulador de recursos y ajustarlos para satisfacer las necesidades de la configuración individual de la base de datos y la carga de trabajo.  Por ejemplo, cualquier proceso de satélite individuales puede ser creado o destruido a petición durante la ejecución.  
  
## Deshabilitar la ejecución del Script externo  
 Compatibilidad con scripts externos es opcional en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación. Incluso después de instalar [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], la capacidad para ejecutar scripts externos está desactivado de forma predeterminada y debe volver a configurar la propiedad manualmente y reiniciar la instancia para habilitar la ejecución del script.  
  
 Por lo tanto, si hay un problema de recursos que necesita mitigar inmediatamente o un problema de seguridad, un administrador puede inmediatamente deshabilitar cualquier ejecución de script externo mediante [sp_configure & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) y establecer la propiedad `external scripts enabled` en FALSE o 0.  
  
## Vea también  
 [Administración y supervisión de soluciones en R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [Cómo: Crear un grupo de recursos para R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  