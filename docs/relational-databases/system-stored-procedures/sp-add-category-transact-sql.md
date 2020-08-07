---
title: sp_add_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 323a86b4efbaa63d8858341c68908e30258d4889
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865293"
---
# <a name="sp_add_category-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Agrega al servidor la categoría de trabajo, alerta u operador especificada. Para obtener un método alternativo, vea [crear una categoría de trabajo mediante SQL Server Management Studio](/sql/ssms/agent/create-a-job-category).
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 > [!IMPORTANT]  
 > En [Azure SQL instancia administrada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría, pero no todas las características Agente SQL Server se admiten actualmente. Para más información, consulte [diferencias de sql instancia administrada T-SQL de Azure en SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) .
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @class = ] 'class'`Clase de la categoría que se va a agregar. la *clase* es **VARCHAR (8)** con un valor predeterminado Job y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|JOB|Agrega una categoría de trabajo.|  
|ALERT|Agrega una categoría de alerta.|  
|OPERATOR|Agrega una categoría de operador.|  
  
`[ @type = ] 'type'`Tipo de categoría que se va a agregar. *Type* es **VARCHAR (12)**, con un valor predeterminado de **local**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|LOCAL|Categoría de trabajos locales.|  
|VARIOS SERVIDORES|Categoría de trabajos multiservidor.|  
|Ninguno|Una categoría para una clase distinta de JOB **.**|  
  
`[ @name = ] 'name'`Nombre de la categoría que se va a agregar. El nombre debe ser único en la clase especificada. *Name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Observaciones  
 **sp_add_category** se debe ejecutar desde la base de datos **msdb** .  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_add_category**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una categoría de trabajos locales denominada `AdminJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_delete_category &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Trabajos dedbo.sys&#40;&#41;de Transact-SQL](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
