---
title: Sys.dm_exec_xml_handles (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_xml_handles
- dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_xml_handles dynamic management function
ms.assetid: a873ce0f-6955-417a-96a1-b2ef11a83633
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c5b5b1ebf8d73a2ea3c93da337910775fcf9d43b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecxmlhandles-transact-sql"></a>sys.dm_exec_xml_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Devuelve información acerca de los identificadores activos que se han abierto por **sp_xml_preparedocument**.  
  
||  
|-|  
|**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dm_exec_xml_handles (session_id | 0 )  
```  
  
## <a name="arguments"></a>Argumentos  
 *session_id* | 0,  
 Id. de la sesión. Si *session_id* se especifica, esta función devuelve información acerca de los identificadores XML en la sesión especificada.  
  
 Si se especifica 0, esta función devuelve información acerca de todos los identificadores XML de todas las sesiones.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Id. de la sesión que contiene este identificador del documento XML.|  
|**document_id**|**int**|Id. de identificador de documento XML devuelto por **sp_xml_preparedocument**.|  
|**namespace_document_id**|**int**|Id. de identificador interno usado para el documento de espacio de nombres asociado que se ha pasado como tercer parámetro a **sp_xml_preparedocument**. Es NULL si no hay ningún documento de espacio de nombres.|  
|**sql_handle**|**varbinary(64)**|Identificador del texto del código SQL en el que se ha definido el identificador.|  
|**statement_start_offset**|**int**|Número de caracteres está ejecutando actualmente del lote o procedimiento almacenado en el que el **sp_xml_preparedocument** se produce la llamada. Puede utilizarse junto con la **sql_handle**, **statement_end_offset**y el **sys.dm_exec_sql_text** función de administración dinámica para recuperar el actualmente ejecutar la instrucción para la solicitud.|  
|**statement_end_offset**|**int**|Número de caracteres está ejecutando actualmente del lote o procedimiento almacenado en el que el **sp_xml_preparedocument** se produce la llamada. Puede utilizarse junto con la **sql_handle**, **statement_start_offset**y el **sys.dm_exec_sql_text** función de administración dinámica para recuperar el actualmente ejecutar la instrucción para la solicitud.|  
|**creation_time**|**datetime**|Marca de tiempo cuando **sp_xml_preparedocument** se llamó.|  
|**original_document_size_bytes**|**bigint**|Tamaño del documento XML no analizado, en bytes.|  
|**original_namespace_document_size_bytes**|**bigint**|Tamaño del documento de espacio de nombres XML no analizado, en bytes. Es NULL si no hay ningún documento de espacio de nombres.|  
|**num_openxml_calls**|**bigint**|Número de llamadas OPENXML para este identificador de documento.|  
|**row_count**|**bigint**|Número de filas devueltas por todas las llamadas OPENXML anteriores para este identificador de documento.|  
|**dormant_duration_ms**|**bigint**|Milisegundos desde la última llamada OPENXML. Si no se ha llamado OPENXML, devuelve los milisegundos desde el **sp_xml_preparedocument**llamada.|  
  
## <a name="remarks"></a>Comentarios  
 La duración de **sql_handles** utiliza para recuperar el texto SQL que ejecuta una llamada a **sp_xml_preparedocument** es mayor que el plan almacenado en caché utilizado para ejecutar la consulta. Si el texto de la consulta no está disponible en la memoria caché, los datos no pueden recuperarse usando la información proporcionada en el resultado de la función. Esto puede ocurrir si está ejecutando muchos lotes grandes.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE en el servidor para ver todas las sesiones o Id. de sesión que no son propiedad del autor de la llamada. El autor de la llamada siempre puede ver los datos de su propio Id. de sesión actual.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se seleccionan todos los identificadores activos.  
  
```  
SELECT * FROM sys.dm_exec_xml_handles(0);  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica &#40; relacionada con la ejecución Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
