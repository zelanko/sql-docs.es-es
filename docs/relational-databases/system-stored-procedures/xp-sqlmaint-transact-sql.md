---
title: xp_sqlmaint (Transact-SQL) | Microsoft Docs
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
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e93410713f9af8228fd757803792665c569b549a
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101913"
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Las llamadas del **sqlmaint** utilidad con una cadena que contiene **sqlmaint**conmutadores. El **sqlmaint** utilidad realiza un conjunto de operaciones de mantenimiento en una o varias bases de datos.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *switch_string* **'**  
 Es una cadena que contiene el **sqlmaint** modificadores de la utilidad. Los modificadores y sus valores tienen que estar separados por un espacio.  
  
 ¿El **-?** no es válido para el conmutador **xp_sqlmaint**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Ninguno. Devuelve un error si el **sqlmaint** utilidad se produce un error.  
  
## <a name="remarks"></a>Notas  
 Si se llama a este procedimiento por el usuario ha iniciado sesión con autenticación de SQL Server, el **- U "***login_id***"** y **-P "***contraseña***"** modificadores se anteponen a *switch_string* antes de la ejecución. Si el usuario ha iniciado sesión con autenticación de Windows, *switch_string* se pasa sin cambios a **sqlmaint**.  
  
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
  
## <a name="see-also"></a>Vea también  
 [sqlmaint, utilidad](../../tools/sqlmaint-utility.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
