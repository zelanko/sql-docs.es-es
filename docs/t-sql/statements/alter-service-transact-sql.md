---
title: ALTER SERVICE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SERVICE
- ALTER_SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying services
- contracts [Service Broker], modifying
- ALTER SERVICE statement
- services [Service Broker], modifying
ms.assetid: 2b4608f7-bb2e-4246-aa29-b52c55995b3a
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0f09a018648566cd928258da958bb06dedc6022
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-service-transact-sql"></a>ALTER SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia un servicio existente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER SERVICE service_name   
   [ ON QUEUE [ schema_name . ]queue_name ]   
   [ ( < opt_arg > [ , ...n ] ) ]  
[ ; ]  
  
<opt_arg> ::=  
   ADD CONTRACT contract_name | DROP CONTRACT contract_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *SERVICE_NAME*  
 Es el nombre del servicio que se va a cambiar. No se pueden especificar nombres de servidor, base de datos o esquema.  
  
 COLA de ON [ *schema_name***.** ] *nombre_de_cola*  
 Especifica la nueva cola para este servicio. [!INCLUDE[ssSB](../../includes/sssb-md.md)] mueve todos los mensajes correspondientes a este servicio de la cola actual a la nueva.  
  
 Agregar contrato *contract_name*  
 Especifica un contrato que se agregará al conjunto de contratos expuesto por este servicio.  
  
 DROP CONTRACT *contract_name*  
 Especifica un contrato que se eliminará del conjunto de contratos expuesto por este servicio. [!INCLUDE[ssSB](../../includes/sssb-md.md)] envía un mensaje de error si hay conversaciones existentes con este servicio que utilicen este contrato.  
  
## <a name="remarks"></a>Comentarios  
 Cuando la instrucción ALTER SERVICE elimina un contrato de un servicio, este último no puede ser el destino de conversaciones que utilicen ese contrato. Por tanto, [!INCLUDE[ssSB](../../includes/sssb-md.md)] no permite que se establezcan conversaciones nuevas con el servicio basadas en ese contrato. Las conversaciones existentes que utilizan el contrato no se ven afectadas.  
  
 Para modificar AUTHORIZATION para un servicio, utilice la instrucción ALTER AUTHORIZATION.  
  
## <a name="permissions"></a>Permissions  
 Permiso para modificar un servicio de forma predeterminada el propietario del servicio, los miembros de la **db_ddladmin** o **db_owner** se han corregido los roles de base de datos y los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-queue-for-a-service"></a>A. Cambiar la cola para un servicio  
 En el ejemplo siguiente se cambia el servicio de `//Adventure-Works.com/Expenses` para que utilice la cola `NewQueue`.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE NewQueue ;  
```  
  
### <a name="b-adding-a-new-contract-to-the-service"></a>B. Agregar un nuevo contrato al servicio  
 En el ejemplo siguiente se cambia el servicio de `//Adventure-Works.com/Expenses` para que permita diálogos en el contrato de `//Adventure-Works.com/Expenses`.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="c-adding-a-new-contract-to-the-service-dropping-existing-contract"></a>C. Agregar un nuevo contrato al servicio, quitando el contrato existente  
 En el ejemplo siguiente se cambia el servicio de `//Adventure-Works.com/Expenses` para que permita diálogos en el contrato `//Adventure-Works.com/Expenses/ExpenseProcessing` y no los permita en el contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing],   
     DROP CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [Eliminar servicio &#40; Transact-SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

