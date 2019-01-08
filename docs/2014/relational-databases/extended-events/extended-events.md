---
title: Eventos extendidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485c748aad8b07a5e8b92a02c03d51a82e5f362a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354051"
---
# <a name="extended-events"></a>Eventos extendidos
  Los eventos extendidos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen una arquitectura muy escalable y configurable que permite a los usuarios recopilar la información justa y necesaria para solucionar o identificar un problema de rendimiento.  
  
 Puede buscar más información acerca de Extended Events en Internet, en [SQL Server Extended Events](https://blogs.msdn.com/b/extended_events/).  
  
## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>Ventajas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events  
 Extended Events es un sistema ligero de supervisión de rendimiento que usa muy pocos recursos de rendimiento. Los eventos extendidos proporcionan dos interfaces de usuario gráficas (**Asistente para nueva sesión** y **Nueva sesión**) para crear, modificar, mostrar y analizar los datos de la sesión.  
  
## <a name="extended-events-concepts"></a>Conceptos de Extended Events  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Los eventos extendidos se basan en conceptos existentes, como evento o consumidor de eventos, usa los conceptos de la traza de eventos para Windows y presenta nuevos conceptos.  
  
 En la tabla siguiente se describen los conceptos de Extended Events.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Paquetes de SQL Server Extended Events](sql-server-extended-events-packages.md)|Describe los paquetes de Extended Events que contienen objetos usados para obtener y procesar datos cuando se ejecuta una sesión de Extended Events.|  
|[Destinos de SQL Server Extended Events](../../database-engine/sql-server-extended-events-targets.md)|Describe los consumidores de eventos que pueden recibir datos durante una sesión de eventos.|  
|[Motor de SQL Server Extended Events](sql-server-extended-events-engine.md)|Describe el motor que implementa y administra una sesión de Extended Events.|  
|[Sesiones de SQL Server Extended Events](sql-server-extended-events-sessions.md)|Describe la sesión de eventos extendidos.|  
  
## <a name="extended-events-architecture"></a>Arquitectura de eventos extendidos  
 Los eventos extendidos constituyen un sistema de control de eventos general para los sistemas del servidor. La infraestructura de Extended Events admite la correlación de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y bajo ciertas condiciones, la correlación de datos de las aplicaciones de base de datos y sistema operativo. En este último caso, el resultado de eventos extendidos debe dirigirse al Seguimiento de eventos para Windows (ETW) para correlacionar los datos de evento con los datos de evento de la aplicación o del sistema operativo.  
  
 Todas las aplicaciones tienen puntos de ejecución que son útiles tanto dentro como fuera de una aplicación. Dentro de la aplicación, puede ponerse en cola el procesamiento asincrónico utilizando información recopilada durante la ejecución inicial de una tarea. Fuera de la aplicación, los puntos de ejecución proporcionan información a las utilidades de supervisión sobre las características de rendimiento y comportamiento de la aplicación supervisada.  
  
 Extended Events admite la utilización de datos de eventos fuera de un proceso. Normalmente, estos datos son utilizados por:  
  
-   Herramientas de seguimiento, como Monitor de sistema y Seguimiento de SQL.  
  
-   Herramientas de registro, como el registro de eventos de Windows o el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Usuarios que administran un producto o desarrollan aplicaciones de un producto.  
  
 Los aspectos clave del diseño de Extended Events son los siguientes:  
  
-   El motor de Extended Events es independiente del evento. Esto permite al motor enlazar cualquier evento con cualquier destino, ya que el motor no está limitado por el contenido del evento. Para obtener más información sobre el motor de Extended Events, vea [SQL Server Extended Events Engine](sql-server-extended-events-engine.md).  
  
-   Los eventos están separados de los consumidores de eventos, llamados *destinos* en Extended Events. Esto significa que cualquier destino puede recibir cualquier evento. Además, cualquier evento generado puede ser automáticamente utilizado por el destino, que puede registrar o proporcionar el contexto adicional del evento. Para obtener más información, vea [SQL Server Extended Events Targets](../../database-engine/sql-server-extended-events-targets.md).  
  
-   Los eventos son diferentes de la acción que se lleva a cabo cuando se produce un evento. Por lo tanto, puede asociarse cualquier acción a cualquier evento.  
  
-   Los predicados pueden filtrar dinámicamente cuándo se deben capturar los datos de evento. Esto se agrega a la flexibilidad de la infraestructura de eventos extendidos. Para obtener más información, vea [SQL Server Extended Events Packages](sql-server-extended-events-packages.md).  
  
 Extended Events puede generar datos de eventos de forma sincrónica (y procesar de forma asincrónica dichos datos) lo que proporciona una solución flexible para el control de eventos. Además, Extended Events proporciona las características siguientes:  
  
