---
title: DROP TYPE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP TYPE
- DROP_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [SQL Server], deleting
- UDTs [SQL Server], deleting
- alias data types [SQL Server], removing
- DROP TYPE statement
ms.assetid: 11bf83f9-0718-4238-a835-83d2eb14ae7b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f19e21b60429d04e4af8c615db79302519e5a507
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="drop-type-transact-sql"></a>DROP TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quita de la base datos actual un tipo de datos de alias o un tipo definido por el usuario de Common Language Runtime (CLR).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Quita el tipo condicionalmente solo si ya existe.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece el tipo de alias o el tipo definido por el usuario.  
  
 *type_name*  
 Es el nombre del tipo de datos de alias o del tipo definido por el usuario que desea quitar.  
  
## <a name="remarks"></a>Notas  
 La instrucción DROP TYPE no se ejecuta si se cumple alguna de las siguientes condiciones:  
  
-   Hay tablas en la base de datos que contienen columnas del tipo de datos de alias o del tipo definido por el usuario. Encontrará más información sobre las columnas de tipo de alias o de tipo definido por el usuario si consulta las vistas de catálogo [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) o [sys.column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md).  
  
-   Hay columnas calculadas, restricciones CHECK, vistas enlazadas a esquema y funciones enlazadas a esquema cuyas definiciones hacen referencia al tipo de alias o a un tipo definido por el usuario. Encontrará más información sobre estas referencias si consulta la vista de catálogo [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md).  
  
-   Hay funciones, procedimientos almacenados o desencadenadores creados en la base de datos, y estas rutinas utilizan variables y parámetros de tipo de alias o de tipo definido por el usuario. Encontrará más información sobre los parámetros de tipo de alias o de tipo definido por el usuario si consulta las vistas de catálogo [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) o [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Se necesita el permiso CONTROL en *type_name* o el permiso ALTER en *schema_name*.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se supone que ya se ha creado un tipo denominado `ssn` en la base de datos actual.  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a>Ver también  
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
