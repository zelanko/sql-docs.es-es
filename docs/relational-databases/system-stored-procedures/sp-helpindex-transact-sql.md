---
title: sp_helpindex (Transact-SQL) | Microsoft Docs
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
- sp_helpindex_TSQL
- sp_helpindex
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpindex
ms.assetid: c7f73ba0-ec35-4b10-aa5f-f1487e51fbf7
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 6560726bb583d823ad0cf0b36310eb68691705f2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39547625"
---
# <a name="sphelpindex-transact-sql"></a>sp_helpindex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de los índices de una tabla o vista.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpindex [ @objname = ] 'name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname=** ] **'***nombre***'**  
 Es el nombre calificado o no calificado de una tabla o vista definida por un usuario. Solo son necesarias las comillas si se especifica una tabla o nombre de vista calificada. Si se proporciona un nombre completo, incluido el nombre de la base de datos, el nombre de la base de datos debe ser el de la base de datos actual. *nombre* es **nvarchar(776)**, no tiene valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**index_name**|**sysname**|Nombre del índice.|  
|**index_description**|**varchar(210)**|Descripción del índice incluido el grupo de archivos en el que está ubicado.|  
|**index_keys**|**nvarchar (2078)**|Columnas de tabla o vista sobre las que se genera el índice.|  
  
 Aparecerá listada una columna de índice descendente en el conjunto de resultados con un signo menos (-) tras el nombre; la columna predeterminada de índice ascendente aparecerá listada solamente por su nombre.  
  
## <a name="remarks"></a>Notas  
 Si se han establecido los índices mediante la opción NORECOMPUTE de UPDATE STATISTICS, esa información se incluye en el **index_description** columna.  
  
 **sp_helpindex** expone solo las columnas de índice ordenable; por lo tanto, no expone información sobre los índices XML o índices espaciales.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo presenta los tipos de índices de la tabla `Customer`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpindex N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
