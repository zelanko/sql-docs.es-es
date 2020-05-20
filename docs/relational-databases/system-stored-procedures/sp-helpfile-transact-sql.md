---
title: sp_helpfile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 812be95c9584e75d8452c946d1935625468a79a1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828341"
---
# <a name="sp_helpfile-transact-sql"></a>sp_helpfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve los nombres físicos y los atributos de los archivos asociados con la base de datos actual. Utilice este procedimiento almacenado para determinar los nombres de los archivos que vaya a adjuntar al servidor o a separar del mismo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filename = ] 'name'`Es el nombre lógico de cualquier archivo de la base de datos actual. *Name* es de **tipo sysname y su**valor predeterminado es NULL. Si no se especifica *Name* , se devuelven los atributos de todos los archivos de la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre de archivo lógico.|  
|**ID**|**smallint**|Identificador numérico del archivo. No se devuelve si *name* se especifica name *.*|  
|**extensión**|**NCHAR (260)**|Nombre de archivo físico.|  
|**filegroup**|**sysname**|Grupo al que pertenece el archivo.<br /><br /> NULL = El archivo es un archivo de registro. Nunca forma parte de un grupo de archivos.|  
|**size**|**nvarchar(15**|Tamaño del archivo en kilobytes.|  
|**tamañomáximo**|**nvarchar(15**|Tamaño máximo que puede alcanzar el archivo. El valor UNLIMITED en este campo indica que el archivo puede aumentar hasta que el disco esté lleno.|  
|**crezca**|**nvarchar(15**|Incremento de crecimiento del archivo. Indica la cantidad de espacio que se agrega al archivo cada vez que se necesita espacio nuevo.<br /><br /> 0 = El archivo tiene un tamaño fijo y no aumenta.|  
|**uso**|**VARCHAR (9)**|En el caso del archivo de datos, el valor es **' solo datos '** y, para el archivo de registro, el valor es **' solo registro '**.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve información acerca de los archivos de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Motor de base de datos procedimientos almacenados &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [Sys. database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [Sys. master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Sys. grupos de archivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Archivos y grupos de archivos de base de datos](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
