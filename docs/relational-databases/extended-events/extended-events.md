---
title: 'Información general de XEvents: SQL Server'
description: La arquitectura de eventos extendidos de SQL Server le permite recopilar los datos necesarios para identificar y solucionar problemas de rendimiento. Se puede configurar y escalar.
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: overview
helpviewer_keywords:
- extended events [SQL Server]
- xe
- XEvents
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fdca475c71f2f1b81dac9b2a37850cea697a4414
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727343"
---
# <a name="extended-events-overview"></a>Introducción a los eventos extendidos

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La arquitectura de Eventos extendidos permite a los usuarios recopilar tantos datos como sea necesario para solucionar o identificar un problema de rendimiento. Eventos extendidos es configurable y ofrece una muy buena escalabilidad.

Encontrará más información sobre Eventos extendidos en [Inicio rápido: eventos extendidos en SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md).

## <a name="benefits-of-ssnoversion-extended-events"></a>Ventajas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events  

Eventos extendidos es un sistema ligero de supervisión de rendimiento que usa una cantidad mínima de recursos de rendimiento. Eventos extendidos proporciona dos interfaces de usuario gráficas para crear, modificar, mostrar y analizar los datos de la sesión. Estas interfaces se denominan:

- Asistente para nueva sesión
- Nueva sesión

