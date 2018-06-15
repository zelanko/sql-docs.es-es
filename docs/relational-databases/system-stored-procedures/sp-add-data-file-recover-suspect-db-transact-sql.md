---
title: sp_add_data_file_recover_suspect_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_data_file_recover_suspect_db
- sp_add_data_file_recover_suspect_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_data_file_recover_suspect_db
ms.assetid: b25262aa-a228-48b7-8739-6581c760b171
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 13c08441680744d38f870fc5b6ebd5d7a1e20c91
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239165"
---
# <a name="spadddatafilerecoversuspectdb-transact-sql"></a>sp_add_data_file_recover_suspect_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un archivo de datos a un grupo de archivos cuando no se puede completar la recuperación en una base de datos debido a espacio insuficiente en el grupo de archivos (error 1105). Tras agregar el archivo, este procedimiento almacenado desactiva el valor sospechoso y completa la recuperación de la base de datos. Los parámetros son los mismos que los de ALTER DATABASE *database_name* ADD FILE.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_data_file_recover_suspect_db [ @dbName= ] 'database'   
    , [ @filegroup = ] 'filegroup_name'   
    , [ @name = ] 'logical_file_name'   
    , [ @filename= ] 'os_file_name'   
    , [ @size = ] 'size'   
    , [ @maxsize = ] 'max_size'   
    , [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@dbName=** ] **'***database* **'**  
 Es el nombre de la base de datos. *base de datos* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@filegroup=** ] **' *** filegroup_name* **'**  
 Es el grupo de archivos al que se agrega el archivo. *filegroup_name* es **nvarchar (260)**, su valor predeterminado es null, lo que indica el archivo principal.  
  
 [  **@name=** ] **' *** nombre_de_archivo_lógico* **'**  
 Es el nombre utilizado en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hacer referencia al archivo. El nombre debe ser único en el servidor. *nombre_de_archivo_lógico* es **nvarchar (260)**, no tiene ningún valor predeterminado.  
  
 [  **@filename=** ] **' *** nombre_de_archivo_de_sistema_operativo* **'**  
 Es la ruta de acceso y el nombre de archivo que el sistema operativo utiliza para el archivo. El archivo debe residir en una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. *nombre_de_archivo_de_sistema_operativo* es **nvarchar (260)**, no tiene ningún valor predeterminado.  
  
 [ **@size=** ] **'***size* **'**  
 Es el tamaño inicial del archivo. *tamaño* es **nvarchar (20)**, su valor predeterminado es null. Especifique un número entero; no incluya decimales. Se pueden utilizar los sufijos MB y KB para especificar megabytes o kilobytes, respectivamente. El valor predeterminado es MB. El valor mínimo es 512 KB. Si *tamaño* no se especifica, el valor predeterminado es 1 MB.  
  
 [ **@maxsize=** ] **'***max_size* **'**  
 Es el tamaño máximo que puede alcanzar el archivo. *max_size* es **nvarchar (20)**, su valor predeterminado es null. Especifique un número entero; no incluya decimales. Se pueden utilizar los sufijos MB y KB para especificar megabytes o kilobytes, respectivamente. El valor predeterminado es MB.  
  
 Si *max_size* no se especifica, el archivo crecerá hasta que el disco está lleno. El registro de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows avisa a un administrador cuando un disco está a punto de llenarse.  
  
 [  **@filegrowth=** ] **' *** growth_increment* **'**  
 Es la cantidad de espacio que se agrega al archivo cada vez que se necesita más espacio. *growth_increment* es **nvarchar (20)**, su valor predeterminado es null. Un valor 0 indica que no hay crecimiento. Especifique un número entero; no incluya decimales. El valor se puede especificar en MB, KB o como un porcentaje (%). Cuando se especifica %, el incremento de crecimiento es el porcentaje especificado del tamaño del archivo en el momento en que tiene lugar el incremento. Si se especifica un número sin los sufijos MB, KB o %, el valor predeterminado es MB.  
  
 Si *growth_increment* es NULL, el valor predeterminado es 10% y el valor mínimo es 64 KB. El tamaño especificado se redondea al múltiplo de 64 KB más cercano.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución predeterminados a los miembros de la **sysadmin** rol fijo de servidor. Estos permisos no se pueden transferir.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, la base de datos `db1` se marcó como sospechosa durante la recuperación debido a espacio insuficiente (error 1105) en el grupo de archivos `fg1`.  
  
```  
USE master;  
GO  
EXEC sp_add_data_file_recover_suspect_db db1, fg1, file2,  
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_file2.mdf', '1MB';  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
