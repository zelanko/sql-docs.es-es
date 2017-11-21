---
title: FILEPROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILEPROPERTY_TSQL
- FILEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- names [SQL Server], files
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTY function
- file names [SQL Server], FILEPROPERTY
ms.assetid: b82244ed-d623-431f-aa06-8017349d847f
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7078fecb77bad44fd6aa4c3ce0baf9565f1d6d3f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="fileproperty-transact-sql"></a>FILEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor de una propiedad de nombre de archivo especificada al especificar un nombre de archivo en la base de datos actual y un nombre de propiedad. Devuelve NULL para los archivos que no estén en la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FILEPROPERTY ( file_name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_name*  
 Es una expresión que contiene el nombre del archivo asociado a la base de datos actual de la que se va a devolver información de propiedades. *file_name* es **nchar(128)**.  
  
 *propiedad*  
 Es una expresión que contiene el nombre de la propiedad de archivo que se va a devolver. *propiedad* es **varchar (128)**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|Valor devuelto|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|El grupo de archivos es de solo lectura.|1 = True<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsPrimaryFile**|El archivo es el archivo principal.|1 = True<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsLogFile**|El archivo es un archivo de registro.|1 = True<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**SpaceUsed**|Cantidad de espacio utilizada por el archivo especificado.|Número de páginas asignadas en el archivo.|  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 *file_name* corresponde a la **nombre** columna en el **sys.master_files** o **sys.database_files** vista de catálogo.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve el valor de la propiedad `IsPrimaryFile` del nombre de archivo `AdventureWorks_Data` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
  
SELECT FILEPROPERTY('AdventureWorks2012_Data', 'IsPrimaryFile')AS [Primary File];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Primary File   
-------------  
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [FILEGROUPPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

