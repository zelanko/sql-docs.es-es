---
title: sp_gettopologyinfo (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d2a9e5031460c478806aacc9e7d97de593ee613
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spgettopologyinfo-transact-sql"></a>sp_gettopologyinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre una topología de replicación transaccional punto a punto. Ejecutar [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) para recopilar información antes de ejecutar este procedimiento.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @request_id=] *request_id*  
 Es el identificador de una solicitud de estado de topología. *request_id* es **int**, su valor predeterminado es null. Para obtener un identificador, utilice la @request_id desde el parámetro de salida [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) o consultar la [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) tabla del sistema.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 sp_gettopologyinfo devuelve un conjunto de resultados que tiene una única columna XML. Los datos de la columna XML están el mismo que los datos de la [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabla del sistema.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_gettopologyinfo se utiliza en la replicación transaccional punto a punto. Ejecutar [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) antes de ejecutar sp_gettopologyinfo. El Asistente de configuración de la topología punto a punto utiliza estos procedimientos, pero también se pueden utilizar directamente si se requiere información de la topología en formato XML. Si prefiere resultados tabulares, consultar la [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabla del sistema.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol fijo de servidor sysadmin o al rol fijo de base de datos db_owner.  
  
## <a name="see-also"></a>Vea también  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  (Replicación transaccional punto a punto)  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
