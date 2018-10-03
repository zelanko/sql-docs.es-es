---
title: Sys.sp_rda_set_query_mode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c6b2fd8fd64bd8d7df6429a21c3f27266657964e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740553"
---
# <a name="syssprdasetquerymode-transact-sql"></a>sys.sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Especifica si las consultas en la base de datos habilitadas para Stretch actual y sus tablas devuelven datos locales y remotos (el valor predeterminado) o únicamente los datos locales.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @mode = ] *@mode*  
 Es uno de los siguientes valores.  
  
-   **DESHABILITADO** producirá un error en todas las consultas en tablas habilitadas para Stretch.  
  
-   **LOCAL_ONLY** las consultas en tablas habilitadas para Stretch devuelven únicamente los datos locales.  
  
-   **LOCAL_AND_REMOTE** las consultas en tablas habilitadas para Stretch devuelven datos locales y remotos. Éste es el comportamiento predeterminado.  
  
 [ @force = ]  *@force*  
 Es un valor de bits opcional que puede establecer en 1 si desea cambiar el modo de consulta sin validación.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="permissions"></a>Permisos  
 Se requieren permisos db_owner.  
  
## <a name="remarks"></a>Comentarios  
 Los siguientes procedimientos almacenados extendidos también establecer el modo de consulta para una base de datos habilitadas para Stretch.  
  
-   **sp_rda_deauthorize_db**  
  
     Después de ejecutar **sp_rda_deauthorize_db** , producirá un error en todas las consultas en tablas y bases de datos habilitadas para Stretch. Es decir, el modo de consulta está establecido en deshabilitado. Para salir de este modo, realice una de las siguientes acciones.  
  
    -   Ejecute [sys.sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectarse a la base de datos de Azure remota. Esta operación restablece automáticamente el modo de consulta LOCAL_AND_REMOTE, que es el comportamiento predeterminado para Stretch Database. Es decir, las consultas devuelven los resultados de datos locales y remotos.  
  
    -   Ejecute [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) con el argumento LOCAL_ONLY para permitir que las consultas continúan ejecutándose con solo los datos locales.  
  
-   **sp_rda_reauthorize_db**  
  
     Al ejecutar [sys.sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectarse a la base de datos de Azure remota, esta operación restablece automáticamente el modo de consulta LOCAL_AND_REMOTE, que es el comportamiento predeterminado para Stretch Database. Es decir, las consultas devuelven los resultados de datos locales y remotos.  
  
## <a name="see-also"></a>Vea también  
 [sys.sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
