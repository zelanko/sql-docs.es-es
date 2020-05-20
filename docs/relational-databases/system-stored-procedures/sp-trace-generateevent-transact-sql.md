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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5c5807225c2bda185b61050433cc3378b25b6fe1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82809885"
---
# <a name="sp_trace_generateevent-transact-sql"></a>sp_trace_generateevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un evento definido por el usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
>**Nota:**  Este procedimiento almacenado **no** está en desuso. El resto de los procedimientos almacenados relacionados con el seguimiento están en desuso.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @eventid = ] event_id`Es el identificador del evento que se va a activar. *event_id* es de **tipo int**y no tiene ningún valor predeterminado. El ID. debe ser uno de los números de eventos de 82 a 91, que representan eventos definidos por el usuario como se establecen con [sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
`[ @userinfo = ] 'user_info'`Es la cadena opcional definida por el usuario que identifica el motivo del evento. *user_info* es de tipo **nvarchar (128)** y su valor predeterminado es NULL.  
  
`[ @userdata = ] user_data`Son los datos opcionales especificados por el usuario para el evento. *user_data* es **varbinary (8000)** y su valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 En la tabla siguiente se describen los valores del código que los usuarios pueden obtener después de completar el procedimiento almacenado.  
  
|Código de retorno|Descripción|  
|-----------------|-----------------|  
|**0**|Ningún error.|  
|**1**|Error desconocido.|  
|**3**|El evento especificado no es válido. Puede que el evento no exista o que no sea adecuado para el procedimiento almacenado.|  
|**13**|Memoria insuficiente. Se devuelve cuando no hay memoria suficiente para realizar la acción especificada.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_trace_generateevent** realiza muchas de las acciones ejecutadas previamente por los procedimientos almacenados extendidos de **xp_trace_ \* ** . Use **sp_trace_generateevent** en lugar de **xp_trace_generate_event**.  
  
 Solo se pueden usar los números de ID. de eventos definidos por el usuario con **sp_trace_generateevent**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generará un error si se utilizan otros números de Id. de eventos.  
  
 Los parámetros de todos los procedimientos almacenados de seguimiento de SQL (**sp_trace_xx**) tienen un tipo estricto. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devolverá un error.  
  
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
  
## <a name="see-also"></a>Consulte también:  
 [Sys. fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Seguimiento de SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
