---
title: sp_db_vardecimal_storage_format (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_db_vardecimal_storage_format
- sp_db_vardecimal_storage_format_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_db_vardecimal_storage_format
- decimal data type, compressing
- compressing decimal data
- numeric data type, compressing
- database compression [SQL Server]
- table compression [SQL Server]
ms.assetid: 9920b2f7-b802-4003-913c-978c17ae4542
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4ff2ceb2a1e5a616ed12815b678fca6e978a308
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spdbvardecimalstorageformat-transact-sql"></a>sp_db_vardecimal_storage_format (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el estado del formato de almacenamiento vardecimal actual de una base de datos, o habilita una base de datos para el formato de almacenamiento vardecimal.  A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], las bases de datos de usuario siempre están habilitadas. La habilitación de las bases de datos para el formato de almacenamiento vardecimal solo es necesaria en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
> [!IMPORTANT]  
>  El cambio del estado del formato de almacenamiento vardecimal de una base de datos puede afectar a la copia de seguridad y la restauración, creación de reflejo de la base de datos, sp_attach_db, el trasvase de registros y la replicación.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_db_vardecimal_storage_format [ [ @dbname = ] 'database_name']   
    [ , [ @vardecimal_storage_format = ] { 'ON' | 'OFF' } ]   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname=] '*database_name*'  
 Es el nombre de la base de datos para la que se cambia el formato de almacenamiento. *database_name* es **sysname**, no tiene ningún valor predeterminado. Si el nombre de la base de datos se omite, se devuelven los estados del formato de almacenamiento vardecimal de todas las base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [ @vardecimal_storage_format=] {'ON' |' DESACTIVAR '}  
 Especifica si el formato de almacenamiento vardecimal está habilitado. @vardecimal_storage_format puede ser ON u OFF. El parámetro es **varchar(3)**, no tiene ningún valor predeterminado. Si se proporciona un nombre de base de datos pero se omite @vardecimal_storage_format, se devuelve la configuración actual de la base de datos especificada. Este argumento no tiene ningún efecto en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versiones posteriores.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si el formato de almacenamiento de la base de datos no se puede cambiar, sp_db_vardecimal_storage_format devuelve un error. Si la base de datos ya se encuentra en el estado especificado, el procedimiento almacenado no tiene efecto.  
  
 Si el @vardecimal_storage_format no se proporciona el argumento, devuelve las columnas Nombre de base de datos y el estado Vardecimal.  
  
## <a name="remarks"></a>Comentarios  
 sp_db_vardecimal_storage_format devuelve el estado vardecimal pero no lo puede cambiar.  
  
 sp_db_vardecimal_storage_format será incorrecto en las siguientes circunstancias:  
  
-   Existen usuarios activos en la base de datos.  
  
-   La base de datos está habilitada para la creación del reflejo.  
  
-   La edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite el formato de almacenamiento vardecimal.  
  
 Para cambiar el estado del formato de almacenamiento vardecimal a OFF, se debe configurar una base de datos en el modo de recuperación simple. Cuando una base de datos se configura en el modo de recuperación simple, la cadena de registros se rompe. Haga una copia de seguridad de toda la base de datos después de configurar el estado del formato de almacenamiento vardecimal en OFF.  
  
 El cambio al estado OFF será incorrecto si existen tablas que usan la compresión de base de datos vardecimal. Para cambiar el formato de almacenamiento de una tabla, use [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para determinar las tablas de una base de datos que usan el formato de almacenamiento vardecimal, use la función `OBJECTPROPERTY` y busque la propiedad `TableHasVarDecimalStorageFormat`, tal y como se indica en el siguiente ejemplo.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT name, object_id, type_desc  
FROM sys.objects   
 WHERE OBJECTPROPERTY(object_id,   
   N'TableHasVarDecimalStorageFormat') = 1 ;  
GO  
```  
  
## <a name="examples"></a>Ejemplos  
 El siguiente código habilita la compresión en la base de datos `AdventureWorks2012`, confirma el estado y, a continuación, comprime las columnas decimales y numéricas de la tabla `Sales.SalesOrderDetail`.  
  
```  
USE master ;  
GO  
  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON' ;  
GO  
  
-- Check the vardecimal storage format state for  
-- all databases in the instance.  
EXEC sp_db_vardecimal_storage_format ;  
GO  
  
USE AdventureWorks2012 ;  
GO  
  
EXEC sp_tableoption 'Sales.SalesOrderDetail', 'vardecimal storage format', 1 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
