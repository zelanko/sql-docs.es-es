---
title: sp_changeqreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changeqreader_agent_TSQL
- sp_changeqreader_agent
helpviewer_keywords:
- sp_changeqreader_agent
ms.assetid: d3fe79c5-31ef-4565-bf38-b476b5fb16f7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2258510d8e28230d238d4187cb3d454078d60842
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829559"
---
# <a name="sp_changeqreader_agent-transact-sql"></a>sp_changeqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia propiedades de seguridad de un Agente de lectura de cola. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución o en el publicador de la base de datos de publicaciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changeqreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_login = ] 'job_login'`Es el inicio de sesión de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] cuenta de Windows con la que se ejecuta el agente. *job_login* es de tipo **nvarchar (257)** y su valor predeterminado es NULL.  
  
`[ @job_password = ] 'job_password'`Es la contraseña de la cuenta de Windows con la que se ejecuta el agente. *job_password* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @frompublisher = ] frompublisher`Es si el procedimiento se ejecuta en el publicador. *frompublisher* es de bit y su valor predeterminado es **0**. Un valor de **1** significa que el procedimiento se ejecuta desde el publicador en la base de datos de publicación.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changeqreader_agent** se utiliza en la replicación transaccional.  
  
 **sp_changeqreader_agent** se utiliza para cambiar la cuenta de Windows con la que se ejecuta un agente de lectura de cola. Puede cambiar la contraseña de un inicio de sesión de Windows existente o proporcionar una contraseña y un inicio de sesión de Windows nuevos.  
  
 Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_changeqreader_agent**.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y modificar la configuración de seguridad de la replicación](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
  
