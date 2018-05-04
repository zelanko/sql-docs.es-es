---
title: Core.sp_remove_collector_type (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_remove_collector_type
- sp_remove_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- core.sp_remove_collector_type stored procedure
- management data warehouse, data collector stored procedures
- sp_remove_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 88ceba25-e41a-405f-a416-bb68918a0024
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b4b7589569f0f0e38463209bc740eb8b6f0d23ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="corespremovecollectortype-transact-sql"></a>core.sp_remove_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una entrada de la vista core.supported_collector_types en el almacén de administración de datos. El procedimiento se debe ejecutar en el contexto de la base de datos de almacén de administración de datos.  
  
 La vista core.supported_collector_types muestra los tipos de recopilador registrados que pueden cargar datos en el almacén de administración de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
core.sp_remove_collector_type [ @collector_type_uid = ] 'collector_type_uid'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collector_type_uid =] '*collector_type_uid*'  
 El GUID para el tipo de recopilador. *collector_type_uid* es **uniqueidentifier**, sin valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **mdw_admin** (con permiso EXECUTE) rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el tipo de recopilador Consulta T-SQL genérico de la vista core.supported_collector_types.  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @RC int;  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = (SELECT collector_type_uid FROM msdb.dbo.syscollector_collector_types WHERE name = N'Generic T-SQL Query Collector Type');  
EXECUTE @RC = core.sp_remove_collector_type @collector_type_uid;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Almacén de administración de datos](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
