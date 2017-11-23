---
title: sp_getmergedeletetype (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- sp_getmergedeletetype
- sp_getmergedeletetype_TSQL
helpviewer_keywords: sp_getmergedeletetype
ms.assetid: 64450e4d-844d-4176-874e-f3845536f7d2
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a517b90bd59f22c6851403b8928e903eecca7c55
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spgetmergedeletetype-transact-sql"></a>sp_getmergedeletetype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el tipo de eliminación de mezcla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_getmergedeletetype [ @source_object = ] 'source_object', [ @rowguid =] 'rowguid', [ @delete_type=] delete_type OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@source_object =**] **'***source_object***'**  
 Es el nombre del objeto de origen. *source_object* es **nvarchar (386)**, no tiene ningún valor predeterminado.  
  
 [  **@rowguid=**] **'***rowguid***'**  
 Es el identificador de fila del tipo de eliminación. *ROWGUID* es **uniqueidentifier**, no tiene ningún valor predeterminado.  
  
 [  **@delete_type=**] *delete_type* **salida**  
 Es el código que indica el tipo de eliminación. *delete_type* es **int**, no tiene ningún valor predeterminado. *delete_type* también es un parámetro OUTPUT y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Eliminación por parte del usuario|  
|**5**|Eliminación parcial|  
|**6**|Eliminación por parte del sistema|  
  
## <a name="remarks"></a>Comentarios  
 **sp_getmergedeletetype** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_getmergedeletetype**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
