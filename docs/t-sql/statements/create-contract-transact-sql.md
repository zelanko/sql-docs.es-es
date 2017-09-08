---
title: CREAR el contrato (Transact-SQL) | Documentos de Microsoft
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
- CONTRACT_TSQL
- CREATE_CONTRACT_TSQL
- CREATE CONTRACT
- CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE CONTRACT statement
- contracts [Service Broker], creating
- message types [Service Broker], contracts
ms.assetid: 494cbfa6-8e93-4161-a64d-90d681915211
caps.latest.revision: 48
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 962ce2d6568a597bd580f7fc9bcd2e9243e44dc4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-contract-transact-sql"></a>CREATE CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuevo contrato. Un contrato define los tipos de mensaje usados en una conversación de [!INCLUDE[ssSB](../../includes/sssb-md.md)] y también determina qué lado de la conversación puede enviar mensajes de ese tipo. Cada conversación obedece a un contrato. El servicio iniciador especifica el contrato para la conversación cuando se inicia la conversación. El servicio de destino especifica los contratos que el servicio de destino acepta para conversaciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE CONTRACT contract_name  
   [ AUTHORIZATION owner_name ]  
      (  {   { message_type_name | [ DEFAULT ] }  
          SENT BY { INITIATOR | TARGET | ANY }   
       } [ ,...n] )   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *contract_name*  
 Es el nombre del contrato que se va a crear. Se crea un contrato nuevo en la base de datos actual, que pertenece a la entidad de seguridad especificada en la cláusula AUTHORIZATION. No se pueden especificar nombres de servidor, base de datos o esquema. El *contract_name* puede tener hasta 128 caracteres.  
  
> [!NOTE]  
>  No cree un contrato que utiliza la palabra clave ANY para la *contract_name*. Cuando especifica ANY para un nombre de contrato en CREATE BROKER PRIORITY, la prioridad se considera para todos los contratos. No se limita a un contrato cuyo nombre sea ANY.  
  
 AUTORIZACIÓN *owner_name*  
 Establece el propietario del contrato en el usuario o el rol de base de datos que se ha especificado. Cuando el usuario actual es **dbo** o **sa**, *owner_name* puede ser el nombre de cualquier usuario o rol válidos. En caso contrario, *owner_name* debe ser el nombre del usuario actual, el nombre de un usuario que el usuario actual tiene permisos de suplantación o el nombre de un rol al que pertenece el usuario actual. Si se omite esta cláusula, el contrato pertenece al usuario actual.  
  
 *message_type_name*  
 Es el nombre de un tipo de mensaje que se incluirá como parte del contrato.  
  
 SENT BY  
 Especifica qué extremo puede enviar un mensaje del tipo de mensaje indicado. Los contratos documentan los mensajes que pueden usar los servicios para tener determinadas conversaciones. Cada conversación tiene dos extremos: el *iniciador* punto de conexión, el servicio que se inició la conversación, y el *destino* punto de conexión, el servicio que se pone en contacto el iniciador.  
  
 INITIATOR  
 Indica que solo el iniciador de la conversación puede enviar mensajes del tipo especificado. Un servicio que se inicia una conversación se conoce como el *iniciador* de la conversación.  
  
 TARGET  
 Indica que solo el destino de la conversación puede enviar mensajes del tipo especificado. Un servicio que acepta una conversación que inició otro servicio se conoce como el *destino* de la conversación.  
  
 ANY  
 Indica que los mensajes de este tipo se pueden enviar por el iniciador y el destino.  
  
 [DEFAULT]  
 Indica que este contrato admite mensajes del tipo predeterminado. De forma predeterminada, todas las bases de datos contienen un tipo de mensaje denominado DEFAULT. Este tipo de mensaje usa una validación de NONE. En el contexto de esta cláusula, DEFAULT no es una palabra clave y debe delimitarse como un identificador. Microsoft SQL Server también proporciona un contrato DEFAULT que especifica el tipo de mensaje DEFAULT.  
  
## <a name="remarks"></a>Comentarios  
 El orden de los tipos de mensaje del contrato no es significativo. Después de que el destino haya recibido el primer mensaje, [!INCLUDE[ssSB](../../includes/sssb-md.md)] permite a cualquier lado de la conversación enviar los mensajes permitidos para ese lado de la conversación en cualquier momento. Por ejemplo, si el iniciador de la conversación puede enviar el tipo de mensaje **//Adventure-Works.com/Expenses/SubmitExpense**, [!INCLUDE[ssSB](../../includes/sssb-md.md)] permite al iniciador enviar cualquier número de **SubmitExpense**mensajes durante la conversación.  
  
 Los tipos de mensaje y direcciones de un contrato no se pueden cambiar. Para cambiar AUTHORIZATION para un contrato, utilice la instrucción ALTER AUTHORIZATION.  
  
 Un contrato debe permitir al iniciador enviar un mensaje. La instrucción CREATE CONTRACT genera errores cuando el contrato no contiene al menos un tipo de mensaje SENT BY ANY o SENT BY INITIATOR.  
  
 Independientemente del contrato, un servicio siempre puede recibir los tipos de mensaje `http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`, `http://schemas.microsoft.com/SQL/ServiceBroker/Error`, y `http://schemas.microsoft.com/SQL/ServiceBroker/EndDialog`. [!INCLUDE[ssSB](../../includes/sssb-md.md)] utiliza estos tipos de mensaje para los mensajes del sistema con destino a la aplicación.  
  
 Un contrato no puede ser un objeto temporal. Se permiten los nombres de contrato que empiezan por #, aunque se trata de objetos permanentes.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros de la **db_ddladmin** o **db_owner** funciones fijas de base de datos y la **sysadmin** rol fijo de servidor puede crear contratos.  
  
 De forma predeterminada, el propietario del contrato, los miembros de la **db_ddladmin** o **db_owner** se han corregido los roles de base de datos y los miembros de la **sysadmin** rol fijo de servidor tienen referencias permiso en un contrato.  
  
 El usuario que ejecuta la instrucción CREATE CONTRACT debe tener permiso REFERENCES en todos los tipos de mensaje especificados.  
  
## <a name="examples"></a>Ejemplos  
 **A. Creación de un contrato**  
  
 En el siguiente ejemplo se crea un contrato de reembolso de gastos basándose en tres tipos de mensaje.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE           
    [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
    VALIDATION= WELL_FORMED_XML ;           
  
CREATE CONTRACT            
    [//Adventure-Works.com/Expenses/ExpenseSubmission]           
    ( [//Adventure-Works.com/Expenses/SubmitExpense]           
          SENT BY INITIATOR,           
      [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
          SENT BY TARGET,           
      [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
          SENT BY TARGET           
    ) ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Eliminar contrato &#40; Transact-SQL &#41;](../../t-sql/statements/drop-contract-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
