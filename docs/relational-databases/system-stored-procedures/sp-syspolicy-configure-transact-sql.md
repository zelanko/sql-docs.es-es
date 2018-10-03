---
title: sp_syspolicy_configure (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_configure
- sp_syspolicy_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_configure
ms.assetid: 70c10922-9345-4190-ba69-808a43f760da
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 4b27da09e0e57029b65c21110a93de46ed0d81a6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783973"
---
# <a name="spsyspolicyconfigure-transact-sql"></a>sp_syspolicy_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura los valores de la administración basada en directivas, por ejemplo si está habilitada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syspolicy_configure [ @name = ] 'name'  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name =** ] **'***nombre***'**  
 Es el nombre del valor que desea configurar. *nombre* es **sysname**, es obligatorio y no puede ser NULL ni una cadena vacía.  
  
 *nombre* puede ser cualquiera de los siguientes valores:  
  
-   'Enabled': determina si la administración basada en directivas está habilitada.  
  
-   'HistoryRetentionInDays': especifica el número de días que se debería conservar el historial de evaluaciones de directivas. Si se establece en 0, el historial no se quitará automáticamente.  
  
-   'LogOnSuccess': especifica si la administración basada en directivas registra las evaluaciones de la directiva correctas.  
  
 [  **@value =** ] *valor*  
 Es el valor que está asociado con el valor especificado para *nombre*. *valor* es **sql_variant**y es necesario.  
  
-   Si especifica 'Enabled' para *nombre*, puede usar cualquiera de los siguientes valores:  
  
    -   0 = Deshabilita la administración basada en directivas.  
  
    -   1 = Habilita la administración basada en directivas.  
  
-   Si especifica 'HistoryRententionInDays' para *nombre*, especifique el número de días como un valor entero.  
  
-   Si especifica 'LogOnSuccess' para *nombre*, puede usar cualquiera de los siguientes valores:  
  
    -   0 = Registra solo las evaluaciones de directiva con errores.  
  
    -   1 = Registra tanto las evaluaciones de directiva correctas como las que tienen errores.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Debe ejecutar sp_syspolicy_configure en el contexto de la base de datos del sistema msdb.  
  
 Para ver los valores actuales de esta configuración, consulte la vista del sistema msdb.dbo.syspolicy_configuration.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de base de datos PolicyAdministratorRole.  
  
> [!IMPORTANT]  
>  Posible elevación de credenciales: los usuarios del rol PolicyAdministratorRole pueden crear desencadenadores del servidor y programar ejecuciones de directivas que pueden afectar al funcionamiento de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por ejemplo, los usuarios del rol PolicyAdministratorRole pueden crear una directiva que puede evitar que la mayoría de los objetos se creen en [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Debido a esta posible elevación de credenciales, el rol PolicyAdministratorRole se debería conceder únicamente a los usuarios que sean de confianza para controlar la configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se habilita la administración basada en directivas.  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'Enabled'  
, @value = 1;  
  
GO  
```  
  
 En el ejemplo siguiente se establece la retención del historial de directivas en 14 días.  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'HistoryRetentionInDays'  
, @value = 14;  
  
GO  
```  
  
 En el ejemplo siguiente se configura la administración basada en directivas para registrar tanto las evaluaciones de directiva correctas como las que tienen errores.  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'LogOnSuccess'  
, @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_enabled &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-enabled-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_set_log_on_success &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-log-on-success-transact-sql.md)  
  
  
