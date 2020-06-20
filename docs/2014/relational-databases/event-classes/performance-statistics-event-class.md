---
title: Performance Statistics, clase de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Performance Statistics event class
ms.assetid: da9cd2c4-6fdd-4ada-b74f-105e3541393c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8fc22c4af9980eb5c1c365c0ce2d0e2f6c8462e1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85029003"
---
# <a name="performance-statistics-event-class"></a>Performance Statistics, clase de eventos
  La clase de eventos Performance Statistics se puede utilizar para supervisar el rendimiento de las consultas, los procedimientos almacenados y los desencadenadores que se están ejecutando. Cada una de las seis subclases de evento indica un evento en la vigencia de las consultas, los procedimientos almacenados y los desencadenadores dentro del sistema. Si usa la combinación de estas subclases de evento y las vistas de administración dinámica asociadas sys.dm_exec_query_stats, sys.dm_exec_procedure_stats y sys.dm_exec_trigger_stats, puede reconstituir el historial de rendimiento de cualquier consulta, procedimiento almacenado o desencadenador dados.  
  
## <a name="performance-statistics-event-class-data-columns"></a>Columnas de datos de la clase de evento Performance Statistics  
 Las tablas siguientes describen las columnas de datos de clase de eventos con cada una de las siguientes subclases de evento: EventSubClass 0, EventSubClass 1, EventSubClass 2, EventSubClass 3, EventSubClass 4 y EventSubClass 5.  
  
### <a name="eventsubclass-0"></a>EventSubClass 0  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|NULL|52|Yes|  
|BinaryData|`image`|NULL|2|Yes|  
|DatabaseID|`int`|IDENTIFICADOR de la base de datos especificada por la instrucción USE *Database* o la base de datos predeterminada si no se ha emitido ninguna instrucción use *Database* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 0 = Nuevo texto SQL del lote que no está presente actualmente en la caché.<br /><br /> Los siguientes tipos de EventSubClass se generan en el seguimiento para lotes ad hoc.<br /><br /> Para lotes ad hoc con *n* consultas:<br /><br /> 1 de tipo 0|21|Yes|  
|IntegerData2|`int`|NULL|55|Yes|  
|ObjectID|`int`|NULL|22|Sí|  
|Offset|`int`|NULL|61|Yes|  
|PlanHandle|`Image`|NULL|65|Yes|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Yes|  
|SqlHandle|`image`|Identificador SQL que se puede utilizar para obtener el texto SQL del lote mediante la vista de administración dinámica sys.dm_exec_sql_text.|63|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Yes|  
|TextData|`ntext`|Texto SQL del lote.|1|Yes|  
  
### <a name="eventsubclass-1"></a>EventSubClass 1  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|Número acumulado de veces que este plan se ha vuelto a compilar.|52|Yes|  
|BinaryData|`image`|XML binario del plan compilado.|2|Sí|  
|DatabaseID|`int`|IDENTIFICADOR de la base de datos especificada por la instrucción USE *Database* o la base de datos predeterminada si no se ha emitido ninguna instrucción use *Database* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 1 = Las consultas en un procedimiento almacenado se han compilado.<br /><br /> Los siguientes tipos de EventSubClass se generan en el seguimiento para procedimientos almacenados.<br /><br /> Para procedimientos almacenados con *n* consultas:<br /><br /> *n* de tipo 1|21|Yes|  
|IntegerData2|`int`|Final de la instrucción dentro del procedimiento almacenado.<br /><br /> -1 para el final del procedimiento almacenado.|55|Yes|  
|ObjectID|`int`|Identificador del objeto asignado por el sistema.|22|Yes|  
|Offset|`int`|Desplazamiento inicial de la instrucción en el procedimiento almacenado o lote.|61|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Yes|  
|SqlHandle|`image`|Identificador SQL que se puede utilizar para obtener el texto SQL del procedimiento almacenado mediante la vista de administración dinámica dm_exec_sql_text.|63|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Yes|  
|TextData|`ntext`|NULL|1|Yes|  
|PlanHandle|`image`|Identificador del plan compilado para el procedimiento almacenado. Se puede usar para obtener el plan XML mediante la vista de administración dinámica sys.dm_exec_query_plan.|65|Yes|  
|ObjectType|`int`|Valor que representa el tipo de objeto incluido en el evento.<br /><br /> 8272 = procedimiento almacenado|28|Yes|  
|BigintData2|`bigint`|Memoria total, en kilobytes, utilizada durante la compilación.|53|Yes|  
|CPU|`int`|Tiempo total de CPU, en milisegundos, transcurrido durante la compilación.|18|Sí|  
|Duration|`int`|Tiempo total transcurrido durante la compilación (en microsegundos).|13|Sí|  
|IntegerData|`int`|Tamaño, en kilobytes, del plan compilado.|25|Yes|  
  
