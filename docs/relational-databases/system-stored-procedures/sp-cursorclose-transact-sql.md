---
title: sp_cursorclose (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bb3db5049ff370a9dccad98dd7e90efb2e346f0f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cierra y desasigna el cursor, así como libera todos los recursos asociados; es decir, quita la tabla temporal que se usa para admitir KEYSET o STATIC **cursor**. sp_cursorclose se invoca especificando el identificador = 9 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 Es un cursor *controlar* valor generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y devuelto por el procedimiento sp_cursoropen. *cursor* es un parámetro necesario que requiere un **int** valor de entrada.  
  
> [!NOTE]  
>  El valor de entrada -1 se aplicará en todos los cursores de la conexión actual.  
  
## <a name="remarks"></a>Comentarios  
 *cursor* devolverá mensajes de error si se ha ejecutado el procedimiento después de que se ha cerrado el cursor o si se especifica un identificador no válido.  
  
 El estado de la RPC indica el éxito o error general.  
  
 El número de filas DONE siempre es 0.  
  
## <a name="see-also"></a>Vea también  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
