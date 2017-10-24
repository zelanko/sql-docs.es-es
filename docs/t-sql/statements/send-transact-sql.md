---
title: "ENVÍO (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SEND_ON_CONVERSATION_TSQL
- ON_CONVERSATION_TSQL
- SEND
- SEND_TSQL
- SEND ON CONVERSATION
- ON CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], message sending
- SEND statement
- messages [Service Broker], sending
- sending messages
ms.assetid: b6e66aeb-1714-4c2b-b7c2-d386d77b0d46
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b149c44df4fb417ed143147cd38b4ae838318ece
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="send-transact-sql"></a>SEND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Envía un mensaje utilizando una o varias conversaciones existentes.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SEND  
   ON CONVERSATION [(]conversation_handle [,.. @conversation_handle_n][)]  
   [ MESSAGE TYPE message_type_name ]  
   [ ( message_body_expression ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 EN la conversación *conversation_handle [.. @conversation_handle_n]*  
 Especifica las conversaciones a las que pertenece el mensaje. El *conversation_handle* debe contener un identificador de conversación válido. El mismo identificador de conversación no se puede utilizar más de una vez.  
  
 TIPO de mensaje *message_type_name*  
 Especifica el tipo de mensaje enviado. Este tipo de mensaje se debe incluir en los contratos de servicio que utilizan estas conversaciones. Estos contratos deben permitir que el tipo de mensaje se envíe desde este lado de la conversación. Por ejemplo, es posible que los servicios de destino de las conversaciones solo envíen mensajes especificados en el contrato como SENT BY TARGET o SENT BY ANY. Si se omite esta cláusula, el mensaje es de tipo DEFAULT.  
  
 *message_body_expression*  
 Proporciona una expresión que representa el cuerpo del mensaje. El *message_body_expression* es opcional. Sin embargo, si la *message_body_expression* está presente la expresión debe ser de un tipo que pueda convertirse a **varbinary (max)**. La expresión no puede ser NULL. Si se omite esta cláusula, el cuerpo del mensaje está vacío.  
  
## <a name="remarks"></a>Comentarios  
  
> [!IMPORTANT]  
>  Si la instrucción SEND no es la primera instrucción de un lote o procedimiento almacenado, la instrucción anterior debe finalizar con un punto y coma (;).  
  
 La instrucción SEND transmite un mensaje desde los servicios en un extremo de una o varias conversaciones de [!INCLUDE[ssSB](../../includes/sssb-md.md)] a los servicios en el otro extremo de esas conversaciones. A continuación, la instrucción RECEIVE se utiliza para recuperar el mensaje enviado desde las colas asociadas a los servicios de destino.  
  
 Los identificadores de conversación proporcionados a la cláusula ON CONVERSATION proceden de uno de estos tres orígenes:  
  
-   Al enviar un mensaje que no es la respuesta a un mensaje recibido de otro servicio, utilice el identificador de conversación devuelto por la instrucción BEGIN DIALOG creado por la conversación.  
  
-   Al enviar un mensaje que es la respuesta a un mensaje previamente recibido de otro servicio, utilice el identificador de conversación devuelto por la instrucción RECEIVE que devolvió el mensaje original.  
  
 En muchos casos, el código que contiene la instrucción SEND es independiente del código que contiene instrucciones del BEGIN DIALOG o RECEIVE proporcionando el identificador de conversación. En estos casos, el identificador de conversación debe ser uno de los elementos de datos de la información de estado que se pasa al código que contiene la instrucción SEND.  
  
 Los mensajes que se envían a servicios de otras instancias de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] se almacenan en una cola de transmisión de la base de datos actual hasta que se puedan transmitir a las colas de servicio de las instancias remotas. Los mensajes enviados a servicios de la misma instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] se colocan directamente en las colas asociadas con esos servicios. Si una condición impide que un mensaje local se coloque en la cola del servicio de destino directamente, se puede almacenar en la cola de transmisión hasta que se resuelva la condición. Por ejemplo, esto se produce en algunos tipos de errores o cuando la cola del servicio de destino está inactiva. Puede usar el **sys.transmission_queue** vista del sistema para ver los mensajes en la cola de transmisión.  
  
 SEND es una instrucción atómica, es decir, si se produce un error en una instrucción SEND que envía un mensaje en varias conversaciones (por ejemplo, porque una conversación está en un estado de error), no se almacena ningún mensaje en la cola de transmisión ni tampoco se pone en ninguna cola de servicio de destino.  
  
 Service Broker optimizar el almacenamiento y la transmisión de los mensajes que se envían en varias conversaciones en la misma instrucción SEND.  
  
 Los mensajes de las colas de transmisión para una instancia se transmiten en secuencia según:  
  
-   El nivel de prioridad de su extremo de conversación asociado.  
  
-   Dentro del nivel de prioridad, su secuencia de envío en la conversación.  
  
 Los niveles de prioridad especificados en prioridades de conversación solo se aplican a los mensajes de la cola de transmisión si la opción de la base de datos HONOR_BROKER_PRIORITY está establecida en ON. Si HONOR_BROKER_PRIORITY está establecida en OFF, todos los mensajes colocados en la cola de transmisión para esa base de datos tendrán asignado el nivel de prioridad predeterminado de 5. Los niveles de prioridad no se aplican a una instrucción SEND en la que los mensajes se colocan directamente en una cola de servicio de la misma instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 La instrucción SEND bloquea por separado cada conversación en la que se envía un mensaje a fin de asegurarse de que se produzca una entrega por conversación ordenada.  
  
 SEND no tiene validez en una función definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Para enviar un mensaje, el usuario actual debe tener el permiso RECEIVE en la cola de cada servicio que envía el mensaje.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se inicia un diálogo y se envía un mensaje XML en el diálogo. Para enviar el mensaje, en el ejemplo se convierte el objeto de xml en **varbinary (max)**.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ExpenseReport XML ;  
  
SET @ExpenseReport = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle  
FROM SERVICE [//Adventure-Works.com/Expenses/ExpenseClient]  
TO SERVICE '//Adventure-Works.com/Expenses'  
ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing] ;  
  
SEND ON CONVERSATION @dialog_handle  
    MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense]  
    (@ExpenseReport) ;  
```  
  
 En el siguiente ejemplo se inician tres diálogos y se envía un mensaje XML en cada uno de ellos.  
  
```  
DECLARE @dialog_handle1 UNIQUEIDENTIFIER,  
        @dialog_handle2 UNIQUEIDENTIFIER,  
        @dialog_handle3 UNIQUEIDENTIFIER,  
        @OrderMsg XML ;  
  
SET @OrderMsg = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle1  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB1/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle2  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB2/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle3  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB3/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
SEND ON CONVERSATION (@dialog_handle1, @dialog_handle2, @dialog_handle3)  
    MESSAGE TYPE [//AllDBs/OrderMsg]  
    (@OrderMsg) ;  
```  
  
## <a name="see-also"></a>Vea también  
 [EMPEZAR conversación de diálogo &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [Finalizar conversación &#40; Transact-SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [RECIBIR &#40; Transact-SQL &#41;](../../t-sql/statements/receive-transact-sql.md)   
 [Sys.transmission_queue &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  

