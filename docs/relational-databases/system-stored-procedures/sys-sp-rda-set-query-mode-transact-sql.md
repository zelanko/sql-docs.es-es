---
title: Sys. sp_rda_set_query_mode (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 06690f79bf2cc708a83ec272906b3f4be09fe03d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807841"
---
# <a name="syssp_rda_set_query_mode-transact-sql"></a>Sys. sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Especifica si las consultas realizadas en la base de datos habilitada para Stretch actual y en sus tablas devuelven datos locales y remotos (el valor predeterminado) o solo los datos locales.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @mode =] * \@ modo*  
 Es uno de los valores siguientes.  
  
-   **Deshabilitado** Se produce un error en todas las consultas en tablas habilitadas para Stretch.  
  
-   **LOCAL_ONLY** Las consultas realizadas en tablas habilitadas para Stretch solo devuelven datos locales.  
  
-   **LOCAL_AND_REMOTE** Las consultas en tablas habilitadas para Stretch devuelven datos locales y remotos. Este es el comportamiento predeterminado.  
  
 [ @force =] * \@ forzar*  
 Es un valor de bit opcional que se puede establecer en 1 si se desea cambiar el modo de consulta sin validación.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o >0 (error)  
  
## <a name="permissions"></a>Permisos  
 Requiere permisos de db_owner.  
  
## <a name="remarks"></a>Comentarios  
 Los siguientes procedimientos almacenados extendidos también establecen el modo de consulta para una base de datos habilitada para Stretch.  
  
-   **sp_rda_deauthorize_db**  
  
     Después de ejecutar **sp_rda_deauthorize_db** , se producirá un error en todas las consultas de bases de datos y tablas habilitadas para Stretch. Es decir, el modo de consulta se establece en Disabled. Para salir de este modo, realice una de las siguientes acciones.  
  
    -   Ejecute [Sys. sp_rda_reauthorize_db &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectar con la base de datos remota de Azure. Esta operación restablece automáticamente el modo de consulta en LOCAL_AND_REMOTE, que es el comportamiento predeterminado de Stretch Database. Es decir, las consultas devuelven los resultados de los datos locales y remotos.  
  
    -   Ejecute [Sys. sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) con el argumento LOCAL_ONLY para permitir que las consultas sigan ejecutándose solo con datos locales.  
  
-   **sp_rda_reauthorize_db**  
  
     Al ejecutar [Sys. sp_rda_reauthorize_db &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) para volver a conectar con la base de datos remota de Azure, esta operación restablece automáticamente el modo de consulta en LOCAL_AND_REMOTE, que es el comportamiento predeterminado de stretch Database. Es decir, las consultas devuelven los resultados de los datos locales y remotos.  
  
## <a name="see-also"></a>Consulte también  
 [Sys. sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
