---
title: sp_helptrigger (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1e6244443fc1f6ba7d83376226fedd56563e0d39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048221"
---
# <a name="sphelptrigger-transact-sql"></a>sp_helptrigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el tipo o los tipos de desencadenadores DML definidos en la tabla especificada de la base de datos actual. sp_helptrigger no se puede usar con desencadenadores DDL. Consulta el [procedimientos almacenados del sistema](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) vista de catálogo en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tabname = ] 'table'` Es el nombre de la tabla en la base de datos actual que se va a devolver información de desencadenadores. *tabla* es **nvarchar(776)** , no tiene ningún valor predeterminado.  
  
`[ @triggertype = ] 'type'` Es el tipo de desencadenador DML para devolver información acerca de. *tipo* es **char(6)** , su valor predeterminado es null, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**DELETE**|Devuelve información de desencadenadores DELETE.|  
|**INSERT**|Devuelve información de desencadenadores INSERT.|  
|**UPDATE**|Devuelve información de desencadenadores UPDATE.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 La siguiente tabla muestra la información del conjunto de resultados.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|Nombre del desencadenador.|  
|**trigger_owner**|**sysname**|Nombre del propietario de la tabla donde se definió el desencadenador.|  
|**isupdate**|**int**|1=Desencadenador UPDATE<br /><br /> 0=No es un desencadenador UPDATE|  
|**isdelete**|**int**|1=Desencadenador DELETE<br /><br /> 0=No es un desencadenador DELETE|  
|**isinsert**|**int**|1=Desencadenador INSERT<br /><br /> 0=No es un desencadenador INSERT|  
|**isafter**|**int**|1=Desencadenador AFTER<br /><br /> 0=No es un desencadenador AFTER|  
|**isinsteadof**|**int**|1=Desencadenador INSTEAD OF<br /><br /> 0=No es un desencadenador INSTEAD OF|  
|**trigger_schema**|**sysname**|Nombre del esquema al que pertenece el desencadenador.|  
  
## <a name="permissions"></a>Permisos  
 Requiere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md) permiso en la tabla.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se ejecuta `sp_helptrigger` para producir información sobre el o los desencadenadores de la tabla `Person.Person`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
