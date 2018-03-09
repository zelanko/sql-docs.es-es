---
title: sp_validname (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_validname
- sp_validname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validname
ms.assetid: d51c53c2-1332-407f-b725-4983f2e710eb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00dc003905fb90ae819bc49eba68aeee2f1cdbb1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spvalidname-transact-sql"></a>sp_validname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Comprueba la validez de los nombres de identificadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Todos los datos no binarios y es distinto de cero, incluidos los datos Unicode que pueden almacenarse mediante el uso de la **nchar**, **nvarchar**, o **ntext** tipos de datos, se aceptan como caracteres válidos para nombres de identificador.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_validname [@name =] 'name'   
     [, [@raise_error =] raise_error]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name=** ] **'***nombre***'**  
 Es el nombre de la [identificadores](../../relational-databases/databases/database-identifiers.md) para que se va a comprobar la validez. *nombre* es **sysname**, no tiene ningún valor predeterminado. *nombre de* no puede ser NULL, no puede ser una cadena vacía y no puede contener un carácter cero binario.  
  
 [  **@raise_error=** ] *raise_error*  
 Especifica si se produce un error. *raise_error* es **bits**, su valor predeterminado es 1. Esto significa que aparecerán errores. 0 hace que no aparezca ningún mensaje de error.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Vea también  
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR &#40; Transact-SQL &#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [nchar y nvarchar &#40; Transact-SQL &#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [ntext, text e imagen &#40; Transact-SQL &#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