## <a name="extended-events-concepts"></a>Conceptos de Extended Events  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Eventos extendidos se basa en conceptos existentes, como un evento o consumidor de eventos, usa los conceptos de Seguimiento de eventos para Windows y presenta nuevos conceptos.  
  
 En la tabla siguiente se describen los conceptos de Extended Events.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Paquetes de SQL Server Extended Events](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|Describe los paquetes de Eventos extendidos que contienen objetos. Estos objetos se usan para obtener y procesar datos cuando se está ejecutando una sesión de Eventos extendidos.|  
|[Destinos de SQL Server Extended Events](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)|Describe los consumidores de eventos que pueden recibir datos durante una sesión de eventos.|  
|[Motor de SQL Server Extended Events](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|Describe el motor que implementa y administra una sesión de Extended Events.|  
|[Sesiones de SQL Server Extended Events](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|Describe la sesión de eventos extendidos.|  
| &nbsp; | &nbsp; |
  
## <a name="extended-events-architecture"></a>Arquitectura de eventos extendidos  

Eventos extendidos es el nombre con el que denominamos a un sistema general de control de eventos para los sistemas del servidor. La infraestructura de Extended Events admite la correlación de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y bajo ciertas condiciones, la correlación de datos de las aplicaciones de base de datos y sistema operativo. En el caso del sistema operativo, la salida de Eventos extendidos debe dirigirse a Seguimiento de eventos para Windows (ETW). ETW se usa para establecer correlaciones entre los datos de eventos y los datos de eventos de la aplicación o del sistema operativo.  

Todas las aplicaciones tienen puntos de ejecución que son útiles tanto dentro como fuera de una aplicación. Dentro de la aplicación, puede ponerse en cola el procesamiento asincrónico utilizando información recopilada durante la ejecución inicial de una tarea. Fuera de la aplicación, los puntos de ejecución proporcionan utilidades de supervisión con información. La información está relacionada con las características de rendimiento y comportamiento de la aplicación supervisada.  

 Extended Events admite la utilización de datos de eventos fuera de un proceso. Normalmente, estos datos son utilizados por:  
  
-   Herramientas de seguimiento, como Monitor de sistema y Seguimiento de SQL.  
  
-   Herramientas de registro, como el registro de eventos de Windows o el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Usuarios que administran un producto o desarrollan aplicaciones de un producto.  
  
 Los aspectos clave del diseño de Extended Events son los siguientes:  
  
-   El motor de Extended Events es independiente del evento. El motor puede enlazar cualquier evento con cualquier destino, ya que el motor no está limitado por el contenido del evento. Para obtener más información sobre el motor de Extended Events, vea [SQL Server Extended Events Engine](../../relational-databases/extended-events/sql-server-extended-events-engine.md).  
  
-   Los eventos están separados de los consumidores de eventos, llamados *destinos* en Extended Events. Esto significa que cualquier destino puede recibir cualquier evento. Además, cualquier evento generado puede ser automáticamente utilizado por el destino, que puede registrar o proporcionar el contexto adicional del evento. Para más información, consulte [SQL Server Extended Events Targets](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).  
  
-   Los eventos son diferentes de la acción que se lleva a cabo cuando se produce un evento. Por lo tanto, puede asociarse cualquier acción a cualquier evento.  
  
-   Los predicados pueden filtrar dinámicamente cuándo se deben capturar los datos de evento. El filtrado dinámico se suma a la flexibilidad de la infraestructura de Eventos extendidos. Para obtener más información, vea [SQL Server Extended Events Packages](../../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
 Extended Events puede generar datos de eventos de forma sincrónica (y procesar de forma asincrónica dichos datos) lo que proporciona una solución flexible para el control de eventos. Además, Extended Events proporciona las características siguientes:  
  
-   Un planteamiento unificado para controlar los eventos en todo el sistema de servidor, a la vez que habilita a los usuarios para aislar eventos específicos con el objeto de solucionar problemas.  
  
-   Integración y compatibilidad con las herramientas de ETW existentes.  
  
-   Un mecanismo completamente configurable de control de eventos basado en [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   La capacidad para supervisar dinámicamente los procesos activos, ejerciendo al mismo tiempo el mínimo efecto sobre dichos procesos.  
  
-   Una sesión de estado del sistema predeterminada que se ejecuta sin efectos apreciables en el rendimiento. La sesión recopila datos del sistema que se pueden utilizar para ayudar a solucionar problemas de rendimiento. Para obtener más información, vea [Usar la sesión system_health](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## <a name="extended-events-tasks"></a>Tareas de Extended Events  

Si mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] ejecuta instrucciones de lenguaje de definición de datos (DDL) de [!INCLUDE[tsql](../../includes/tsql-md.md)] , funciones y vistas de administración dinámica, o vistas de catálogo, podrá crear soluciones sencillas o complejas de problemas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events para el entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Utilice el **Explorador de objetos** para administrar sesiones de eventos.|[Administrar sesiones de eventos en el Explorador de objetos](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|Describe cómo crear una sesión de Extended Events.|[Crear una sesión de eventos extendidos](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)|  
|Describe cómo ver y restaurar los datos de destino.| [Visualización avanzada de datos de destino de eventos extendidos en SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|Describe cómo usar las herramientas de Extended Events para crear administrar sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events.|[Herramientas de eventos extendidos](../../relational-databases/extended-events/extended-events-tools.md)|  
|Describe cómo alterar una sesión de Extended Events.|[Modificar una sesión de eventos extendidos](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|Describe cómo obtener información acerca de los campos asociados a los eventos.|[Obtener los campos de todos los eventos](https://msdn.microsoft.com/library/4e4ee03f-5bca-42ed-a37c-db1c82e3aad2)|  
|Describe cómo determinar los eventos que están disponibles en los paquetes registrados.|[Ver los eventos de los paquetes registrados](https://msdn.microsoft.com/library/9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f)|  
|Describe cómo determinar los destinos de eventos extendidos que están disponibles en los paquetes registrados.|[Ver los destinos de eventos extendidos de los paquetes registrados](https://msdn.microsoft.com/library/4985aa5f-ac99-49f6-852c-9d25916549e9)|  
|Describe cómo ver los eventos y las acciones de los eventos extendidos que son equivalentes a cada evento de Seguimiento de SQL y sus columnas asociadas.|[Ver los eventos extendidos equivalentes a las clases de evento de Seguimiento de SQL](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Describe cómo determinar los parámetros que puede establecer al usar el argumento ADD TARGET en CREATE EVENT SESSION o ALTER EVENT SESSION.|[Obtener los parámetros configurables del argumento ADD TARGET](https://msdn.microsoft.com/library/08454543-c5c8-4ca3-9af9-f1d82264471c)|  
|Describe cómo convertir un script de Seguimiento de SQL existente en una sesión de eventos extendidos.|[Convertir un script de seguimiento de SQL existente en una sesión de eventos extendidos](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Describe cómo determinar las consultas que mantienen el bloqueo, el plan de la consulta y la pila de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el momento en que se realizó el bloqueo.|[Determinar las consultas que retienen bloqueos](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|Describe cómo identificar el origen de los bloqueas que afectan al rendimiento de la base de datos.|[Buscar los objetos que han obtenido más bloqueos](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Describe cómo usar los eventos extendidos con el seguimiento de eventos para Windows a fin de supervisar la actividad del sistema.|[Supervisar la actividad del sistema mediante eventos extendidos](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
|Usar las vistas de catálogo y las vistas de administración dinámica (DMV) para eventos extendidos | [Instrucciones SELECT y JOIN en vistas del sistema para eventos extendidos en SQL Server](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |
| &nbsp; | &nbsp; |

Use la consulta siguiente de Transact-SQL (T-SQL) para enumerar todos los posibles eventos extendidos y sus descripciones:

```sql
SELECT
     obj1.name as [XEvent-name],
     col2.name as [XEvent-column],
     obj1.description as [Descr-name],
     col2.description as [Descr-column]
  FROM
               sys.dm_xe_objects        as obj1
      JOIN sys.dm_xe_object_columns as col2 on col2.object_name = obj1.name
  ORDER BY
    obj1.name,
    col2.name
```


## <a name="code-examples-can-differ-for-azure-sql-database"></a>Ejemplos de código que pueden diferir de Azure SQL Database

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="see-also"></a>Consulte también

[Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)  
[Compatibilidad de DAC con las versiones y objetos de SQL Server](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)  
[Implementar una aplicación de capa de datos](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
[Supervisar aplicaciones de capa de datos](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)  
&nbsp;  
[Vistas de administración dinámica de eventos extendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)  
[Vistas de catálogo de eventos extendidos (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
&nbsp;  
[XELite: biblioteca multiplataforma para leer XEvents de archivos XEL o secuencias en directo de SQL](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/); publicada en mayo de 2019.  
[Read-SQLXEvent PowerShell cmdlet](https://www.powershellgallery.com/packages/SqlServer.XEvent), publicado en junio de 2019.  
[Misterios de SQL: Seguimiento de causalidad frente a secuencia de eventos para sesiones de XEvent (blog publicado el 1 de abril de 2019)](https://bobsql.com/sql-mysteries-causality-tracking-vs-event-sequence-for-xevent-sessions/)  
