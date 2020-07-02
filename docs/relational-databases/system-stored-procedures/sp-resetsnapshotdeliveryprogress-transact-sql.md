---
title: sp_resetsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e87afd1d76eb4bfb9602e1b3d57dd62a43b65772
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85639875"
---
# <a name="sp_resetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Restablece el proceso de entrega de instantáneas de una suscripción de extracción para poder reiniciar la entrega de instantáneas. Se ejecuta en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @verbose_level = ] verbose_level`Especifica la cantidad de información devuelta. *verbose_level*es de **tipo int**y su valor predeterminado es **1**. Un valor de **1** significa que se devuelve un error si no se pueden obtener los bloqueos necesarios en la tabla **MSsnapshotdeliveryprogress** y **0** significa que no se devuelve ningún error.  
  
`[ @drop_table = ] 'drop_table'`Indica si se va a quitar o truncar la tabla que contiene información sobre el progreso de la instantánea. *drop_table* es de tipo **nvarchar (5)** y su valor predeterminado es **false**. que significa que la tabla se trunca. Si es True, la tabla se quita.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_resetsnapshotdeliveryprogress** quita todas las filas de la tabla **MSsnapshotdeliveryprogress** . Se quitan todos los metadatos que hayan quedado en la base de datos de suscripciones después de un progreso anterior que se haya realizado en los procesos de entrega de instantáneas.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_resetsnapshotdeliveryprogress**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
