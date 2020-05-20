---
title: sp_clean_db_file_free_space (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_clean_db_file_free_space
- sp_clean_db_file_free_space_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ghost records
- sp_clean_db_file_free_space
ms.assetid: 3eb53a67-969d-4cb8-9681-b1c8e6fd55b6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1761c3546d043dd74a3fe2b491618140635fe61c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823463"
---
# <a name="sp_clean_db_file_free_space-transact-sql"></a>sp_clean_db_file_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita la información residual que queda en las páginas de base de datos a causa de las rutinas de modificación de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sp_clean_db_file_free_space limpia todas las páginas de un solo archivo de una base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_clean_db_file_free_space   
[ @dbname ] = 'database_name'   
, @fileid = 'file_number'   
 [ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname =] '*database_name*'  
 Es el nombre de la base de datos que se va a limpiar. *dbname* es de **tipo sysname** y no puede ser null.  
  
 [ @fileid =] '*file_number*'  
 Es el id. del archivo de datos que se va a limpiar. *file_number* es de **tipo int** y no puede ser null.  
  
 [ @cleaning_delay =] '*delay_in_seconds*'  
 Especifica un intervalo de retardo entre la limpieza de páginas. Esto ayuda a reducir el efecto en el sistema de E/S. *delay_in_seconds* es de **tipo int** y su valor predeterminado es 0.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 Elimina las operaciones de una tabla o las operaciones de actualización que hacen que una fila que se va a mover pueda liberar inmediatamente espacio en una página quitando las referencias a la fila. Sin embargo, en determinadas circunstancias, la fila puede permanecer físicamente en la página de datos como un registro fantasma. Los registros fantasma se quitan periódicamente mediante un proceso en segundo plano. No devuelve estos datos residuales [!INCLUDE[ssDE](../../includes/ssde-md.md)] en respuesta a las consultas. Sin embargo, en entornos en los que la seguridad física de los datos o de los archivos de copia de seguridad corre un riesgo, puede utilizar sp_clean_db_file_free_space para limpiar estos registros fantasma.  
  
 El período de tiempo necesario para ejecutar sp_clean_db_file_free_space depende del tamaño del archivo, del espacio disponible y de la capacidad del disco. Dado que la ejecución de sp_clean_db_file_free_space puede afectar significativamente a la actividad de E/S, se recomienda ejecutar este procedimiento fuera del horario de funcionamiento habitual.  
  
 Antes de ejecutar sp_clean_db_file_free_space es aconsejable crear una copia de seguridad completa de la base de datos.  
  
 El procedimiento almacenado de [sp_clean_db_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-free-space-transact-sql.md) relacionado limpia todos los archivos de la base de datos.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol de la base de datos db_owner.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se limpia toda la información residual del archivo de datos principal de la base de datos `AdventureWorks2012`.  
  
```  
USE master;  
GO  
EXEC sp_clean_db_file_free_space   
@dbname = N'AdventureWorks2012', @fileid = 1 ;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Motor de base de datos procedimientos almacenados &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)
 <br>[Guía del proceso de limpieza de Ghost](../ghost-record-cleanup-process-guide.md) 
  
  
