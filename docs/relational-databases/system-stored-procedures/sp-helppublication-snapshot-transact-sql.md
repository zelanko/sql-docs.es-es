---
title: sp_helppublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c82b95cd68ec451129d0611b55d1366ab823ad47
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703533"
---
# <a name="sphelppublicationsnapshot-transact-sql"></a>sp_helppublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca del Agente de instantáneas de una publicación específica. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher =** ] **'***publisher***'**  
 Especifica que no es[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse cuando se agrega un artículo a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del agente de instantáneas.|  
|**Nombre**|**Nvarchar (100)**|Nombre del agente de instantáneas.|  
|**publisher_security_mode**|**smallint**|Modo de seguridad utilizado por el agente al conectarse al publicador, que puede ser uno de los siguientes:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows.|  
|**publisher_login**|**sysname**|Inicio de sesión utilizado para conectarse al publicador.|  
|**publisher_password**|**nvarchar (524)**|Por motivos de seguridad, un valor de **\* \* \* \* \* \* \* \* \* \*** siempre es Devuelve.|  
|**job_id**|**uniqueidentifier**|Id. único del trabajo del agente.|  
|**job_login**|**nvarchar(512)**|Es la cuenta de Windows bajo la que se ejecuta el agente de instantáneas, que se devuelve en el formato *dominio*\\*username*.|  
|**job_password**|**sysname**|Por motivos de seguridad, un valor de **\* \* \* \* \* \* \* \* \* \*** siempre es Devuelve.|  
|**schedule_name**|**sysname**|Nombre de la programación utilizada para este trabajo de agente.|  
|**frequency_type**|**int**|Se trata de la frecuencia de ejecución programada del agente, que puede ser uno de estos valores.<br /><br /> **1** = una vez<br /><br /> **2** = a petición<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensualmente<br /><br /> **32** = mensualmente relativa<br /><br /> **64** = inicio automático<br /><br /> **128** = periódica|  
|**frequency_interval**|**int**|Los días en los que se ejecuta el agente; puede tener los valores siguientes.<br /><br /> **1** = el domingo<br /><br /> **2** = el lunes<br /><br /> **3** = el martes<br /><br /> **4** = el miércoles<br /><br /> **5** = el jueves<br /><br /> **6** = el viernes<br /><br /> **7** = el sábado<br /><br /> **8** = día<br /><br /> **9** = días laborables<br /><br /> **10** = días del fin de semana|  
|**frequency_subday_type**|**int**|Es el tipo que define la frecuencia con que el agente ejecuta cuando *frequency_type* es **4** (diariamente), y puede tener uno de estos valores.<br /><br /> **1** = a la hora especificada<br /><br /> **2** = segundos<br /><br /> **4** = minutos<br /><br /> **8** = horas|  
|**frequency_subday_interval**|**int**|Número de intervalos de *frequency_subday_type* que se producen entre las ejecuciones programadas del agente.|  
|**frequency_relative_interval**|**int**|Es la semana que se ejecuta el agente en un mes determinado cuando *frequency_type* es **32** (relativo mensual), y puede tener uno de estos valores.<br /><br /> **1** = primero<br /><br /> **2** = segundo<br /><br /> **4** = tercero<br /><br /> **8** = cuarto<br /><br /> **16** = último|  
|**frequency_recurrence_factor**|**int**|Número de semanas o meses entre las ejecuciones programadas del agente.|  
|**active_start_date**|**int**|Fecha en que se programa la primera ejecución del agente, con el formato AAAAMMDD.|  
|**active_end_date**|**int**|Fecha en que se programa la última ejecución del agente, con el formato AAAAMMDD.|  
|**active_start_time**|**int**|Hora en que se programa la primera ejecución del agente, con el formato HHMMSS.|  
|**active_end_time**|**int**|Hora en que se programa la última ejecución del agente, con el formato HHMMSS.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_publication_snapshot** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el publicador o los miembros de la **db_owner** rol fijo de base de datos en la base de datos de publicación puede ejecutar **sp_help_publication_snapshot** .  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
