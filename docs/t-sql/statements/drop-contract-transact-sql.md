---
title: DROP CONTRACT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_CONTRACT_TSQL
- DROP CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- dropping contracts
- removing contracts
- deleting contracts
- contracts [Service Broker], dropping
- DROP CONTRACT statement
ms.assetid: fdd0f81e-3c22-4cdf-9416-b4977a6ac3b6
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 60c390e778210c83df5e18fee974d1818356aab5
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
ms.locfileid: "33700048"
---
# <a name="drop-contract-transact-sql"></a>DROP CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un contrato existente de una base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP CONTRACT contract_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *contract_name*  
 Nombre del contrato que se va a quitar. No se pueden especificar nombres de servidor, base de datos o esquema.  
  
## <a name="remarks"></a>Notas  
 No se puede quitar un contrato si hay servicios o prioridades de conversación que hacen referencia a él.  
  
 Al quitar un contrato, [!INCLUDE[ssSB](../../includes/sssb-md.md)] finaliza con un error las conversaciones existentes que lo utilizan.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, el permiso para quitar un contrato corresponde al propietario del contrato, a los miembros de los roles fijos de base de datos db_ddladmin o db_owner, y a los miembros del rol fijo de servidor sysadmin.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se quita el contrato `//Adventure-Works.com/Expenses/ExpenseSubmission` de la base de datos.  
  
```  
DROP CONTRACT   
    [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
## <a name="see-also"></a>Ver también  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [ALTER SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [CREATE CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
