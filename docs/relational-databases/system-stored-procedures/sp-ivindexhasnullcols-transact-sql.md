---
title: sp_ivindexhasnullcols (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dbdbe2a627eb49dbd2ab71bef5bc102f1b157d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Comprueba que el índice clúster de la vista indizada es exclusivo y no contiene ninguna columna que pueda tener el valor NULL cuando se vaya a utilizar la vista indizada para crear una publicación transaccional. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@viewname** =] **'***view_name***'**  
 Es el nombre de la vista que se va a verificar. *view_name* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@fhasnullcols** =] *field_has_null_columns* salida  
 Indica si el índice de la vista tiene columnas que permiten valores NULL. *view_name* es **sysname**, no tiene ningún valor predeterminado. Devuelve un valor de **1** si el índice de la vista tiene columnas que permiten valores NULL. Devuelve un valor de **0** si la vista no contiene columnas que permiten valores NULL.  
  
> [!NOTE]  
>  Si el propio procedimiento almacenado devuelve un código de retorno de **1**, lo que significa que la ejecución del procedimiento almacenado ha producido un error, este valor es **0** y debe omitirse.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_ivindexhasnullcols** se utiliza en la replicación transaccional.  
  
 De manera predeterminada, los artículos de vista indizada de una publicación se crean como tablas en los suscriptores. Sin embargo, cuando la columna indizada permite valores NULL, la vista indizada se crea como una vista indizada en el suscriptor en lugar de una tabla. Al ejecutar este procedimiento almacenado, se puede alertar al usuario sobre si existe o no este problema con la vista indizada actual.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_ivindexhasnullcols**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
