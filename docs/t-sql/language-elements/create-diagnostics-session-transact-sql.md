---
title: "Crear sesión de diagnóstico (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71f3463ad4d91bd117c322e9e63c0b331b07ca9f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-diagnostics-session-transact-sql"></a>Crear sesión de diagnóstico (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Las sesiones de diagnóstico le permiten guardar información de diagnóstico detallada, definido por el usuario, en el rendimiento del sistema o la consulta.  
  
 Las sesiones de diagnóstico se usan normalmente para depurar el rendimiento de una consulta específica o para supervisar el comportamiento de un componente específico del dispositivo durante la operación de dispositivo.  
  
> [!NOTE]  
>  Debe estar familiarizado con XML para poder utilizar las sesiones de diagnóstico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N’{<session_xml>}’;  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name=”event_name”/>  
         [ <Where>\<filter_property_name Name=”value” ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name=”property_name”/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
## <a name="arguments"></a>Argumentos  
 *diagnostics_name*  
 El nombre de la sesión de diagnóstico. Nombres de la sesión de diagnóstico pueden incluir caracteres a-z, A-z y 0-9 solo. Además, los nombres de la sesión de diagnóstico deben empezar por un carácter. *diagnostics_name* está limitada a 127 caracteres.  
  
 *max_item_count_num*  
 El número de eventos debe conservarse en una vista. Por ejemplo, si se especifica 100, 100 eventos más recientes que cumpla los criterios de filtro se conservará en la sesión de diagnóstico. Si se detectan menos de 100 encontrar coincidencias con eventos, la sesión de diagnóstico contiene menos de 100 eventos. *max_item_count_num* debe ser al menos 100 y menor o igual a 100 000.  
  
 *event_name*  
 Define los eventos reales que se recopilan en la sesión de diagnóstico.  *event_name* es uno de los eventos enumerados en [sys.pdw_diag_events](http://msdn.microsoft.com/en-us/d813aac0-cea1-4f53-b8e8-d26824bc2587) donde `sys.pdw_diag_events.is_enabled='True'`.  
  
 *filter_property_name*  
 El nombre de la propiedad en la que se va a restringir los resultados. Por ejemplo, si desea limitar según el identificador de sesión, *filter_property_name* debe ser *SessionId*. Vea *property_name* a continuación para obtener una lista de posibles valores para *filter_property_name*.  
  
 *value*  
 Un valor para evaluar con respecto a *filter_property_name*. El tipo de valor debe coincidir con el tipo de propiedad. Por ejemplo, si el tipo de propiedad es decimal, el tipo de *valor* debe ser decimal.  
  
 *comp_type*  
 El tipo de comparación. Posibles valores son: es igual a, EqualsOrGreaterThan, EqualsOrLessThan, GreaterThan, LessThan, valores, Contains, RegEx  
  
 *property_name*  
 Una propiedad relacionada con el evento.  Nombres de propiedad pueden formar parte de la etiqueta de captura, o utilizan como parte de criterios de filtrado.  
  
|Nombre de propiedad|Description|  
|-------------------|-----------------|  
|UserName|Un nombre de usuario (inicio de sesión).|  
|SessionId|Un identificador de sesión.|  
|QueryId|Un identificador de la consulta.|  
|CommandType|Un tipo de comando.|  
|CommandText|Texto dentro de un comando procesar.|  
|OperationType|El tipo de operación para el evento.|  
|Duración|La duración del evento.|  
|SPID|El identificador de proceso del servicio.|  
  
## <a name="remarks"></a>Comentarios  
 Cada usuario se permite un máximo de 10 sesiones simultáneas de diagnóstico. Vea [sys.pdw_diag_sessions](http://msdn.microsoft.com/en-us/ca111ddc-2787-4205-baf0-1a242c0257a9) para obtener una lista de las sesiones actuales y colocar cualquiera que ya no necesite sesiones mediante `DROP DIAGNOSTICS SESSION`.  
  
 Las sesiones de diagnóstico continuarán recopilar metadatos hasta que se quita.  
  
## <a name="permissions"></a>Permissions  
 Requiere la **ALTER SERVER STATE** permiso.  
  
## <a name="locking"></a>Bloqueo  
 Tiene un bloqueo compartido en la tabla de sesiones de diagnóstico.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-diagnostics-session"></a>A. Crear una sesión de diagnóstico  
 Este ejemplo crea una sesión de diagnóstico para registrar las métricas de rendimiento del motor de base de datos. En el ejemplo se crea una sesión de diagnóstico que realiza escuchas de eventos de ejecución/final de consulta de motor y los eventos de bloqueo DMS. Lo que se devuelve es el texto del comando, el nombre del equipo, el Id. de solicitud (Id. de consulta) y la sesión que creó el evento.  
  
```  
CREATE DIAGNOSTICS SESSION MYDIAGSESSION AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:EngineQueryRunningEvent" />  
      <Event Name="DmsCoreInstrumentation:DmsBlockingQueueEnqueueBeginEvent" />  
      <Where>  
         <SessionId Value="381" ComparisonType="NotEquals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Query.CommandText" />  
      <Property Name="MachineName" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Alias" />  
      <Property Name="Duration" />  
      <Property Name="Session.SessionId" />  
   </Capture>  
</Session>';  
```  
  
 Después de la creación de la sesión de diagnóstico, ejecute una consulta.  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 A continuación, ver los resultados de la sesión de diagnóstico seleccionándola en el esquema de sysdiag.  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 Observe que el esquema sysdiag contiene una vista que se denomina el nombre de la sesión de diagnóstico.  
  
 Para ver únicamente la actividad para la conexión, agregue el `Session.SPID` propiedad y agregue `WHERE [Session.SPID] = @@spid;` a la consulta.  
  
 Cuando haya terminado con la sesión de diagnóstico, eliminarse con la **diagnóstico de DROP** comando.  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>B. Sesión de diagnóstico alternativo  
 Un segundo ejemplo con propiedades ligeramente diferentes.  
  
```  
-- Determine the session_id of your current session  
SELECT TOP 1 session_id();  
-- Replace \<*session_number*> in the code below with the numbers in your session_id  
CREATE DIAGNOSTICS SESSION PdwOptimizationDiagnostics AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:MemoGenerationBeginEvent" />  
      <Event Name="EngineInstrumentation:MemoGenerationEndEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationBeginEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationEndEvent" />  
      <Event Name="DSQLInstrumentation:BuildRelOpContextTreeBeginEvent" />  
      <Event Name="DSQLInstrumentation:PostPlanGenModifiersEndEvent" />  
      <Where>  
         <SessionId Value="\<*session_number*>" ComparisonType="Equals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Session.SessionId" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Query.CommandText" />  
      <Property Name="Name" />  
      <Property Name="DateTimePublished" />  
      <Property Name="DateTimePublished.Ticks" />  
  </Capture>  
</Session>';  
```  
  
 Ejecutar una consulta, como por ejemplo:  
  
```  
USE ssawPDW;  
GO  
SELECT * FROM dbo.FactFinance;  
```  
  
 La consulta siguiente devuelve los intervalos de autorización:  
  
```  
SELECT *   
FROM master.sysdiag.PdwOptimizationDiagnostics   
ORDER BY DateTimePublished;  
```  
  
 Cuando haya terminado con la sesión de diagnóstico, eliminarse con la **diagnóstico de DROP** comando.  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  

