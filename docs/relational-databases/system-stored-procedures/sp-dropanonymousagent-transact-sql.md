---
title: sp_dropanonymousagent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 8c9a025beaf1d9701411668a13fa78273105d30c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717328"
---
# <a name="sp_dropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Quita un agente anónimo de la supervisión de replicación en el distribuidor del publicador. Este procedimiento almacenado se ejecuta en el publicador de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @subid = ] sub_id`Es el identificador global de una suscripción anónima. *sub_id* es de tipo **uniqueidentifier**y no tiene ningún valor predeterminado. Este identificador se puede recuperar en el suscriptor mediante **sp_helppullsubscription**. El valor del campo **subid** del conjunto de resultados devuelto es este identificador global.  
  
`[ @type = ] type`Es el tipo de suscripción. el *tipo* es **int**y no tiene ningún valor predeterminado. Los valores válidos son **1** o **2**. Especifique **1**, si la replicación de instantáneas o la replicación transaccional utilizan el agente de distribución. Especifique **2**, si la replicación de mezcla utiliza el agente de mezcla.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropanonymousagent** se utiliza en todos los tipos de replicación.  
  
 Este procedimiento almacenado solo se utiliza para quitar agentes de suscripción anónima y no se puede utilizar para quitar suscripciones conocidas.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de base de datos **db_owner** en la base de datos de distribución pueden ejecutar **sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
