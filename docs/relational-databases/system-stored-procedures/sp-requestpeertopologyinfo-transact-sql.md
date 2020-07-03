---
title: sp_requestpeertopologyinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeertopologyinfo
- sp_requestpeertopologyinfo_TSQL
helpviewer_keywords:
- sp_requestpeertopologyinfo
ms.assetid: 15cd28bd-5a72-41fb-ae1b-726baaa6fad5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c88b25976af9914d21ea4ee80d165e893360bdf0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899278"
---
# <a name="sp_requestpeertopologyinfo-transact-sql"></a>sp_requestpeertopologyinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Rellena la [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabla del sistema con información sobre una topología de replicación transaccional punto a punto. Ejecute [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md) para obtener información de la tabla en formato XML.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_requestpeertopologyinfo [ @publication = ] 'publication'  
        [ ,[ @requestid=] request_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication =] '*publicación*'  
 Es el nombre de la publicación para la que se realiza una solicitud del estado de toda la topología. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
 [ @request_id =] *request_id*  
 Es el número de identificación que está asignado a la solicitud del estado de la topología. *request_id* es de **tipo int**y su valor predeterminado es NULL. [Sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md)puede usar este identificador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_requestpeertopologyinfo se utiliza en la replicación transaccional punto a punto. Ejecute sp_requestpeertopologyinfo antes de ejecutar [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md). El Asistente de configuración de la topología punto a punto utiliza estos procedimientos, pero también se pueden utilizar directamente si se requiere información de la topología en formato XML. Si prefiere resultados tabulares, consulte la tabla del sistema [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) .  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de servidor sysadmin o al rol fijo de base de datos db_owner.  
  
## <a name="see-also"></a>Consulte también  
 [Replicación transaccional punto a punto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
