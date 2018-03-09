---
title: sp_helpqreader_agent (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50492a76e742459e7b883f9887026d0ce63d1eb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpqreaderagent-transact-sql"></a>sp_helpqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve las propiedades del Agente de lectura de cola. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución o en el publicador en cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@frompublisher=** ] *frompublisher*  
 Especifica si se llama al procedimiento almacenado en el publicador o en el distribuidor. *frompublisher* es de tipo bit, con un valor predeterminado de 0. **1** significa que se llama al procedimiento almacenado del publicador, y **0** significa que el procedimiento almacenado se llama desde el distribuidor.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del agente.|  
|**Nombre**|**nvarchar (100)**|Nombre del agente.|  
|**job_id**|**uniqueidentifier**|Id. único del trabajo del agente.|  
|**job_login**|**nvarchar(512)**|Es la cuenta de Windows bajo la que se ejecuta el agente de distribución, que se devuelve en el formato *dominio*\\*nombre de usuario*.|  
|**job_password**|**sysname**|Por motivos de seguridad, un valor de  **\* \* \* \* \* \* \* \* \* \***  siempre es Devuelve.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpqreader_agent** se utiliza en la replicación transaccional.  
  
## <a name="permissions"></a>Permissions  
 Cuando el valor de *frompublisher* es **1**, solo los miembros de la **sysadmin** rol fijo de servidor en el publicador o los miembros de la **db_owner**rol fijo de base de datos en la base de datos de publicación puede ejecutar **sp_helpqreader_agent**. En caso contrario, solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor o los miembros de la **db_owner** rol fijo de base de datos en la base de datos de distribución puede ejecutar **sp_helpqreader_ agente**.  
  
## <a name="see-also"></a>Vea también  
 [Habilitar suscripciones actualizables para publicaciones transaccionales](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
