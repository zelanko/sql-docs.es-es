---
title: sp_clean_db_file_free_space (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_clean_db_file_free_space
- sp_clean_db_file_free_space_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ghost records
- sp_clean_db_file_free_space
ms.assetid: 3eb53a67-969d-4cb8-9681-b1c8e6fd55b6
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 41c242e65df878a0a97d6fce221d3bcf3dcde9e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spcleandbfilefreespace-transact-sql"></a>sp_clean_db_file_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita la información residual que queda en las páginas de base de datos a causa de las rutinas de modificación de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sp_clean_db_file_free_space limpia todas las páginas solo en un archivo de una base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_clean_db_file_free_space   
[ @dbname ] = 'database_name'   
, @fileid = 'file_number'   
 [ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname=] '*database_name*'  
 Es el nombre de la base de datos que se va a limpiar. *dbname* es **sysname** y no puede ser NULL.  
  
 [ @fileid=] '*file_number*'  
 Es el id. del archivo de datos que se va a limpiar. *file_number* es **int** y no puede ser NULL.  
  
 [ @cleaning_delay=] '*retraso_en_segundos*'  
 Especifica un intervalo de retardo entre la limpieza de páginas. Esto ayuda a reducir el efecto en el sistema de E/S. *retraso_en_segundos* es **int** con un valor predeterminado es 0.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Elimina las operaciones de una tabla o las operaciones de actualización que hacen que una fila que se va a mover pueda liberar inmediatamente espacio en una página quitando las referencias a la fila. Sin embargo, en determinadas circunstancias, la fila puede permanecer físicamente en la página de datos como un registro fantasma. Los registros fantasma se quitan periódicamente mediante un proceso en segundo plano. No devuelve estos datos residuales el [!INCLUDE[ssDE](../../includes/ssde-md.md)] en respuesta a consultas. Sin embargo, en entornos en los que la seguridad física de los datos o de los archivos de copia de seguridad corre un riesgo, puede utilizar sp_clean_db_file_free_space para limpiar estos registros fantasma.  
  
 El período de tiempo necesario para ejecutar sp_clean_db_file_free_space depende del tamaño del archivo, del espacio disponible y de la capacidad del disco. Dado que la ejecución de sp_clean_db_file_free_space puede afectar significativamente a la actividad de E/S, se recomienda ejecutar este procedimiento fuera del horario de funcionamiento habitual.  
  
 Antes de ejecutar sp_clean_db_file_free_space es aconsejable crear una copia de seguridad completa de la base de datos.  
  
 Relacionado [sp_clean_db_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-free-space-transact-sql.md) procedimiento almacenado limpia todos los archivos de la base de datos.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol de la base de datos db_owner.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se limpia toda la información residual del archivo de datos principal de la base de datos `AdventureWorks2012`.  
  
```  
USE master;  
GO  
EXEC sp_clean_db_file_free_space   
@dbname = N'AdventureWorks2012', @fileid = 1 ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
