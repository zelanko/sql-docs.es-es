---
title: sp_helptext (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helptext
- sp_helptext_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptext
ms.assetid: 24135456-05f0-427c-884b-93cf38dd47a8
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3cc2628e0c689f41ff954ae9e0d916f79e65c06b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sphelptext-transact-sql"></a>sp_helptext (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra definiciones de reglas definidas por el usuario, valores predeterminados, procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] no cifrados, funciones [!INCLUDE[tsql](../../includes/tsql-md.md)] definidas por el usuario, desencadenadores, columnas calculadas, restricciones CHECK, vistas u objetos del sistema, como un procedimiento almacenado del sistema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helptext [ @objname = ] 'name' [ , [ @columnname = ] computed_column_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname =** ] **'***nombre***'**  
 Es el nombre, completo o no, de un objeto definido por el usuario en el ámbito de esquema. Se requieren comillas solo si se especifica un nombre de objeto calificado. Si se proporciona un nombre completo, incluido el nombre de la base de datos, el nombre de la base de datos debe ser el de la base de datos actual. El objeto debe estar en la base de datos actual. *nombre* es **nvarchar(776)**, no tiene ningún valor predeterminado.  
  
 [  **@columnname =** ] **'***computed_column_name***'**  
 Es el nombre de la columna calculada para la que se va a mostrar la definición. La tabla que contiene la columna debe especificarse como *nombre*. *column_name* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Texto**|**nvarchar(255)**|Definición del objeto|  
  
## <a name="remarks"></a>Comentarios  
 sp_helptext muestra la definición que se utiliza para crear un objeto en varias filas. Cada fila contiene 255 caracteres de la definición de [!INCLUDE[tsql](../../includes/tsql-md.md)]. La definición reside en el **definición** columna en el [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) vista de catálogo.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** . Las definiciones de los objetos del sistema están visibles públicamente. La definición de los objetos de usuario está visible para el propietario del objeto o los receptores de los permisos siguientes: ALTER, CONTROL, TAKE OWNERSHIP o VIEW DEFINITION.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-the-definition-of-a-trigger"></a>A. Mostrar la definición de un desencadenador  
 En el ejemplo siguiente se muestra la definición del desencadenador `dEmployee` en el [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]base de datos.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptext 'HumanResources.dEmployee';  
GO  
```  
  
### <a name="b-displaying-the-definition-of-a-computed-column"></a>B. Mostrar la definición de una columna calculada  
 En el ejemplo siguiente se muestra la definición de la columna calculada `TotalDue` de la tabla `SalesOrderHeader` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
sp_helptext @objname = N'AdventureWorks2012.Sales.SalesOrderHeader', @columnname = TotalDue ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text`  
  
 `---------------------------------------------------------------------`  
  
 `(isnull(([SubTotal]+[TaxAmt])+[Freight],(0)))`  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
