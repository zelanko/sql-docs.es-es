---
title: sp_check_for_sync_trigger (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_for_sync_trigger
helpviewer_keywords:
- sp_check_for_sync_trigger
ms.assetid: 54a1e2fd-c40a-43d4-ac64-baed28ae4637
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d274e25b3a12a4fdd60c32365626bcb9ba912848
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628703"
---
# <a name="spcheckforsynctrigger-transact-sql"></a>sp_check_for_sync_trigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Determina si se va a llamar a un procedimiento almacenado o un desencadenador definido por el usuario en el contexto de un desencadenador de replicación que se utiliza para suscripciones de actualización inmediata. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_check_for_sync_trigger [ @tabid = ] 'tabid'   
    [ , [ @trigger_op = ] 'trigger_output_parameters' OUTPUT ]  
    [ , [ @fonpublisher = ] fonpublisher ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@tabid =** ] '*tabid*'  
 Es el identificador de objeto de la tabla en la que se comprueba si hay desencadenadores de actualización inmediata. *tabid* es **int** no tiene ningún valor predeterminado.  
  
 [ **@trigger_op =** ] '*trigger_output_parameters*' salida  
 Especifica si el parámetro de salida va a devolver el tipo de desencadenador desde el que se le llama. *trigger_output_parameters* es **char (10)** y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**INS**|Desencadenador INSERT.|  
|**UPD**|Desencadenador UPDATE.|  
|**SUPR**|Desencadenador DELETE.|  
|NULL (predeterminado)||  
  
 [  **@fonpublisher =** ] *fonpublisher*  
 Especifica la ubicación donde el procedimiento almacenado se ejecuta. *fonpublisher* es **bit**, con un valor predeterminado de 0. Si es 0, la ejecución está en el suscriptor y si es 1, la ejecución está en el publicador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El valor 0 indica que el procedimiento almacenado no se llama en el contexto de un desencadenador de actualización inmediata. 1 indica que se llama dentro del contexto de un desencadenador de actualización inmediata y es el tipo de desencadenador que se devuelve en *@trigger_op*.  
  
## <a name="remarks"></a>Comentarios  
 **sp_check_for_sync_trigger** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_check_for_sync_trigger** se usa para coordinar entre la réplica y los desencadenadores definidos por el usuario. Este procedimiento almacenado determina si se le llama en el contexto de un desencadenador de replicación. Por ejemplo, puede llamar al procedimiento **sp_check_for_sync_trigger** en el cuerpo de un desencadenador definido por el usuario. Si **sp_check_for_sync_trigger** devuelve **0**, el desencadenador definido por el usuario continúa el procesamiento. Si **sp_check_for_sync_trigger** devuelve **1**, se cierra el desencadenador definido por el usuario. Así se garantiza que el desencadenador definido por el usuario no se activa cuando el desencadenador de replicación actualiza la tabla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra código que se podría utilizar en un desencadenador de una tabla del suscriptor.  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int  
SELECT @table_id = object_id('tablename')  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT  
IF @retcode = 1  
RETURN  
```  
  
## <a name="example"></a>Ejemplo  
 El código también puede agregarse a un desencadenador en una tabla en el publicador; el código es similar, pero la llamada a **sp_check_for_sync_trigger** incluye un parámetro adicional.  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int, @fonpublisher int  
SELECT @table_id = object_id('tablename')  
SELECT @fonpublisher = 1  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT, @fonpublisher  
IF @retcode = 1  
RETURN  
```  
  
## <a name="permissions"></a>Permisos  
 **sp_check_for_sync_trigger** procedimiento almacenado se puede ejecutar cualquier usuario con permisos SELECT en la [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) vista del sistema.  
  
## <a name="see-also"></a>Vea también  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
