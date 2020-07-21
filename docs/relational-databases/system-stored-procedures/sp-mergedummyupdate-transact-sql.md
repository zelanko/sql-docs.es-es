---
title: sp_mergedummyupdate (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords:
- sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5502b64da269639d99fe54d4930f7f3b7b145d73
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899368"
---
# <a name="sp_mergedummyupdate-transact-sql"></a>sp_mergedummyupdate (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Realiza una actualización ficticia en la fila especificada de forma que se envíe de nuevo durante la siguiente mezcla. Este procedimiento almacenado se puede ejecutar en el publicador de la base de datos de publicaciones o en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @source_object = ] 'source_object'`Es el nombre del objeto de origen. *source_object*es de tipo **nvarchar (386)** y no tiene ningún valor predeterminado.  
  
`[ @rowguid = ] 'rowguid'`Es el identificador de fila. *ROWGUID* es de tipo **uniqueidentifier**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_mergedummyupdate** se utiliza en la replicación de mezcla.  
  
 **sp_mergedummyupdate** resulta útil si escribe su propia alternativa al Visor de conflictos de replicación (Wzcnflct.exe).  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de base de datos **db_owner** pueden ejecutar **sp_mergedummyupdate**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
