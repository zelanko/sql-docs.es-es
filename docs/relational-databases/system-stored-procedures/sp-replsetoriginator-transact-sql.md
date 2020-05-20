---
title: sp_replsetoriginator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5e1f29f06d7a840ed6628ecd4dc193a4f1c54b82
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82817095"
---
# <a name="sp_replsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Se utiliza para invocar la detección y control de bucles invertidos en la replicación transaccional bidireccional. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'server_name'`Es el nombre del servidor donde se aplica la transacción. *originating_server* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @database_name = ] 'database_name'`Es el nombre de la base de datos donde se aplica la transacción. *originating_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 el Agente de distribución ejecuta **sp_replsetoriginator** para registrar el origen de las transacciones aplicadas por la replicación. Esta información se utiliza para invocar la detección de bucles invertidos en suscripciones transaccionales bidireccionales que tienen establecida la propiedad de bucles invertidos.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** en el publicador, los miembros del rol fijo de base de datos **db_owner** en la base de datos de publicación o los usuarios de la lista de acceso a la publicación (PAL) pueden ejecutar **sp_replsetoriginator**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
