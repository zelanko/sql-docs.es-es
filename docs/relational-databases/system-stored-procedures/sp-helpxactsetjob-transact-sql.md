---
title: sp_helpxactsetjob (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpxactsetjob
- sp_helpxactsetjob_TSQL
helpviewer_keywords:
- sp_helpxactsetjob
ms.assetid: 242cea3e-e6ac-4f84-a072-b003b920eb33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7402fcc825e6f537703268c1fd3fead9c88b1f5e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62959615"
---
# <a name="sphelpxactsetjob-transact-sql"></a>sp_helpxactsetjob (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca del trabajo Xactset para un publicador de Oracle. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpxactsetjob [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publisher** = ] **'***publisher***'**  
 Es el nombre de la que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador al que pertenece el trabajo. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**jobnumber**|**int**|Número de trabajo de Oracle.|  
|**lastdate**|**varchar(22)**|Fecha en que se ejecutó el trabajo por última vez.|  
|**thisdate**|**varchar(22)**|Hora de cambio.|  
|**nextdate**|**varchar(22)**|Fecha en que se ejecutará el trabajo de nuevo.|  
|**broken**|**varchar(1)**|Marca de interrupción del trabajo.|  
|**interval**|**varchar(200)**|Intervalo del trabajo.|  
|**failures**|**int**|Número de errores del trabajo.|  
|**xactsetjobwhat**|**varchar(200)**|Nombre del procedimiento ejecutado por el trabajo.|  
|**xactsetjob**|**varchar(1)**|Estado del trabajo, que puede ser uno de los siguientes:<br /><br /> **1** -el trabajo está habilitado.<br /><br /> **0** -el trabajo está deshabilitado.|  
|**xactsetlonginterval**|**int**|Intervalo largo del trabajo.|  
|**xactsetlongthreshold**|**int**|Umbral largo del trabajo.|  
|**xactsetshortinterval**|**int**|Intervalo corto del trabajo.|  
|**xactsetshortthreshold**|**int**|Umbral corto del trabajo.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpxactsetjob** se utiliza en la replicación de instantáneas y transaccional para los publicadores de Oracle.  
  
 **sp_helpxactsetjob** siempre devuelve la configuración actual del trabajo Xactset (HREPL_XactSetJob) en el publicador. Si el trabajo Xactset se encuentra en la cola de trabajos, devuelve además los atributos del trabajo de la vista de diccionario de datos USER_JOB creada con la cuenta de administrador en el publicador de Oracle.  
  
## <a name="permissions"></a>Permisos  
 Solo un miembro de la **sysadmin** rol fijo de servidor puede ejecutar **sp_helpxactsetjob**.  
  
## <a name="see-also"></a>Vea también  
 [Configuración del trabajo del conjunto de transacciones para un publicador de Oracle&#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [sp_publisherproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)  
  
  
