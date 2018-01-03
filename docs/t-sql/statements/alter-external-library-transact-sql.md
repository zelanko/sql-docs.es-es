---
title: ALTER biblioteca externa (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 28a62f00b479506e919faf2cbdbf1202045192eb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="alter-external-library-transact-sql"></a>BIBLIOTECA externa ALTER (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Modifica el contenido de una biblioteca externa de paquete existente.

## <a name="syntax"></a>Sintaxis

```
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = 'R' )
[ ; ]

<file_spec> ::=
{
(CONTENT = { <client_library_specifier> | <library_bits> | NONE}
[, PLATFORM = WINDOWS )
}

<client_library_specifier> :: =
  '[\\computer_name\]share_name\[path\]manifest_file_name'
| '[local_path\]manifest_file_name'
| '<relative_path_in_external_data_source>'

<library_bits> :: =
{ varbinary_literal | varbinary_expression }
```

### <a name="arguments"></a>Argumentos

**nombre_de_biblioteca**

Especifica el nombre de una biblioteca de paquete existente. Las bibliotecas tienen como ámbito el usuario. Es decir, nombres de las bibliotecas se consideran únicos dentro del contexto de un usuario específico o un propietario.

**owner_name**

Especifica el nombre del usuario o rol que tiene la biblioteca externa.

**file_spec**

Especifica el contenido del paquete para una plataforma específica. Se admite el artefacto de un solo archivo por cada plataforma.

El archivo puede especificarse en forma de una ruta de acceso local o una ruta de red. Si se especifica la opción de origen de datos, el nombre de archivo puede ser una ruta de acceso relativa con respecto a la del contenedor al que hace referencia en el `EXTERNAL DATA SOURCE`.

Si lo desea, puede especificarse una plataforma de sistema operativo para el archivo. Artefacto de un solo archivo o el contenido se permite para cada plataforma de sistema operativo de un determinado idioma o en tiempo de ejecución.

**DATA_SOURCE = external_data_source_name**

Especifica el nombre del origen de datos externo que contiene la ubicación del archivo de biblioteca. Esta ubicación debe hacer referencia a una ruta de acceso de almacenamiento de blobs de Azure. Para crear un origen de datos externo, use [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](create-external-data-source-transact-sql.md).

> [!IMPORTANT] 
> Actualmente, no se admiten blobs como origen de datos en la versión de SQL Server 2017.

**library_bits**

Especifica el contenido del paquete como un literal hexadecimal, similar a los ensamblados. Esta opción permite a los usuarios crear una biblioteca para modificar la biblioteca si dispone del permiso requerido, pero no tiene acceso de la ruta de acceso de archivo a cualquier carpeta que puede tener acceso el servidor.

**PLATAFORMA = WINDOWS**

Especifica la plataforma para el contenido de la biblioteca. Este valor es necesario para modificar una biblioteca para agregar una plataforma diferente. Windows es la única plataforma admitida.

## <a name="remarks"></a>Comentarios

Para el lenguaje R, paquetes deben estar preparados en forma de archivos de almacenamiento comprimido con el. Código postal de extensión para Windows. Actualmente, solo la plataforma de Windows es compatible.  

El `ALTER EXTERNAL LIBRARY` instrucción solo carga los bits de la biblioteca en la base de datos. La biblioteca modificada no se instala realmente hasta que un usuario ejecuta un script externo después, mediante la ejecución de [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="permissions"></a>Permissions

Requiere la `ALTER ANY EXTERNAL LIBRARY` permiso. Los usuarios que crean una biblioteca externa, puede modificar esa biblioteca externa.

## <a name="examples"></a>Ejemplos

Los ejemplos siguientes se modifica una biblioteca externa denominada customPackage.

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. Reemplace el contenido de una biblioteca mediante un archivo

En el ejemplo siguiente se modifica una biblioteca externa denominada customPackage, mediante un archivo comprimido que contiene los bits actualizados.

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

Para instalar la biblioteca actualizada, ejecute el procedimiento almacenado `sp_execute_external_script`.

```sql   
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
WITH RESULT SETS (([result] int));
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. Modificar una biblioteca mediante una secuencia de bytes

En el ejemplo siguiente se modifica la biblioteca existente pasando los nuevos bits como un hexadecimal literal.

```SQL
ALTER EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

## <a name="see-also"></a>Vea también  

[Crear biblioteca externa (Transact-SQL)](create-external-library-transact-sql.md)
[quitar biblioteca externa (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
