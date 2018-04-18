---
title: Sys.sp_rda_set_query_mode (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a803ed67f498a04c56700129869140e3b8c4eda1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="syssprdasetquerymode-transact-sql"></a>sys.sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Especifica si las consultas realizadas en la base de datos habilitada para Stretch actual y sus tablas devuelven datos locales y remotos (valor predeterminado) o únicamente los datos locales.  
  
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
  
-   **LOCAL_ONLY** consultas en tablas habilitadas para Stretch devuelven únicamente los datos locales.  
  
-   **LOCAL_AND_REMOTE** consultas en tablas habilitadas para Stretch devuelven datos locales y remotos. Éste es el comportamiento predeterminado.  
  
 [ @force = ]  *@force*  
 Es un valor de bit opcional que puede establecer en 1 si desea cambiar el modo de consulta sin validación.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="permissions"></a>Permissions  
 Se requieren permisos db_owner.  
  
## <a name="remarks"></a>Comentarios  
 Los siguientes procedimientos almacenados extendidos también establece el modo de consulta para una base de datos habilitada para Stretch.  
  
-   **sp_rda_deauthorize_db**  
  
     Después de ejecutar **sp_rda_deauthorize_db** , se producirá un error en todas las consultas de bases de datos habilitadas para Stretch y tablas. Es decir, el modo de consulta se establece en deshabilitado. Para salir de este modo, realice una de las siguientes acciones.  
  
    -   Ejecutar [sys.sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectarse a la base de datos de Azure remota. Esta operación restablece automáticamente el modo de consulta a LOCAL_AND_REMOTE, que es el comportamiento predeterminado para la base de datos de Stretch. Es decir, las consultas devuelven resultados de datos locales y remotos.  
  
    -   Ejecutar [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) con el argumento LOCAL_ONLY para permitir que las consultas continúe que se ejecutarán únicamente los datos locales.  
  
-   **sp_rda_reauthorize_db**  
  
     Al ejecutar [sys.sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectarse a la base de datos de Azure remota, esta operación restablece automáticamente el modo de consulta a LOCAL_AND_REMOTE, que es el comportamiento predeterminado para Ajustar la base de datos. Es decir, las consultas devuelven resultados de datos locales y remotos.  
  
## <a name="see-also"></a>Vea también  
 [sys.sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
