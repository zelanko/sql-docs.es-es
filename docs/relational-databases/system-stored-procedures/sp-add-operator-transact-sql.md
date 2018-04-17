---
title: sp_add_operator (Transact-SQL) | Documentos de Microsoft
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
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c91f79397a84f6277f4bb891144a5fceb40d02ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spaddoperator-transact-sql"></a>sp_add_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un operador (destinatario de la notificación) para utilizarlo con las alertas y los trabajos.  
  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_operator [ @name = ] 'name'   
     [ , [ @enabled = ] enabled ]   
     [ , [ @email_address = ] 'email_address' ]   
     [ , [ @pager_address = ] 'pager_address' ]   
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
 [  **@name=** ] **'***nombre***'**  
 Nombre de un operador (destinatario de la notificación). Este nombre debe ser único y no puede contener el porcentaje (**%**) caracteres. *nombre* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@enabled=** ] *habilitado*  
 Indica el estado actual del operador. *habilitado* es **tinyint**, su valor predeterminado es **1** (habilitado). Si **0**, el operador no está habilitado y no recibe notificaciones.  
  
 [  **@email_address=** ] **'***email_address***'**  
 La dirección de correo electrónico del operador. Esta cadena se pasa directamente al sistema de correo electrónico. *Email_Address* es **nvarchar (100)**, su valor predeterminado es null.  
  
 Puede especificar una dirección de correo electrónico física o un alias para *email_address*. Por ejemplo:  
  
 '**jdoe**'o'**jdoe@xyz.com**'  
  
> [!NOTE]  
>  Debe utilizar la dirección de correo electrónico para Correo electrónico de base de datos.  
  
 [  **@pager_address=** ] **'***pager_address***'**  
 La dirección del buscapersonas del operador. Esta cadena se pasa directamente al sistema de correo electrónico. *pager_address* es **narchar(100)**, su valor predeterminado es null.  
  
 [ **@weekday_pager_start_time=** ] *weekday_pager_start_time*  
 Hora a partir de la cual el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envía una notificación mediante buscapersonas al operador especificado los días laborables, de lunes a viernes. *weekday_pager_start_time*es **int**, su valor predeterminado es **090000**, lo que indica 9:00 A.M. en un reloj de 24 horas. Se debe especificar con el formato HHMMSS.  
  
 [  **@weekday_pager_end_time=** ] *weekday_pager_end_time*  
 El tiempo después del cual **SQLServerAgent** servicio deja de enviar una notificación por buscapersonas al operador especificado los días laborables, del lunes al viernes. *weekday_pager_end_time*es **int**, su valor predeterminado es 180000, lo que indica las 6:00 p. M. en un reloj de 24 horas. Se debe especificar con el formato HHMMSS.  
  
 [ **@saturday_pager_start_time =**] *saturday_pager_start_time*  
 El tiempo después del cual **SQLServerAgent** servicio envía una notificación por buscapersonas al operador especificado los sábados. *saturday_pager_start_time* es **int**, su valor predeterminado es 090000, lo que indica 9:00 A.M. en un reloj de 24 horas. Se debe especificar con el formato HHMMSS.  
  
 [  **@saturday_pager_end_time=** ] *saturday_pager_end_time*  
 El tiempo después del cual **SQLServerAgent** servicio ya no envía una notificación por buscapersonas al operador especificado los sábados. *saturday_pager_end_time*es **int**, su valor predeterminado es **180000**, que indica las 6:00 P.M. en un reloj de 24 horas. Se debe especificar con el formato HHMMSS.  
  
 [ **@sunday_pager_start_time=** ] *sunday_pager_start_time*  
 El tiempo después del cual **SQLServerAgent** servicio envía una notificación por buscapersonas al operador especificado los domingos. *sunday_pager_start_time*es **int**, su valor predeterminado es **090000**, lo que indica 9:00 A.M. en un reloj de 24 horas. Se debe especificar con el formato HHMMSS.  
  
 [  **@sunday_pager_end_time =**] *sunday_pager_end_time*  
 El tiempo después del cual **SQLServerAgent** servicio ya no envía una notificación por buscapersonas al operador especificado los domingos. *sunday_pager_end_time*es **int**, su valor predeterminado es **180000**, que indica las 6:00 P.M. en un reloj de 24 horas. Se debe especificar con el formato HHMMSS.  
  
 [  **@pager_days=** ] *pager_days*  
 Es un número que indica los días que el operador está disponible para recibir avisos de localización (de acuerdo con las horas de inicio y fin especificadas). *pager_days*es **tinyint**, su valor predeterminado es **0** que indica el operador no está nunca disponible para recibir un aviso. Los valores válidos son de **0** a través de **127**. *pager_days*se calcula sumando los valores individuales de los días necesarios. Por ejemplo, del lunes al viernes es **2**+**4**+**8**+**16** + **32** = **62**. En la siguiente tabla se incluye el valor para cada día de la semana.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Lunes|  
|**4**|Martes|  
|**8**|Miércoles|  
|**16**|Jueves|  
|**32**|Viernes|  
|**64**|Sábado|  
  
 [  **@netsend_address=** ] **'***netsend_address***'**  
 La dirección de red del operador al que se envía el mensaje de red. *netsend_address*es **nvarchar (100)**, su valor predeterminado es null.  
  
 [  **@category_name=** ] **'***categoría***'**  
 El nombre de la categoría de este operador. *categoría* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_add_operator** se debe ejecutar desde la **msdb** base de datos.  
  
 Los avisos de localización son compatibles con el sistema de correo electrónico, que debe disponer de capacidad de correo electrónico a buscapersonas si desea utilizar esta funcionalidad.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofrece un método gráfico sencillo para administrar trabajos y es el método recomendado para crear y administrar la infraestructura de trabajo.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_add_operator**.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se configura la información del operador para `danwi`. El operador está habilitado. El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envía notificaciones por buscapersonas de lunes a viernes, de 8 a.m. a 5 p.m.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_operator  
    @name = N'Dan Wilson',  
    @enabled = 1,  
    @email_address = N'danwi',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 62 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
