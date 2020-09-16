---
description: DROP AGGREGATE (Transact-SQL)
title: DROP AGGREGATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 46c1074500d6ea73af9b10ff373a8beb9cb433d5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541305"
---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Quita una función de agregado definida por el usuario de la base de datos actual. Las funciones de agregado definidas por el usuario se crean con [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *IF EXISTS*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Quita condicionalmente el agregado solo si ya existe.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la función de agregado definida por el usuario.  
  
 *aggregate_name*  
 Es el nombre de la función de agregado definida por el usuario que se desea quitar.  
  
## <a name="remarks"></a>Comentarios  
 DROP AGGREGATE no se ejecuta si hay vistas, funciones o procedimientos almacenados creados con enlaces de esquema que hacen referencia a la función de agregado definida por el usuario que se desea quitar.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar DROP AGGREGATE, el usuario debe tener, como mínimo, el permiso ALTER para el esquema al que pertenece el agregado definido por el usuario o el permiso CONTROL para el agregado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el agregado `Concatenate`.  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [Crear funciones de agregado definidas por el usuario](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  
