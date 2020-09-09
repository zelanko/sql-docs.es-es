---
description: sp_helppeerrequests (Transact-SQL)
title: sp_helppeerrequests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0ea9dce50e440c9b519032d46340b1b0a495eea0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535161"
---
# <a name="sp_helppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve información sobre todas las solicitudes de estado recibidas por los participantes en una topología de replicación punto a punto, donde estas solicitudes se iniciaron mediante la ejecución de [sp_requestpeerresponse &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) en cualquier base de datos Publicada en la topología. Este procedimiento almacenado se ejecuta en la base de datos de publicación, en un publicador que participa en una topología de replicación punto a punto. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación en una topología punto a punto para la que se enviaron solicitudes de estado. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @description = ] 'description'` Valor que se puede utilizar para identificar solicitudes de estado individuales, lo que permite filtrar las respuestas devueltas en función de la información definida por el usuario proporcionada al llamar a [sp_requestpeerresponse &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). la *Descripción* es de tipo **nvarchar (4000)** y su valor predeterminado es **%** . De forma predeterminada, se devuelven todas las solicitudes de estado para la publicación. Este parámetro se utiliza para devolver solo las solicitudes de estado con una descripción que coincida con el valor proporcionado en la *Descripción*, donde las cadenas de caracteres coinciden con una cláusula [like &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md) .  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica una solicitud.|  
|**publicaciones**|**sysname**|Nombre de la publicación para la que se envía la solicitud de estado.|  
|**sent_date**|**datetime**|Fecha y hora en que se envía la solicitud de estado.|  
|**description**|**nvarchar(4000)**|Información definida por el usuario que se puede utilizar para identificar solicitudes de estado individuales.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_helppeerrequests** se usa en la replicación transaccional punto a punto.  
  
 **sp_helppeerrequests** se utiliza al restaurar una base de datos Publicada en una topología punto a punto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_helppeerrequests**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_deletepeerrequesthistory &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
