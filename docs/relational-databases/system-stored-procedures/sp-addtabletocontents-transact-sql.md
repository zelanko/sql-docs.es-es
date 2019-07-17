---
title: sp_addtabletocontents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
author: stevestein
ms.author: sstein
ms.openlocfilehash: e9d5e0e22f5dcca3611923782786a83ada1672ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117934"
---
# <a name="spaddtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inserta en las tablas de seguimiento de mezcla las referencias para las filas de una tabla de origen que no están incluidas actualmente en las tablas de seguimiento. Use esta opción si ha bulk-cargado una gran cantidad de datos mediante **bcp**, que no activarán los desencadenadores de seguimiento de mezcla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_name = ] 'table_name'` Es el nombre de la tabla. *table_name* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @owner_name = ] 'owner_name'` Es el nombre del propietario de la tabla. *owner_name* es **sysname**, su valor predeterminado es null.  
  
`[ @filter_clause = ] 'filter_clause'` Especifica una cláusula de filtro que controla qué filas de datos recientemente cargados deben agregarse a las tablas de seguimiento de mezcla. *filter_clause* es **nvarchar (4000)** , su valor predeterminado es null. Si *filter_clause* es **null**, masiva todas las filas cargadas se agregan.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addtabletocontents** solo se usa en la replicación de mezcla.  
  
 Las filas de la *table_name* se denominan mediante sus **rowguidcol** y las referencias se agregan a las tablas de seguimiento de mezcla. **sp_addtabletocontents** debe utilizarse después de la copia masiva de datos en una tabla que se publica mediante replicación de mezcla. El procedimiento almacenado inicia el seguimiento de las filas copiadas y garantiza que las nuevas filas se incluirán en la siguiente sincronización.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_addtabletocontents**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
