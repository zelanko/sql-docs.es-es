---
title: sys.fn_trace_gettable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_trace_gettable
- fn_trace_gettable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_trace_gettable function
- sys.fn_trace_gettable function
ms.assetid: c2590159-6ec5-4510-81ab-e935cc4216cd
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2624c7ea8a3c118f1bb1da2e456bd03cbbdbe968
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="sysfntracegettable-transact-sql"></a>sys.fn_trace_gettable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el contenido de uno o más archivos de seguimiento en forma de tabla.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use eventos extendidos en su lugar.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_trace_gettable ( 'filename' , number_files )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*filename*'  
 Especifica el archivo de seguimiento inicial que se va a leer. *nombre de archivo* es **nvarchar (256)**, no tiene ningún valor predeterminado.  
  
 *number_files*  
 Especifica el número de archivos de sustitución que se van a leer. Este número incluye el archivo inicial especificado en *filename*. *number_files* es un **int**.  
  
## <a name="remarks"></a>Comentarios  
 Si *number_files* se especifica como **predeterminado**, **fn_trace_gettable** lee todos los archivos de sustitución incremental hasta que alcanza el final del seguimiento. **fn_trace_gettable** devuelve una tabla con todas las columnas válidas para el seguimiento especificado. Para obtener más información, vea [sp_trace_setevent &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
 Tenga en cuenta que la función fn_trace_gettable no cargará los archivos de sustitución incremental (cuando se especifica esta opción mediante el uso de la *number_files* argumento) donde el nombre de archivo de seguimiento original termina con un carácter de subrayado y un valor numérico. (Esto no se aplica al carácter de subrayado y al número que se anexan automáticamente cuando un archivo realiza la sustitución incremental). Para solucionar este problema, puede cambiar el nombre de los archivos de seguimiento y quitar los caracteres de subrayado del nombre de archivo original. Por ejemplo, si el archivo original se denomina **Trace_Oct_5.trc** y el archivo de sustitución incremental se denomina **Trace_Oct_5_1.trc**, puede cambiar el nombre de los archivos a **TraceOct5.trc** y  **TraceOct5_1.trc**.  
  
 Esta función puede leer un seguimiento que todavía esté activo en la instancia en la que se ejecuta.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER TRACE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-fntracegettable-to-import-rows-from-a-trace-file"></a>A. Usar fn_trace_gettable para importar filas de un archivo de seguimiento  
 En el siguiente ejemplo se llama a `fn_trace_gettable` en la cláusula `FROM` de una instrucción `SELECT...INTO`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
### <a name="b-using-fntracegettable-to-return-a-table-with-an-identity-column-that-can-be-loaded-into-a-sql-server-table"></a>B. Usar fn_trace_gettable para devolver una tabla con una columna IDENTITY que se pueda cargar en una tabla de SQL Server  
 Este ejemplo llama a la función como parte de una instrucción `SELECT...INTO` y devuelve una tabla con una columna `IDENTITY` que se puede cargar en la tabla `temp_trc`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENTITY(int, 1, 1) AS RowNumber, * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
