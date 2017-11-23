---
title: sp_replsetoriginator (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords: sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c4fc0aa2ee6dcb1b410c55977469d7d62c6f1dd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spreplsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza para invocar la detección y control de bucles invertidos en la replicación transaccional bidireccional. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@server_name=**] **'***nombre_servidor***'**  
 Es el nombre del servidor donde se aplica la transacción. *originating_server* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@database_name=**] **'***database_name***'**  
 Es el nombre de la base de datos donde se aplica la transacción. *originating_db* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replsetoriginator** se ejecuta el agente de distribución para registrar el origen de las transacciones aplicadas mediante replicación. Esta información se utiliza para invocar la detección de bucles invertidos en suscripciones transaccionales bidireccionales que tienen establecida la propiedad de bucles invertidos.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el publicador, los miembros de la **db_owner** rol fijo de base de datos en la base de datos de publicación, o los usuarios en la lista de acceso de publicación (PAL) puede ejecutar **sp_replsetoriginator**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
