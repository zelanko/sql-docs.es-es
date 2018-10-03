---
title: sp_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs:
- TSQL
helpviewer_keywords:
- sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1be4fbfb6ce30443a979fb500954e7aa8fa9779a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614937"
---
# <a name="spdatabases-transact-sql"></a>sp_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enumera las bases de datos que residen en una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o que están accesibles a través de una puerta de enlace de la base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**DATABASE_NAME**|**sysname**|Nombre de la base de datos. En el [!INCLUDE[ssDE](../../includes/ssde-md.md)], esta columna representa el nombre de la base de datos tal como está almacenado en el **sys.databases** vista de catálogo.|  
|**DATABASE_SIZE**|**int**|Tamaño de la base de datos, en kilobytes.|  
|**COMENTARIOS**|**varchar(254)**|Para el [!INCLUDE[ssDE](../../includes/ssde-md.md)], este campo siempre devuelve NULL.|  
  
## <a name="remarks"></a>Comentarios  
 Los nombres de bases de datos devueltos pueden utilizarse como parámetros en la instrucción USE para cambiar el contexto de la base de datos actual.  
  
 **sp_databases** no tiene ningún equivalente en Open Database Connectivity (ODBC).  
  
## <a name="permissions"></a>Permisos  
 Requiere permiso CREATE DATABASE, ALTER ANY DATABASE o VIEW ANY DEFINITION y debe tener permiso de acceso a la base de datos. No se le puede denegar el permiso VIEW ANY DEFINITION.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra la ejecución de `sp_databases`.  
  
```sql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;Transact-SQL&#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
