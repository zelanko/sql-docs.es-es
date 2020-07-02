---
title: sp_cursorclose (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b2a0f6f23d38cb0841ba6e1b7891d9d32fc95b1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646261"
---
# <a name="sp_cursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Cierra y desasigna el cursor, además de liberar todos los recursos asociados; es decir, quita la tabla temporal utilizada para admitir el conjunto de claves o el **cursor**estático. sp_cursorclose se invoca especificando el identificador 9 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 Es un valor de *identificador* de cursor generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y devuelto por el procedimiento Sp_cursoropen. *cursor* es un parámetro necesario que requiere un valor de entrada **int** .  
  
> [!NOTE]  
>  El valor de entrada -1 se aplicará en todos los cursores de la conexión actual.  
  
## <a name="remarks"></a>Comentarios  
 el *cursor* devolverá mensajes de error si el procedimiento se ejecutó después de que el cursor se hubiera cerrado o si se especifica un identificador no válido.  
  
 El estado de la RPC indica el éxito o error general.  
  
 El número de filas DONE siempre es 0.  
  
## <a name="see-also"></a>Consulte también  
 [sp_cursoropen &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
