---
title: sp_update_operator (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a98f5a61c76e1e6ef0cd2dc2a17a445084dd15eb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spupdateoperator-transact-sql"></a>sp_update_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza información acerca de un operador (destinatario de la notificación) para utilizarla con las alertas y los trabajos.  
  
   ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]  
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]  
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]  
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @name=] '*nombre*'  
 El nombre del operador que se va a modificar. *nombre* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ @new_name=] '*new_name*'  
 Nuevo nombre del operador. El nombre debe ser único. *new_name* es **sysname**, su valor predeterminado es null.  
  
 [ @enabled=] *habilitado*  
 Un número que indica el estado actual del operador (**1** si está habilitado, **0** si no). *habilitado* es **tinyint**, su valor predeterminado es null. Si no está habilitado, un operador no recibirá notificaciones de alertas.  
  
 [ @email_address=] '*email_address*'  
 La dirección de correo electrónico del operador. Esta cadena se pasa directamente al sistema de correo electrónico. *Email_Address* es **nvarchar (100)**, su valor predeterminado es null.  
  
 [ @pager_address=] '*pager_number*'  
 La dirección del buscapersonas del operador. Esta cadena se pasa directamente al sistema de correo electrónico. *pager_number* es **nvarchar (100)**, su valor predeterminado es null.  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 Especifica la hora a partir de la cual puede enviarse una notificación por buscapersonas a este operador, de lunes a viernes. *weekday_pager_start_time*es **int**, su valor predeterminado es null y debe especificarse en el formato HHMMSS para utilizarse con un reloj de 24 horas.  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 Especifica la hora a partir de la cual no puede enviarse una notificación por buscapersonas al operador especificado, de lunes a viernes. *weekday_pager_end_time*es **int**, su valor predeterminado es null y debe especificarse en el formato HHMMSS para utilizarse con un reloj de 24 horas.  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 Especifica la hora a partir de la cual puede enviarse una notificación por buscapersonas los sábados al operador especificado. *saturday_pager_start_time*es **int**, su valor predeterminado es null y debe especificarse en el formato HHMMSS para utilizarse con un reloj de 24 horas.  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 Especifica la hora a partir de la cual no puede enviarse una notificación por buscapersonas los sábados al operador especificado. *saturday_pager_end_time*es **int**, su valor predeterminado es null y debe especificarse en el formato HHMMSS para utilizarse con un reloj de 24 horas.  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 Especifica la hora a partir de la cual puede enviarse una notificación por buscapersonas los domingos al operador especificado. *sunday_pager_start_time*es **int**, su valor predeterminado es null y debe especificarse en el formato HHMMSS para utilizarse con un reloj de 24 horas.  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 Especifica la hora a partir de la cual no puede enviarse una notificación por buscapersonas los domingos al operador especificado. *sunday_pager_end_time*es **int**, su valor predeterminado es null y debe especificarse en el formato HHMMSS para utilizarse con un reloj de 24 horas.  
  
 [ @pager_days=] *pager_days*  
 Especifica los días en que el operador está disponible para recibir mensajes por buscapersonas (de acuerdo con las horas inicial y final especificadas). *pager_days*es **tinyint**, su valor predeterminado es null y debe estar comprendido entre **0** a través de **127**. *pager_days* se calcula sumando los valores individuales de los días necesarios. Por ejemplo, del lunes al viernes es **2**+**4**+**8**+**16** + **32** = **64**.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Lunes|  
|**4**|Martes|  
|**8**|Miércoles|  
|**16**|Jueves|  
|**32**|Viernes|  
|**64**|Sábado|  
  
 [ @netsend_address=] '*netsend_address*'  
 La dirección de red del operador al que se envía el mensaje de red. *netsend_address*es **nvarchar (100)**, su valor predeterminado es null.  
  
 [ @category_name=] '*categoría*'  
 El nombre de la categoría de esta alerta. *categoría* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_update_operator se debe ejecutar desde la base de datos msdb.  
  
## <a name="permissions"></a>Permissions  
 Permisos para ejecutar este procedimiento de forma predeterminada a los miembros del rol fijo de servidor sysadmin.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se actualiza el estado del operador a habilitado y se establecen los días (de lunes a viernes, de 8 a.m. a 5 p.m.) en que se le puede enviar una notificación por buscapersonas.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
