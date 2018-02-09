---
title: FileTableRootPath (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs:
- TSQL
helpviewer_keywords:
- FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1dd6d1b54d92142f3089b6323127257341ffe4d4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve la ruta de acceso UNC del nivel raíz de un objeto FileTable específico o de la base de datos actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FileTableRootPath ( [ ‘[schema_name.]FileTable_name’ ], @option )  
```  
  
## <a name="arguments"></a>Argumentos  
 *FileTable_name*  
 Nombre del FileTable. *FileTable_name* es de tipo **nvarchar**. Se trata de un parámetro opcional. El valor predeterminado es la base de datos actual. Especificar *schema_name* también es opcional. Puede pasar NULL como *FileTable_name* para usar el valor de parámetro predeterminado  
  
 *@option*  
 Expresión entera que define cómo se debe dar formato al componente de servidor de la ruta de acceso. *@option*puede tener uno de los siguientes valores:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|Devuelve el nombre del servidor convertido a formato NetBIOS, por ejemplo:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDB`<br /><br /> Es el valor predeterminado.|  
|**1**|Devuelve el nombre del servidor sin la conversión, por ejemplo:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDB`|  
|**2**|Devuelve la ruta de acceso al servidor completa, por ejemplo:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDB`|  
  
## <a name="return-type"></a>Tipo devuelto  
 **nvarchar(4000)**  
  
 Cuando la base de datos pertenece a un grupo de disponibilidad AlwaysOn, la **FileTableRootPath** función devuelve el nombre de red virtual (VNN) en lugar del nombre de equipo.  
  
## <a name="general-remarks"></a>Notas generales  
 El **FileTableRootPath** función devuelve NULL cuando se cumple alguna de las condiciones siguientes:  
  
-   El valor de *FileTable_name* no es válido.  
  
-   El autor de la llamada no tiene suficientes permisos para hacer referencia a la tabla especificada o a la base de datos actual.  
  
-   La opción FILESTREAM de *database_directory* no está establecida para la base de datos actual.  
  
 Para más información, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Para mantener independientes del equipo y de la base de datos actuales el código y las aplicaciones, evite escribir código basado en rutas de acceso absolutas de archivos. En su lugar, obtenga la ruta de acceso completa de un archivo en tiempo de ejecución mediante el uso de la **FileTableRootPath** y **GetFileNamespacePath** funciona conjuntamente, tal como se muestra en el ejemplo siguiente. De forma predeterminada, la función **GetFileNamespacePath** devuelve la ruta de acceso relativa del archivo en la ruta de acceso raíz de la base de datos.  
  
```sql  
USE MyDocumentDB;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 El **FileTableRootPath** función requiere:  
  
-   Permiso SELECT en el objeto FileTable para obtener la ruta de acceso raíz de un objeto FileTable específico.  
  
-   **db_datareader** o permiso superior para obtener la ruta de acceso raíz de la base de datos actual.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cómo llamar a la **FileTableRootPath** (función).  
  
```  
USE MyDocumentDB;  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB”  
SELECT FileTableRootPath();  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB\MyFileTable”  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB\MyFileTable”  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
