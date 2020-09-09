---
description: sp_helppeerresponses (Transact-SQL)
title: sp_helppeerresponses (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerresponses_TSQL
- sp_helppeerresponses
helpviewer_keywords:
- sp_helppeerresponses
ms.assetid: e55789d1-43fb-4a37-9e5e-60ccef122a5d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1b3918d773984223c450e11ead71d045bf21db6d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535135"
---
# <a name="sp_helppeerresponses-transact-sql"></a>sp_helppeerresponses (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve todas las respuestas a una solicitud de estado específica recibida de un participante en una topología de replicación punto a punto, donde la solicitud se inició ejecutando [sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) en cualquier base de datos Publicada en la topología. Este procedimiento almacenado se ejecuta en la base de datos de publicación, en un publicador que participa en una topología de replicación punto a punto. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @request_id = ] request_id` Es el identificador de una solicitud de estado específica. *request_id* es de **tipo int**y no tiene ningún valor predeterminado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id_de_solicitud**|**int**|Id. de la solicitud de estado.|  
|**personas**|**sysname**|Nombre del elemento del mismo nivel que generó la respuesta.|  
|**peer_db**|**sysname**|Nombre de la base de datos del mismo nivel que generó la respuesta.|  
|**received_date**|**datetime**|Fecha y hora cuando el solicitante recibió la respuesta del elemento del mismo nivel que la envió.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_helppeerresponses** se usa en la replicación transaccional punto a punto.  
  
 **sp_helppeerresponses** procedimiento se utiliza al restaurar una base de datos Publicada en una topología punto a punto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_helppeerresponses**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_deletepeerrequesthistory &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
