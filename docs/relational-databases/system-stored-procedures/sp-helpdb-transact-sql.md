---
title: sp_helpdb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6d514adfed27693456338ece6fa58638e319475
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47629813"
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Presenta información acerca de una base de datos especificada o de todas las bases de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname=** ] **'***nombre***'**  
 Es el nombre de la base de datos para el que se proporciona información. *nombre* es **sysname**, no tiene ningún valor predeterminado. Si *nombre* no se especifica, **sp_helpdb** informa sobre todas las bases de datos en el **sys.databases** vista de catálogo.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de base de datos.|  
|**valor de db_size**|**nvarchar(13)**|Tamaño total de la base de datos.|  
|**Propietario**|**sysname**|Bases de datos como propietario, **sa**.|  
|**dbid**|**smallint**|Id. de la base de datos.|  
|**Creado**|**nvarchar(11)**|Fecha de creación de la base de datos.|  
|**status**|**nvarchar(600)**|Lista de valores separados por comas de las opciones actualmente establecidas en la base de datos.<br /><br /> Las opciones con valores booleanos aparecen solamente si están habilitadas. Las opciones no booleanas se muestran con sus valores correspondientes en forma de *option_name*=*valor*.<br /><br /> Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|**COMPATIBILITY_LEVEL**|**tinyint**|Nivel de compatibilidad de la base de datos: 60, 65, 70, 80 o 90.|  
  
 Si *nombre* se especifica, hay un conjunto de resultados adicional que muestra la asignación de archivos de la base de datos especificado.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**nchar(128)**|Nombre de archivo lógico.|  
|**FileID**|**smallint**|Identificador de archivo.|  
|**Nombre de archivo**|**nchar(260)**|Nombre del archivo en el sistema operativo (nombre de archivo físico).|  
|**filegroup**|**nvarchar(128)**|Grupo al que pertenece el archivo.<br /><br /> NULL = El archivo es de registro. Nunca forma parte de un grupo de archivos.|  
|**size**|**nvarchar(18)**|Tamaño del archivo, en megabytes.|  
|**tamaño máximo**|**nvarchar(18)**|Tamaño máximo que puede alcanzar el archivo. El valor UNLIMITED en este campo indica que el archivo puede aumentar hasta que el disco esté lleno.|  
|**Crecimiento**|**nvarchar(18)**|Incremento de crecimiento del archivo. Esto indica la cantidad de espacio que se agrega al archivo que se necesita espacio cada vez.|  
|**Uso de**|**varchar (9)**|Uso del archivo. Para un archivo de datos, el valor es **"solo datos"** y para el archivo de registro es el valor **'iniciar solo'**.|  
  
## <a name="remarks"></a>Comentarios  
 El **estado** conjunto de columnas en el resultado de las opciones que se han establecido en ON en la base de datos de informes. No todas las opciones de base de datos notificadas por el **estado** columna. Para ver una lista completa de la configuración de opción de base de datos actual, use el **sys.databases** vista de catálogo.  
  
## <a name="permissions"></a>Permisos  
 Cuando se especifica una sola base de datos, la pertenencia a la **pública** se requiere el rol en la base de datos. Cuando no se especifica ninguna base de datos, pertenencia a la **pública** rol en el **maestro** se requiere la base de datos.  
  
 Si no se puede tener acceso a una base de datos, **sp_helpdb** muestra información del mensaje 15622 y toda la base de datos como sea posible.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-information-about-a-single-database"></a>A. Devolver información acerca de una sola base de datos  
 En el siguiente ejemplo se muestra información sobre la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. Devolver información acerca de todas las bases de datos  
 En el ejemplo siguiente se muestra información acerca de todas las bases de datos del servidor donde se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
