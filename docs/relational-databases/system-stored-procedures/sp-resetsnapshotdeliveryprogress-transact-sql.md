---
title: sp_resetsnapshotdeliveryprogress (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
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
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0aa67918309c5c34bbe3826853c26cf7422c4666
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spresetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restablece el proceso de entrega de instantáneas de una suscripción de extracción para poder reiniciar la entrega de instantáneas. Se ejecuta en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@verbose_level** =] *verbose_level*  
 Especifica la cantidad de información devuelta. *verbose_level*es **int**, su valor predeterminado es **1**. Un valor de **1** significa que el error se devuelve si no se puede obtener los bloqueos necesarios en el **MSsnapshotdeliveryprogress** tabla, y **0** significa que se devuelve ningún error.  
  
 [  **@drop_table** =] **'***drop_table***'**  
 Indica si se quita o trunca la tabla que contiene información sobre el progreso de la instantánea. *drop_table* es **nvarchar (5)**, su valor predeterminado es **FALSE**. que significa que la tabla se trunca. Si es True, la tabla se quita.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_resetsnapshotdeliveryprogress** quita todas las filas de la **MSsnapshotdeliveryprogress** tabla. Se quitan todos los metadatos que hayan quedado en la base de datos de suscripciones después de un progreso anterior que se haya realizado en los procesos de entrega de instantáneas.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_resetsnapshotdeliveryprogress**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
