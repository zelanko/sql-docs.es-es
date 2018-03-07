---
title: ALTER BROKER PRIORITY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_BROKER_TSQL
- ALTER BROKER PRIORITY
- ALTER BROKER
- ALTER_BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER BROKER PRIORITY statement
- ssbdiagnose
ms.assetid: 15fda1b2-e4dd-4f9d-935a-2e38926075b2
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 833c0bed38d02905b3a260f50824825c9859484f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="alter-broker-priority-transact-sql"></a>ALTER BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de una prioridad de conversación de [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
{ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = { PriorityValue | DEFAULT } ]  
              )  
}  
[;]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConversationPriorityName*  
 Especifica el nombre de la prioridad de conversación que se va a modificar. El nombre debe hacer referencia a una prioridad de conversación de la base de datos actual.  
  
 SET  
 Especifica los criterios para determinar si la prioridad de conversación se aplica a una conversación. SET es necesario y debe incluir al menos un criterio: CONTRACT_NAME, LOCAL_SERVICE_NAME, REMOTE_SERVICE_NAME o PRIORITY_LEVEL.  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 Especifica el nombre de un contrato que se va a usar como criterio para determinar si la prioridad de conversación se aplica a una conversación. *ContractName* es un [!INCLUDE[ssDE](../../includes/ssde-md.md)] identificador y debe especificar el nombre de un contrato de la base de datos actual.  
  
 *ContractName*  
 Especifica que la prioridad de conversación se puede aplicar solo a las conversaciones que la instrucción BEGIN DIALOG que inició la conversación especificó ON CONTRACT *ContractName*.  
  
 ANY  
 Especifica que la prioridad de conversación se puede aplicar a cualquier conversación, independientemente de qué contrato use.  
  
 Si no se especifica CONTRACT_NAME, la propiedad de contrato de la prioridad de conversación no se modifica.  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 Especifica el nombre de un servicio que se va a usar como criterio para determinar si la prioridad de conversación se aplica a un extremo de una conversación.  
  
 *LocalServiceName* es un [!INCLUDE[ssDE](../../includes/ssde-md.md)] identificador y debe especificar el nombre de un servicio en la base de datos actual.  
  
 *LocalServiceName*  
 Especifica que la prioridad de conversación se puede aplicar a lo siguiente:  
  
-   Cualquier extremo iniciador de conversación cuyo nombre de servicio iniciador coincida con *LocalServiceName*.  
  
-   Cualquier extremo de conversación de destino cuyo nombre de servicio de destino coincide con *LocalServiceName*.  
  
 ANY  
 -   Especifica que la prioridad de conversación se puede aplicar a cualquier extremo de conversación, independientemente del nombre del servicio local utilizado por el extremo.  
  
 Si no se especifica LOCAL_SERVICE_NAME, la propiedad de servicio local de la prioridad de conversación no se modifica.  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 Especifica el nombre de un servicio que se va a usar como criterio para determinar si la prioridad de conversación se aplica a un extremo de una conversación.  
  
 *RemoteServiceName* es un literal de tipo **nvarchar (256)**. [!INCLUDE[ssSB](../../includes/sssb-md.md)]utiliza una comparación byte a byte para que coincida con el *RemoteServiceName* cadena. En la comparación se distinguen mayúsculas y minúsculas, y no se considera la intercalación actual. El servicio de destino puede estar en la instancia actual de [!INCLUDE[ssDE](../../includes/ssde-md.md)] o en una instancia remota de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 '*RemoteServiceName*'  
 Especifica la prioridad de conversación que se va a asignar a:  
  
-   Cualquier extremo iniciador de conversación cuyo nombre de servicio de destino asociado coincida con *RemoteServiceName*.  
  
-   Cualquier extremo de conversación de destino cuyo nombre de servicio iniciador asociado coincida con *RemoteServiceName*.  
  
 ANY  
 Especifica que la prioridad de conversación se aplica a cualquier extremo de conversación, independientemente del nombre del servicio remoto asociado al extremo.  
  
 Si no se especifica REMOTE_SERVICE_NAME, la propiedad de servicio remoto de la prioridad de conversación no se modifica.  
  
 Valor de PRIORITY_LEVEL = { *PriorityValue* | **predeterminado** }  
 Especifica el nivel de prioridad que se asigna a cualquier extremo de conversación que utilice los contratos y servicios especificados en la prioridad de conversación. *PriorityValue* debe ser un entero literal de 1 (prioridad más baja) y 10 (prioridad más alta).  
  
 Si no se especifica PRIORITY_LEVEL, la propiedad de nivel de prioridad no se modifica.  
  
## <a name="remarks"></a>Comentarios  
 Ninguna de las propiedades modificadas por ALTER BROKER PRIORITY se aplica a las conversaciones existentes. Las conversaciones existentes continúan con la prioridad que les fue asignada cuando se iniciaron.  
  
 Para obtener más información, vea [CREATE BROKER PRIORITY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-broker-priority-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Permiso para crear una prioridad de conversación de forma predeterminada a los miembros de la **db_ddladmin** o **db_owner** funciones fijas de base de datos y a la **sysadmin** rol fijo de servidor. Requiere el permiso ALTER en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-only-the-priority-level-of-an-existing-conversation-priority"></a>A. Cambiar solo el nivel de prioridad de una prioridad de conversación existente.  
 Cambia el nivel de prioridad, pero no cambia las propiedades del servicio remoto, el contrato o el servicio local.  
  
```  
ALTER BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-changing-all-of-the-properties-of-an-existing-conversation-priority"></a>B. Cambiar todas las propiedades de una prioridad de conversación existente.  
 Cambia las propiedades de servicio remotas, nivel de prioridad, contrato, servicio local.  
  
```  
ALTER BROKER PRIORITY SimpleContractPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContractB,  
         LOCAL_SERVICE_NAME = TargetServiceB,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceB',  
         PRIORITY_LEVEL = 8);  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
