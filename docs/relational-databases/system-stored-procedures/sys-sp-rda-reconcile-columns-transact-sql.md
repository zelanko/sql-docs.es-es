---
title: sys.sp_rda_reconcile_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 83ac2322d39fba05ce75f50fcd9cf9e5005b72b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982985"
---
# <a name="syssprdareconcilecolumns-transact-sql"></a>sys.sp_rda_reconcile_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Reconcilia las columnas de la tabla remota de Azure a las columnas de la tabla de SQL Server habilitada para Stretch.  
    
  **sp_rda_reconcile_columns** agrega columnas a la tabla remota que hay en la tabla de SQL Server habilitada para Stretch, pero no en la tabla remota. Estas columnas pueden ser columnas que se ha eliminado accidentalmente de la tabla remota. Sin embargo, **sp_rda_reconcile_columns** no elimina las columnas de la tabla remota que hay en la tabla remota, pero no en la tabla de SQL Server.
  
  > [!IMPORTANT]
  > Cuando **sp_rda_reconcile_columns** vuelve a crear las columnas que eliminó por error de la tabla remota, no restaura los datos que había antes en las columnas eliminadas.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 \@objname = ' *\@objname*'  
 El nombre de la tabla de SQL Server habilitada para Stretch.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o > 0 (error)  
  
## <a name="permissions"></a>Permisos  
 Se requieren permisos db_owner.  
   
## <a name="remarks"></a>Comentarios  
 Si hay columnas en la tabla remota de Azure que ya no existen en la tabla de SQL Server habilitada para Stretch, estas columnas adicionales no impiden que Stretch Database funcione con normalidad. También puede quitar estas columnas adicionales de forma manual.  
  
## <a name="example"></a>Ejemplo  
 Para conciliar las columnas de la tabla de Azure remota, ejecute la siguiente instrucción.  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
