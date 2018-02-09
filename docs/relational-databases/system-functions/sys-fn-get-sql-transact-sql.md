---
title: sys.fn_get_sql (Transact-SQL) | Microsoft Docs
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
- fn_get_sql
- sys.fn_get_sql_TSQL
- fn_get_sql_TSQL
- sys.fn_get_sql
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_sql function
- text [SQL Server], SQL handles
- sys.fn_get_sql function
- valid SQL handles [SQL Server]
- SQL handles
ms.assetid: d5fe49b5-0813-48f2-9efb-9187716b2fd4
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 941417a97ce739173e2aba195d51ec845848186f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="sysfngetsql-transact-sql"></a>sys.fn_get_sql (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el texto de la instrucción SQL para el identificador SQL especificado.  
  
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Microsoft SQL Server. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Use sys.dm_exec_sql_text en su lugar. Para obtener más información, vea [sys.dm_exec_sql_text &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_get_sql ( SqlHandle )  
```  
  
## <a name="arguments"></a>Argumentos  
 *SqlHandle*  
 Es el valor del identificador. *SqlHandle* es **varbinary(64)** no tiene ningún valor predeterminado.  
  
## <a name="tables-returned"></a>Tablas devueltas  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|dbid|**smallint**|Id. de la base de datos. En el caso de instrucciones SQL ad hoc y preparadas, identificador de la base de datos en que se compilaron las instrucciones.|  
|objectid|**int**|Identificador del objeto de base de datos. Este valor es NULL para las instrucciones SQL ad hoc.|  
|number|**smallint**|Indica el número del grupo, si se agrupan los procedimientos.<br /><br /> 0 = Las no son procedimientos.<br /><br /> NULL = Instrucciones SQL ad hoc.|  
|encrypted|**bit**|Indica si el objeto está cifrado.<br /><br /> 0 = No cifrado<br /><br /> 1 = Cifrada|  
|texto|**texto**|Texto de la instrucción SQL. Este valor es NULL para objetos cifrados.|  
  
## <a name="remarks"></a>Comentarios  
 Puede obtener un identificador SQL válido de la columna sql_handle de la [sys.dm_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) vista de administración dinámica.  
  
 Si se pasa un identificador que ya no existe en la memoria caché, fn_get_sq**l** devuelve un conjunto de resultados vacío. Si pasa un identificador no válido, el archivo por lotes se detiene y aparece un mensaje de error.  
  
 El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no se puede almacenar en caché algunas [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones, como instrucciones de copia masiva e instrucciones con literales de cadena mayores de 8 KB. No se pueden recuperar identificadores de esas instrucciones utilizando la función fn_get_sql.  
  
 El **texto** columna del conjunto de resultados se filtra con texto que puede contener contraseñas. Para más información acerca de la seguridad relacionados con los procedimientos almacenados que no se supervisan, vea [filtrar un seguimiento](../../relational-databases/sql-trace/filter-a-trace.md).  
  
 La función fn_get_sql devuelve información similar a la [DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md) comando. Los siguientes son ejemplos de situaciones en las que se puede utilizar la función fn_get_sql cuando no se puede utilizar DBCC INPUTBUFFER:   
  
-   Cuando los eventos tengan más de 255 caracteres.  
  
-   Cuando tenga que devolver el nivel más alto de anidamiento de un procedimiento almacenado. Por ejemplo, hay dos procedimientos almacenados denominados sp_1 y sp_2. Si sp_1 llama a sp_2 y el identificador se obtiene de la vista de administración dinámica sys.dm_exec_requests mientras se ejecuta sp_2, la función fn_get_sql devuelve información sobre sp_2. Además, la función fn_get_sql devuelve el texto completo del procedimiento almacenado en el nivel más alto de anidamiento.  
  
## <a name="permissions"></a>Permissions  
 El usuario necesita tener el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 Los administradores de base de datos pueden utilizar la función fn_get_sql, como se muestra en el ejemplo siguiente, para facilitar el diagnóstico de procesos problemáticos. Una vez que un administrador identifica el identificador de sesión problemático, puede recuperar el identificador SQL de esa sesión, llamar a la función fn_get_sql con él y luego utilizar los desplazamientos inicial y final para determinar el texto del identificador de sesión SQL problemático.  
  
```  
DECLARE @Handle varbinary(64);  
SELECT @Handle = sql_handle   
FROM sys.dm_exec_requests   
WHERE session_id = 52 and request_id = 0;  
SELECT * FROM sys.fn_get_sql(@Handle);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
