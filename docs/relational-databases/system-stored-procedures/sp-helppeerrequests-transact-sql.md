---
title: sp_helppeerrequests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba660dbcaf09b3df5890032ab0f1b428cce7860e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028105"
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre todas las solicitudes de estado recibidas por los participantes en una topología de replicación punto a punto, donde estas solicitudes se iniciaron ejecutando [sp_requestpeerresponse &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) en cualquier base de datos publicada en la topología. Este procedimiento almacenado se ejecuta en la base de datos de publicación, en un publicador que participa en una topología de replicación punto a punto. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication**=] **'***publicación***'**  
 Es el nombre de la publicación de una topología punto a punto para la que se han enviado solicitudes de estado. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@description**=] **'***descripción***'**  
 Valor que se puede usar para identificar solicitudes de estado individuales, lo que permite filtrar las respuestas devueltas en función de usuario define la información proporcionada al llamar a [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). *descripción* es **nvarchar (4000)**, su valor predeterminado es **%**. De forma predeterminada, se devuelven todas las solicitudes de estado para la publicación. Este parámetro se usa para devolver sólo las solicitudes de estado con una descripción que coincide con el valor proporcionado en *descripción*, donde se comparan las cadenas de caracteres con un [como &#40;Transact-SQL&#41; ](../../t-sql/language-elements/like-transact-sql.md)cláusula.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica una solicitud.|  
|**publicación**|**sysname**|Nombre de la publicación para la que se envía la solicitud de estado.|  
|**sent_date**|**datetime**|Fecha y hora en que se envía la solicitud de estado.|  
|**Descripción**|**nvarchar(4000)**|Información que puede usarse para identificar las solicitudes de estado individuales definidas por el usuario.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_helppeerrequests** se utiliza en la replicación transaccional punto a punto.  
  
 **sp_helppeerrequests** se utiliza al restaurar una base de datos publicada en una topología punto a punto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_helppeerrequests**.  
  
## <a name="see-also"></a>Vea también  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
