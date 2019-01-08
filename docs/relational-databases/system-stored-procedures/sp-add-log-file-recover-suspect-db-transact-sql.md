---
title: sp_add_log_file_recover_suspect_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_file_recover_suspect_db_TSQL
- sp_add_log_file_recover_suspect_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_file_recover_suspect_db
ms.assetid: b41ca3a5-7222-4c22-a012-e66a577a82f6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 525af6370b7e1af1591162109382005adbbf0bac
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505653"
---
# <a name="spaddlogfilerecoversuspectdb-transact-sql"></a>sp_add_log_file_recover_suspect_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un archivo de registro a un grupo de archivos cuando la recuperación no puede completarse en una base de datos debido a un error de espacio de registro insuficiente (9002). Después de agrega el archivo, **sp_add_log_file_recover_suspect_db** desactiva el valor sospechoso y completa la recuperación de la base de datos. Los parámetros son los mismos que los de ALTER DATABASE *database_name* ADD LOG FILE.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_log_file_recover_suspect_db [ @dbName= ] 'database' ,   
    [ @name = ] 'logical_file_name' ,   
    [ @filename= ] 'os_file_name' ,   
    [ @size = ] 'size' ,   
    [ @maxsize = ] 'max_size' ,   
    [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbName =** ] **'**_base de datos_**'**  
 Es el nombre de la base de datos. *base de datos* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@name=** ] **'**_nombre_de_archivo_lógico_**'**  
 Es el nombre usado en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se hace referencia al archivo. El nombre debe ser único en el servidor. *logical_file_name* es **nvarchar (260)**, no tiene ningún valor predeterminado.  
  
 [  **@filename =** ] **'**_os_file_name_**'**  
 Es la ruta de acceso y el nombre de archivo que el sistema operativo utiliza para el archivo. El archivo debe residir en el servidor donde esté instalado el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. *os_file_name* es **nvarchar (260)**, no tiene ningún valor predeterminado.  
  
 [  **@size=** ] **'**_tamaño_ **'**  
 Es el tamaño inicial del archivo. *tamaño* es **nvarchar (20)**, su valor predeterminado es null. Especifique un número entero; no incluya decimales. Se pueden utilizar los sufijos MB y KB para especificar megabytes o kilobytes, respectivamente. El valor predeterminado es MB. El valor mínimo es 512 KB. Si *tamaño* no se especifica, el valor predeterminado es 1 MB.  
  
 [  **@maxsize=** ] **'**_max_size_ **'**  
 Es el tamaño máximo que puede alcanzar el archivo. *max_size* es **nvarchar (20)**, su valor predeterminado es null. Especifique un número entero; no incluya decimales. Se pueden utilizar los sufijos MB y KB para especificar megabytes o kilobytes, respectivamente. El valor predeterminado es MB.  
  
 Si *max_size* no se especifica, el archivo crecerá hasta que el disco está lleno. El registro de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows avisa a un administrador cuando un disco está a punto de llenarse.  
  
 [  **@filegrowth=** ] **'**_growth_increment_ **'**  
 Es la cantidad de espacio que se agrega al archivo cada vez que se necesita más espacio. *growth_increment* es **nvarchar (20)**, su valor predeterminado es null. Un valor 0 indica que no hay crecimiento. Especifique un número entero; no incluya decimales. El valor se puede especificar en MB, KB o como un porcentaje (%). Cuando se especifica %, el incremento de crecimiento es el porcentaje del tamaño del archivo especificado en el momento en que tiene lugar el incremento. Si se especifica un número sin los sufijos MB, KB o %, el valor predeterminado es MB.  
  
 Si *growth_increment* es NULL, el valor predeterminado es 10% y el valor de tamaño mínimo es 64 KB. El tamaño especificado se redondea al múltiplo de 64 KB más cercano.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución predeterminados a los miembros de la **sysadmin** rol fijo de servidor. Estos permisos no se pueden transferir.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, la base de datos `db1` se ha marcado como sospechosa durante la recuperación debido a un error de espacio de registro insuficiente (error 9002).  
  
```  
USE master;  
GO  
EXEC sp_add_log_file_recover_suspect_db db1, logfile2,  
'C:\Program Files\Microsoft SQL  
    Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_logfile2.ldf',   
    '1MB';  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_data_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-data-file-recover-suspect-db-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