### <a name="eventsubclass-2"></a>EventSubClass 2  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|Número acumulado de veces que este plan se ha vuelto a compilar.|52|Yes|  
|BinaryData|`image`|XML binario del plan compilado.|2|Yes|  
|DatabaseID|`int`|IDENTIFICADOR de la base de datos especificada por la instrucción USE *Database* o la base de datos predeterminada si no se ha emitido ninguna instrucción use *Database* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 2 = Las consultas en una instrucción SQL ad hoc se han compilado.<br /><br /> Los siguientes tipos de EventSubClass se generan en el seguimiento para lotes ad hoc.<br /><br /> Para lotes ad hoc con *n* consultas:<br /><br /> número*n* de tipo 2|21|Yes|  
|IntegerData2|`int`|Final de la instrucción dentro del lote.<br /><br /> -1 para el final del lote.|55|Yes|  
|ObjectID|`int`|N/D|22|Yes|  
|Offset|`int`|Desplazamiento inicial de la instrucción dentro del lote.<br /><br /> 0 para el comienzo del lote.|61|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|SqlHandle|`image`|Identificador SQL. Se puede utilizar para obtener el texto SQL del lote mediante la vista de administración dinámica dm_exec_sql_text.|63|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Yes|  
|TextData|`ntext`|NULL|1|Yes|  
|PlanHandle|`image`|Identificador del plan compilado para el lote. Se puede usar para obtener el plan XML del lote mediante la vista de administración dinámica dm_exec_query_plan.|65|Yes|  
|BigintData2|`bigint`|Memoria total, en kilobytes, utilizada durante la compilación.|53|Yes|  
|CPU|`int`|Tiempo total de CPU, en microsegundos, transcurrido durante la compilación.|18|Sí|  
|Duration|`int`|Tiempo total transcurrido durante la compilación (en milisegundos).|13|Yes|  
|IntegerData|`int`|Tamaño, en kilobytes, del plan compilado.|25|Yes|  
  
### <a name="eventsubclass-3"></a>EventSubClass 3  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|Número acumulado de veces que este plan se ha vuelto a compilar.|52|Yes|  
|BinaryData|`image`|NULL|2|Yes|  
|DatabaseID|`int`|IDENTIFICADOR de la base de datos especificada por la instrucción USE *Database* o la base de datos predeterminada si no se ha emitido ninguna instrucción use *Database* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 3 = Se ha destruido una consulta almacenada en caché y los datos históricos de rendimiento asociados al plan están a punto de ser destruidos.<br /><br /> Los siguientes tipos de EventSubClass se generan en el seguimiento.<br /><br /> Para lotes ad hoc con *n* consultas:<br /><br /> 1 de tipo 3 cuando la consulta se vacíe de la caché.<br /><br /> Para procedimientos almacenados con *n* consultas:<br />1 de tipo 3 cuando la consulta se vacía de la caché.|21|Yes|  
|IntegerData2|`int`|Final de la instrucción en el procedimiento almacenado o lote.<br /><br /> -1 para el final del lote o procedimiento almacenado.|55|Yes|  
|ObjectID|`int`|NULL|22|Yes|  
|Offset|`int`|Desplazamiento inicial de la instrucción en el procedimiento almacenado o lote.<br /><br /> 0 para el comienzo del lote o procedimiento almacenado.|61|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Yes|  
|SqlHandle|`image`|Identificador SQL que se puede utilizar para obtener el texto SQL del lote o procedimiento almacenado mediante la vista de administración dinámica dm_exec_sql_text.|63|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Yes|  
|TextData|`ntext`|QueryExecutionStats|1|Yes|  
|PlanHandle|`image`|Identificador del plan compilado para el lote o procedimiento almacenado. Se puede usar para obtener el plan XML mediante la vista de administración dinámica dm_exec_query_plan.|65|Yes|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
  
### <a name="eventsubclass-4"></a>EventSubClass 4  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|NULL|52|Yes|  
|BinaryData|`image`|NULL|2|Yes|  
|DatabaseID|`int`|Identificador de la base de datos en la que reside el procedimiento almacenado dado.|3|Sí|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Yes|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 4 = un procedimiento almacenado en memoria caché se ha quitado de la caché y los datos de rendimiento históricos asociados a él están a punto de ser destruidos.|21|Yes|  
|IntegerData2|`int`|NULL|55|Yes|  
|ObjectID|`int`|Identificador del procedimiento almacenado. Equivale a la columna object_id en sys.procedures.|22|Sí|  
|Offset|`int`|NULL|61|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|SqlHandle|`image`|Identificador SQL que se puede utilizar para obtener el texto SQL del procedimiento almacenado que se ejecutó mediante la vista de administración dinámica dm_exec_sql_text.|63|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Yes|  
|TextData|`ntext`|ProcedureExecutionStats|1|Yes|  
|PlanHandle|`image`|Identificador del plan compilado para el procedimiento almacenado. Se puede usar para obtener el plan XML mediante la vista de administración dinámica dm_exec_query_plan.|65|Yes|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
  
### <a name="eventsubclass-5"></a>EventSubClass 5  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|`bigint`|NULL|52|Yes|  
|BinaryData|`image`|NULL|2|Yes|  
|DatabaseID|`int`|Identificador de la base de datos en la que reside el desencadenador dado.|3|Yes|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 5 = un desencadenador almacenado en memoria caché se ha quitado de la caché y los datos de rendimiento históricos asociados a él están a punto de ser destruidos.|21|Yes|  
|IntegerData2|`int`|NULL|55|Yes|  
|ObjectID|`int`|Identificador del desencadenador. Equivale a la columna object_id en las vistas de catálogo sys.triggers/sys.server_triggers.|22|Sí|  
|Offset|`int`|NULL|61|Yes|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|SqlHandle|`image`|Identificador SQL que se puede utilizar para obtener el texto SQL del desencadenador mediante la vista de administración dinámica dm_exec_sql_text.|63|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Yes|  
|TextData|`ntext`|TriggerExecutionStats|1|Yes|  
|PlanHandle|`image`|Identificador del plan compilado para el desencadenador. Se puede usar para obtener el plan XML mediante la vista de administración dinámica dm_exec_query_plan.|65|Yes|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [SHOWPLAN XML for Query compile (clase de eventos)](showplan-xml-for-query-compile-event-class.md)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](../views/views.md)  
  
  
