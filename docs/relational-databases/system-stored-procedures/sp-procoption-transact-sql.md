---
title: sp_procoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 218371ab6d8133dbaf1865eeffc11f92883b4305
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533677"
---
# <a name="spprocoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Establece o borra la configuración de ejecución automática de un procedimiento almacenado. Un procedimiento almacenado que se establece en ejecuciones de la ejecución automática cada vez una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ProcName = ] 'procedure'` Es el nombre del procedimiento que se va a establecer una opción. *procedimiento* es **nvarchar(776)**, no tiene ningún valor predeterminado.  
  
`[ @OptionName = ] 'option'` Es el nombre de la opción para establecer. El único valor para *opción* es **inicio**.  
  
`[ @OptionValue = ] 'value'` Indica si se establece la opción en (**true** o **en**) u off (**false** o **desactivar**). *valor* es **varchar (12)**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o número de error (error)  
  
## <a name="remarks"></a>Comentarios  
 Procedimientos de inicio deben estar en el **maestro** de base de datos y no puede contener parámetros de entrada o salida. La ejecución de los procedimientos almacenados comienza cuando se recuperan todas las bases de datos y se registra el mensaje "Se completó la recuperación" en el inicio.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se establece un procedimiento para la ejecución automática.  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'   
    , @OptionName = 'startup'   
    , @OptionValue = 'on';   
```  
  
 En el ejemplo siguiente se detiene la ejecución automática de un procedimiento.  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'      
    , @OptionName = 'startup'
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar un procedimiento almacenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
