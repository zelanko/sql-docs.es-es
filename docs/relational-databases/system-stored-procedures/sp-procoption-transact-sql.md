---
title: sp_procoption (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49f2d1c4bf0e446b7c1577afbae138027a1a5745
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spprocoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Establece o borra la configuración de ejecución automática de un procedimiento almacenado. Un procedimiento almacenado que se establece en ejecuciones de la ejecución automática cada vez que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@ProcName =** ] **'***procedimiento***'**  
 Es el nombre del procedimiento para que se va a establecer una opción. *procedimiento* es **nvarchar(776)**, no tiene ningún valor predeterminado.  
  
 [  **@OptionName =** ] **'***opción***'**  
 Es el nombre de la opción que se va a establecer. El único valor para *opción* es **inicio**.  
  
 [  **@OptionValue =** ] **'***valor***'**  
 Indica si se establece la opción en (**true** o **en**) o desactivada (**false** o **desactivar**). *valor* es **varchar (12)**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o número de error (error)  
  
## <a name="remarks"></a>Comentarios  
 Procedimientos de inicio deben estar en el **principal** la base de datos y no puede contener parámetros de entrada o salida. La ejecución de los procedimientos almacenados comienza cuando se recuperan todas las bases de datos y se registra el mensaje "Se completó la recuperación" en el inicio.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se establece un procedimiento para la ejecución automática.  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';   
```  
  
 En el ejemplo siguiente se detiene la ejecución automática de un procedimiento.  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar un procedimiento almacenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
