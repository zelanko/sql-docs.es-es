---
title: xp_sqlmaint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac6461e522973b43926b66b6e525526ae6952d85
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755513"
---
# <a name="xp_sqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Llama a la utilidad **SQLMAINT** con una cadena que contiene los modificadores **SQLMAINT**. La utilidad **SQLMAINT** realiza un conjunto de operaciones de mantenimiento en una o varias bases de datos.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *switch_string* **'**  
 Es una cadena que contiene los modificadores de la utilidad **SQLMAINT** . Los modificadores y sus valores tienen que estar separados por un espacio.  
  
 El **-?** el modificador no es válido para **xp_sqlmaint**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Ninguno. Devuelve un error si se produce un error en la utilidad **SQLMAINT** .  
  
## <a name="remarks"></a>Comentarios  
 Si un usuario que ha iniciado sesión con SQL Server autenticación llama a este procedimiento, los modificadores **-U "***login_id***"** y **-P "***contraseña***"** se anteponen a *switch_string* antes de la ejecución. Si el usuario ha iniciado sesión con la autenticación de Windows, *switch_string* se pasa sin cambiar a **SQLMAINT**.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, `xp_sqlmaint` llama a `sqlmaint` para realizar comprobaciones de integridad, crear un archivo de informe y actualizar `msdb.dbo.sysdbmaintplan_history`.  
  
```  
EXEC xp_sqlmaint '-D AdventureWorks2012 -PlanID 02A52657-D546-11D1-9D8A-00A0C9054212   
   -Rpt "C:\Program Files\Microsoft SQL Server\MSSQL\LOG\DBMaintPlan2.txt" -WriteHistory  -CkDB -CkAl';   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The command(s) executed successfully.  
```  
  
## <a name="see-also"></a>Consulte también  
 [SQLMAINT (utilidad)](../../tools/sqlmaint-utility.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
