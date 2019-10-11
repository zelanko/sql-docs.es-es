---
title: FileTableRootPath (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs:
- TSQL
helpviewer_keywords:
- FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
author: rothja
ms.author: jroth
ms.openlocfilehash: 10b4aa19b86530213f852ea90f959a1d7ef6c74f
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251233"
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve la ruta de acceso UNC del nivel raíz de un objeto FileTable específico o de la base de datos actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FileTableRootPath ( [ '[schema_name.]FileTable_name' ], @option )  
```  
  
## <a name="arguments"></a>Argumentos  
 *FileTable_name*  
 Nombre del FileTable. *FileTable_name* es de tipo **nvarchar**. Se trata de un parámetro opcional. El valor predeterminado es la base de datos actual. Especificar *schema_name* también es opcional. Puede pasar NULL para que *FileTable_name* use el valor de parámetro predeterminado.  
  
 *@no__t 1option*  
 Expresión entera que define cómo se debe dar formato al componente de servidor de la ruta de acceso. *\@option* puede tener uno de los siguientes valores:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Devuelve el nombre del servidor convertido a formato NetBIOS, por ejemplo:<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> Este es el valor predeterminado.|  
|**1**|Devuelve el nombre del servidor sin la conversión, por ejemplo:<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|Devuelve la ruta de acceso al servidor completa, por ejemplo:<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>Tipo devuelto  
 **nvarchar(4000)**  
  
 Cuando la base de datos pertenece a un grupo de disponibilidad de Always On, la función **FileTableRootPath** devuelve el nombre de la red virtual (VNN) en lugar del nombre del equipo.  
  
## <a name="general-remarks"></a>Notas generales  
 La función **FileTableRootPath** devuelve NULL cuando se cumple una de las condiciones siguientes:  
  
-   El valor de *FileTable_name* no es válido.  
  
-   El autor de la llamada no tiene suficientes permisos para hacer referencia a la tabla especificada o a la base de datos actual.  
  
-   No se ha establecido la opción FILESTREAM de *database_directory* para la base de datos actual.  
  
 Para más información, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Para mantener independientes del equipo y de la base de datos actuales el código y las aplicaciones, evite escribir código basado en rutas de acceso absolutas de archivos. En su lugar, obtenga la ruta de acceso completa de un archivo en tiempo de ejecución mediante las funciones **FileTableRootPath** y **GetFileNamespacePath** , como se muestra en el ejemplo siguiente. De forma predeterminada, la función **GetFileNamespacePath** devuelve la ruta de acceso relativa del archivo en la ruta de acceso raíz de la base de datos.  
  
```sql  
USE MyDocumentDatabase;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 La función **FileTableRootPath** requiere:  
  
-   Permiso SELECT en el objeto FileTable para obtener la ruta de acceso raíz de un objeto FileTable específico.  
  
-   **db_datareader** o el permiso superior para obtener la ruta de acceso raíz de la base de datos actual.  
  
## <a name="examples"></a>Ejemplos  
 En los siguientes ejemplos se muestra cómo llamar a la función **FileTableRootPath** .  
  
```  
USE MyDocumentDatabase;  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase"  
SELECT FileTableRootPath();  
  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable"  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable"  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
