---
title: ALTER EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33270c8ccc490a400db45b6525d8c6002d974f3a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583178"
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Modifica el contenido de una biblioteca de paquetes externa existente.

> [!NOTE]
> En SQL Server 2017, se admiten el lenguaje R y la plataforma Windows. En SQL Server 2019 CTP 2.4 se admiten R, Python, Java y Linux en la plataforma Windows. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2019"></a>Sintaxis para SQL Server 2019

```text
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = <language> )
[ ; ]

<file_spec> ::=
{
    (CONTENT = { <client_library_specifier> | <library_bits> | NONE}
    [, PLATFORM = <platform> )
}

<client_library_specifier> :: =
{
      '[\\computer_name\]share_name\[path\]manifest_file_name'
    | '[local_path\]manifest_file_name'
    | '<relative_path_in_external_data_source>'
}

<library_bits> :: =
{ 
      varbinary_literal 
    | varbinary_expression 
}

<platform> :: = 
{
      WINDOWS
    | LINUX
}

<language> :: = 
{
      'R'
    | 'Python'
    | 'Java'
}
```
::: moniker-end
::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2017"></a>Sintaxis para SQL Server 2017

```text
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
{
      '[\\computer_name\]share_name\[path\]manifest_file_name'
    | '[local_path\]manifest_file_name'
    | '<relative_path_in_external_data_source>'
}

<library_bits> :: =
{ 
      varbinary_literal 
    | varbinary_expression 
}
```
::: moniker-end

### <a name="arguments"></a>Argumentos

**library_name**

Especifica el nombre de una biblioteca de paquetes existente. Las bibliotecas tienen como ámbito el usuario. Los nombres de biblioteca deben ser únicos dentro del contexto de un usuario o propietario específico.

El nombre de biblioteca no se puede asignar de forma arbitraria. Es decir, se debe usar el nombre que el tiempo de ejecución que realiza la llamada espera cuando se carga el paquete.

**owner_name**

Especifica el nombre del usuario o rol que es propietario de la biblioteca externa.

**file_spec**

Especifica el contenido del paquete para una plataforma específica. Solo se admite un artefacto de archivo por cada plataforma.

El archivo se puede especificar como una ruta de acceso local o una ruta de acceso de red. Si se especifica la opción de origen de datos, el nombre de archivo puede ser una ruta de acceso relativa con respecto al contenedor al que hace referencia en el `EXTERNAL DATA SOURCE`.

Opcionalmente, se puede especificar una plataforma de sistema operativo para el archivo. Solo se permite un artefacto de archivo o contenido para cada plataforma de sistema operativo para un determinado lenguaje o tiempo de ejecución.

**library_bits**

Especifica el contenido del paquete como un literal hexadecimal, similar a los ensamblados. 

Esta opción es útil si se dispone del permiso requerido para modificar una biblioteca, pero el acceso de archivo en el servidor está restringido y no se puede guardar el contenido en una ruta de acceso a la que el servidor pueda tener acceso.

En su lugar, se puede pasar el contenido del paquete como una variable en formato binario.

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
**PLATFORM = WINDOWS**

Especifica la plataforma para el contenido de la biblioteca. Este valor es obligatorio al modificar una biblioteca para agregar una plataforma diferente. En SQL Server 2017, Windows es la única plataforma admitida.

::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**PLATFORM**

Especifica la plataforma para el contenido de la biblioteca. Este valor es obligatorio al modificar una biblioteca para agregar una plataforma diferente. En SQL Server 2019, Windows y Linux son las únicas plataformas admitidas.

**language**

Especifica el lenguaje del paquete. El valor puede ser **R**, **Python** o **Java**.
::: moniker-end

## <a name="remarks"></a>Notas

::: moniker range=">=sql-server-2017 <=sql-server-2017||=sqlallproducts-allversions"
Para el lenguaje R, los paquetes deben estar preparados en forma de archivos de almacenamiento comprimidos con la extensión .ZIP para Windows. En SQL Server 2017, Windows es la única plataforma admitida.  
::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
En el lenguaje R, cuando se usa un archivo, los paquetes deben estar preparados en forma de archivos de almacenamiento comprimidos con la extensión .ZIP. 

Para el lenguaje Python, el paquete en un archivo .whl o .zip se debe preparar como un archivo comprimido. Si el paquete ya es un archivo .zip, se debe incluir en un nuevo archivo .zip. En la actualidad no se permite la carga directa de un paquete como archivo .whl o .zip.
::: moniker-end

La instrucción `ALTER EXTERNAL LIBRARY` solo carga los bits de biblioteca en la base de datos. La biblioteca modificada se instala cuando un usuario ejecuta código en el [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) que llama a la biblioteca.

## <a name="permissions"></a>Permisos

De forma predeterminada, el usuario **dbo** o cualquier miembro del rol **db_owner** tiene permiso para ejecutar ALTER EXTERNAL LIBRARY. Además, el usuario que crea una biblioteca externa puede modificarla.

## <a name="examples"></a>Ejemplos

En los ejemplos siguientes se cambia una biblioteca externa denominada `customPackage`.

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. Sustitución del contenido de una biblioteca mediante un archivo

En el ejemplo siguiente se modifica una biblioteca externa denominada `customPackage`, mediante un archivo comprimido que contiene los bits actualizados.

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
@script=N'library(customPackage)'
;
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para el lenguaje Python en SQL Server 2019, el ejemplo también funciona si se reemplaza `'R'` con `'Python'`.
::: moniker-end
### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. Modificación de una biblioteca existente mediante un flujo de bytes

En el ejemplo siguiente se modifica la biblioteca existente pasando los nuevos bits como un literal hexadecimal.

```SQL
ALTER EXTERNAL LIBRARY customLibrary 
SET (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Para el lenguaje Python en SQL Server 2019, el ejemplo también funciona si se reemplaza `'R'` con `'Python'`.
::: moniker-end

> [!NOTE]
> En este ejemplo de código solo se muestra la sintaxis; el valor binario de `CONTENT =` se ha truncado para mejorar la lectura y no se puede crear una biblioteca funcional. El contenido real de la variable binaria sería mucho más largo.

## <a name="see-also"></a>Vea también

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md) 
