---
title: Modificar tipo de mensaje (Transact-SQL) | Documentos de Microsoft
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
- ALTER_MESSAGE_TYPE_TSQL
- ALTER MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER MESSAGE TYPE statement
- modifying message types
- message types [Service Broker], modifying
ms.assetid: 98c94176-2bdf-4725-b4bc-d33b6b14817d
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ed67afafb33faa22ececbea51c1ed502b1e5725
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-message-type-transact-sql"></a>ALTER MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de un tipo de mensaje.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER MESSAGE TYPE message_type_name  
   VALIDATION =  
    {  NONE   
     | EMPTY   
     | WELL_FORMED_XML   
     | VALID_XML WITH SCHEMA COLLECTION schema_collection_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *message_type_name*  
 Es el nombre del tipo de mensaje que se va a cambiar. No se pueden especificar nombres de servidor, base de datos o esquema.  
  
 VALIDATION   
 Especifica cómo [!INCLUDE[ssSB](../../includes/sssb-md.md)] valida el cuerpo del mensaje para mensajes de este tipo.  
  
 Ninguno  
 No se realiza ninguna validación. El cuerpo del mensaje puede contener cualquier dato o tener un valor NULL.  
  
 EMPTY  
 El cuerpo del mensaje debe tener un valor NULL.  
  
 WELL_FORMED_XML   
 El cuerpo del mensaje debe contener XML correcto.  
  
 VALID_XML_WITH_SCHEMA = *schema_collection_name*  
 El cuerpo del mensaje debe contener XML que cumpla con el esquema de la colección de esquemas especificada. El *schema_collection_name* debe ser el nombre de una colección de esquemas XML.  
  
## <a name="remarks"></a>Comentarios  
 El cambio de la validación de un tipo de mensaje no afecta a los mensajes que ya se han entregado a una cola.  
  
 Para modificar AUTHORIZATION para un tipo de mensaje, utilice la instrucción ALTER AUTHORIZATION.  
  
## <a name="permissions"></a>Permissions  
 Permiso para modificar un tipo de mensaje predeterminado es el propietario del tipo de mensaje, los miembros de la **db_ddladmin** o **db_owner** se han corregido los roles de base de datos y los miembros de la **sysadmin**rol fijo de servidor.  
  
 Si la instrucción ALTER MESSAGE TYPE especifica una colección de esquemas, el usuario que ejecuta la instrucción debe tener el permiso REFERENCES en la colección de esquemas especificada.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia el tipo de mensaje `//Adventure-Works.com/Expenses/SubmitExpense` para que requiera que el cuerpo del mensaje contenga un documento XML correcto.  
  
```  
ALTER MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = WELL_FORMED_XML ;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Crear tipo de mensaje &#40; Transact-SQL &#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [Eliminar tipo de mensaje &#40; Transact-SQL &#41;](../../t-sql/statements/drop-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