-   Un planteamiento unificado para controlar los eventos en todo el sistema de servidor, a la vez que habilita a los usuarios para aislar eventos específicos con el objeto de solucionar problemas.  
  
-   Integración y compatibilidad con las herramientas de ETW existentes.  
  
-   Un mecanismo completamente configurable de control de eventos basado en [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   La capacidad para supervisar dinámicamente los procesos activos, ejerciendo al mismo tiempo el mínimo efecto sobre dichos procesos.  
  
-   Una sesión de estado del sistema predeterminada que se ejecuta sin efectos apreciables en el rendimiento. La sesión recopila datos del sistema que se pueden utilizar para ayudar a solucionar problemas de rendimiento. Para obtener más información, vea [Usar la sesión system_health](use-the-ssms-xe-profiler.md).  
  
## <a name="extended-events-tasks"></a>Tareas de Extended Events  
 Si mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] ejecuta instrucciones de lenguaje de definición de datos (DDL) de [!INCLUDE[tsql](../../includes/tsql-md.md)] , funciones y vistas de administración dinámica, o vistas de catálogo, podrá crear soluciones sencillas o complejas de problemas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events para el entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Utilice el **Explorador de objetos** para administrar sesiones de eventos.|[Administrar sesiones de eventos en el Explorador de objetos](../../ssms/object/object-explorer.md)|  
|Describe cómo crear una sesión de Extended Events.|[Crear una sesión de eventos extendidos](../../database-engine/create-an-extended-events-session.md)|  
|Describe cómo ver y restaurar los datos de destino.|[Ver datos de sesiones de eventos](../../database-engine/view-event-session-data.md)|  
|Describe cómo usar las herramientas de Extended Events para crear administrar sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events.|[Herramientas de eventos extendidos](extended-events-tools.md)|  
|Describe cómo alterar una sesión de Extended Events.|[Modificar una sesión de eventos extendidos](alter-an-extended-events-session.md)|  
|Describe cómo copiar o exportar datos de destino.|[Copiar o exportar datos de destino](../../database-engine/copy-or-export-target-data.md)|  
|Describe cómo modificar la vista de los resultados de seguimiento para personalizar el modo en el que desea analizar los datos.|[Modificar la vista de resultados del seguimiento](../../database-engine/modify-the-trace-results-view.md)|  
|Describe cómo obtener información acerca de los campos asociados a los eventos.|[Obtener los campos de todos los eventos](../../database-engine/get-the-fields-for-all-events.md)|  
|Describe cómo determinar los eventos que están disponibles en los paquetes registrados.|[Ver los eventos de los paquetes registrados](../../database-engine/view-the-events-for-registered-packages.md)|  
|Describe cómo determinar los destinos de eventos extendidos que están disponibles en los paquetes registrados.|[Ver los destinos de eventos extendidos de los paquetes registrados](../../database-engine/view-the-extended-events-targets-for-registered-packages.md)|  
|Describe cómo ver los eventos y las acciones de los eventos extendidos que son equivalentes a cada evento de Seguimiento de SQL y sus columnas asociadas.|[Ver los eventos extendidos equivalentes a las clases de evento de Seguimiento de SQL](view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Describe cómo determinar los parámetros que puede establecer al usar el argumento ADD TARGET en CREATE EVENT SESSION o ALTER EVENT SESSION.|[Obtener los parámetros configurables del argumento ADD TARGET](../../database-engine/get-the-configurable-parameters-for-the-add-target-argument.md)|  
|Describe cómo convertir un script de Seguimiento de SQL existente en una sesión de eventos extendidos.|[Convertir un script de seguimiento de SQL existente en una sesión de eventos extendidos](convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Describe cómo determinar las consultas que mantienen el bloqueo, el plan de la consulta y la pila de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el momento en que se realizó el bloqueo.|[Determinar las consultas que retienen bloqueos](determine-which-queries-are-holding-locks.md)|  
|Describe cómo identificar el origen de los bloqueas que afectan al rendimiento de la base de datos.|[Buscar los objetos que han obtenido más bloqueos](find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Describe cómo usar los eventos extendidos con el seguimiento de eventos para Windows a fin de supervisar la actividad del sistema.|[Supervisar la actividad del sistema mediante eventos extendidos](monitor-system-activity-using-extended-events.md)|  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de capa de datos](../data-tier-applications/data-tier-applications.md)   
 [Compatibilidad de DAC con las versiones y objetos de SQL Server](../data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [Implementar una aplicación de capa de datos](../data-tier-applications/deploy-a-data-tier-application.md)   
 [Supervisar aplicaciones de capa de datos](../data-tier-applications/monitor-data-tier-applications.md)   
 [Vistas de administración dinámica de eventos extendidos](../views/views.md)   
 [Vistas de catálogo de eventos de extended &#40;Transact-SQL&#41;] (~/relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql  
  
  
