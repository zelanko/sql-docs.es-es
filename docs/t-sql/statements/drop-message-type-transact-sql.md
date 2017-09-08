---
title: QUITAR el tipo de mensaje (Transact-SQL) | Documentos de Microsoft
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
- DROP_MESSAGE_TYPE_TSQL
- DROP MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- message types [Service Broker], removing
- deleting message types
- dropping message types
- DROP MESSAGE TYPE statement
- removing message types
ms.assetid: 805e8ad5-8a93-49f0-88e5-e6fca8814dd5
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 859419b6809d1c44486130eadaf30c1411a03b97
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-message-type-transact-sql"></a>DROP MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un tipo de mensaje existente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP MESSAGE TYPE message_type_name  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *message_type_name*  
 Es el nombre del tipo de mensaje que se va a eliminar. No se pueden especificar nombres de servidor, base de datos o esquema.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, se concede permiso para quitar un tipo de mensaje al propietario del tipo de mensaje, a los miembros de los roles fijos de base de datos ddl_admin o db_owner y a los miembros del rol fijo de servidor sysadmin.  
  
## <a name="remarks"></a>Comentarios  
 No puede quitar un tipo de mensaje si algún contrato hace referencia al tipo de mensaje.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente elimina el tipo de mensaje `//Adventure-Works.com/Expenses/SubmitExpense` de la base de datos.  
  
```  
DROP MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense] ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Modificar tipo de mensaje &#40; Transact-SQL &#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [Crear tipo de mensaje &#40; Transact-SQL &#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
