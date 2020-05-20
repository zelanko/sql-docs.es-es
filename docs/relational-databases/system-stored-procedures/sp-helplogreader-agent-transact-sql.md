---
title: sp_helplogreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords:
- sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4c1afca8eed465c191fccb4d24e79a7bd95af9aa
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828936"
---
# <a name="sp_helplogreader_agent-transact-sql"></a>sp_helplogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve las propiedades del trabajo del Agente de registro del LOG para la base de datos de publicaciones. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|IDENTIFICADOR del agente.|  
|**name**|**nvarchar(100**|Nombre del agente.|  
|**publisher_security_mode**|**smallint**|Modo de seguridad utilizado por el agente al conectarse al publicador, que puede ser uno de los siguientes:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows.|  
|**publisher_login**|**sysname**|Inicio de sesión utilizado para conectarse al publicador.|  
|**publisher_password**|**nvarchar (524)**|Por motivos de seguridad, **\*\*\*\*\*\*\*\*\*\*** siempre se devuelve un valor de.|  
|**job_id**|**uniqueidentifier**|Id. único del trabajo del agente.|  
|**job_login**|**nvarchar(512)**|Es la cuenta de Windows con la que se ejecuta el agente de registro del log, que se devuelve con el formato *dominio* \\ *nombreDeUsuario*.|  
|**job_password**|**sysname**|Por motivos de seguridad, **\*\*\*\*\*\*\*\*\*\*** siempre se devuelve un valor de.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helplogreader_agent** se utiliza en la replicación transaccional.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** en el publicador o los miembros del rol fijo de base de datos **db_owner** en la base de datos de publicación pueden ejecutar **sp_helplogreader_agent**.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y modificar la configuración de seguridad de la replicación](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addlogreader_agent &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_changelogreader_agent &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
