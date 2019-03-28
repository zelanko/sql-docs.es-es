---
title: sp_trace_generateevent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_generateevent_TSQL
- sp_trace_generateevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_generateevent
ms.assetid: 3ef05bfb-b467-4403-89cc-6e77ef9247dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a24bb05e8f10e2920bd206531723c228d6c1734
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529357"
---
# <a name="sptracegenerateevent-transact-sql"></a>sp_trace_generateevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un evento definido por el usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
>**NOTA:**  Este procedimiento almacenado es **no** en desuso. El resto de los procedimientos almacenados relacionados con el seguimiento están en desuso.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @eventid = ] event_id` Es el identificador del evento que se va a activar. *event_id* es **int**, no tiene ningún valor predeterminado. El identificador debe ser uno de los números de evento del 82 al 91, que representan los eventos definidos por el usuario como se establece mediante [sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
`[ @userinfo = ] 'user_info'` Es la cadena opcional definida por el usuario que identifica la causa del evento. *user_info* es **nvarchar (128)**, su valor predeterminado es null.  
  
`[ @userdata = ] user_data` Son los datos opcionales especificados por el usuario para el evento. *user_data* es **varbinary (8000)**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 En la tabla siguiente se describen los valores del código que los usuarios pueden obtener después de completar el procedimiento almacenado.  
  
|Código de retorno|Descripción|  
|-----------------|-----------------|  
|**0**|Ningún error.|  
|**1**|Error desconocido.|  
|**3**|El evento especificado no es válido. Puede que el evento no exista o que no sea adecuado para el procedimiento almacenado.|  
|**13**|Memoria insuficiente. Se devuelve cuando no hay memoria suficiente para realizar la acción especificada.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_trace_generateevent** realiza muchas de las acciones ejecutadas previamente por el **xp_trace_\***  procedimientos almacenados extendidos. Use **sp_trace_generateevent** en lugar de **xp_trace_generate_event**.  
  
 Solo los números de Id. de eventos definido por el usuario pueden utilizarse con **sp_trace_generateevent**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generará un error si se utilizan otros números de Id. de eventos.  
  
 Los parámetros de seguimiento de SQL de todos los procedimientos almacenados (**sp_trace_xx**) deben escribirse. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devolverá un error.  
  
## <a name="permissions"></a>Permisos  
 El usuario debe tener permiso ALTER TRACE.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea un evento configurable por el usuario en una tabla de ejemplo.  
  
```  
--Create a sample table.  
CREATE TABLE user_config_test(col1 int, col2 char(10));  
  
--DROP the trigger if it already exists.  
IF EXISTS  
   (SELECT * FROM sysobjects WHERE name = 'userconfig_trg')  
   DROP TRIGGER userconfig_trg;  
  
--Create an ON INSERT trigger on the sample table.  
CREATE TRIGGER userconfig_trg  
   ON user_config_test FOR INSERT;  
AS  
EXEC master..sp_trace_generateevent  
   @event_class = 82, @userinfo = N'Inserted row into user_config_test';  
  
--When an insert action happens, the user-configurable event fires. If   
you were capturing the event id=82, you will see it in the Profiler output.  
INSERT INTO user_config_test VALUES(1, 'abc');  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Seguimiento de SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
