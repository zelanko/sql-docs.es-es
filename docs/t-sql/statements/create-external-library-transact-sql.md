---
title: Crear biblioteca externa (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: CREATE EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: f52205803e3ab44e7c72808255dbe93fd61de336
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="create-external-library-transact-sql"></a>Crear biblioteca externa (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

Carga los paquetes de R en una base de datos de la ruta de acceso de archivo o secuencia de bytes especificada.

Esta instrucción actúa como un mecanismo genérico para el Administrador de base de datos cargar los artefactos necesarios para los tiempos de ejecución de idiomas externos nueva (R, Python, Java, etc.) y las plataformas de sistemas operativos compatibles con [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. Actualmente se admiten solo el lenguaje R y la plataforma de Windows.

## <a name="syntax"></a>Sintaxis

```
CREATE EXTERNAL LIBRARY library_name  
    [ AUTHORIZATION owner_name ]  
FROM <file_spec> [,…2]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
(CONTENT = { <client_library_specifier> | <library_bits> }  
[, PLATFORM = WINDOWS ])  
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

Las bibliotecas se agregan a la base de datos como ámbito el usuario. Es decir, los nombres de biblioteca se consideran únicos dentro del contexto de un usuario específico o un propietario y nombres de biblioteca deben ser únicos para cada usuario. Por ejemplo, dos usuarios **RUser1** y **RUser2** pueden ambos individualmente y por separado cargar la biblioteca de R `ggplot2`.

**owner_name**

Especifica el nombre del usuario o rol que tiene la biblioteca externa. Si no se especifica, la propiedad se otorga al usuario actual.

Las bibliotecas que pertenezca al propietario de la base de datos se consideran globales para la base de datos y en tiempo de ejecución. En otras palabras, los propietarios de base de datos pueden crear bibliotecas que contienen un conjunto común de bibliotecas o paquetes que se comparten entre varios usuarios. Cuando se crea una biblioteca externa por un usuario distinto de la `dbo` usuario, la biblioteca externa es privada para que solo el usuario.

Cuando el usuario **RUser1** ejecuta un script de R, el valor de `libPath` puede contener varias rutas de acceso. La primera ruta de acceso siempre es la ruta de acceso a la biblioteca compartida creada por el propietario de la base de datos. La segunda parte del `libPath` especifica la ruta de acceso que contiene paquetes cargados individualmente por **RUser1**.

**file_spec**

Especifica el contenido del paquete para una plataforma específica. Se admite el artefacto de un solo archivo por cada plataforma.

El archivo puede especificarse en forma de una ruta de acceso local o la ruta de acceso de red.

Si lo desea, puede especificarse una plataforma de sistema operativo para el archivo. Artefacto de un solo archivo o el contenido se permite para cada plataforma de sistema operativo de un determinado idioma o en tiempo de ejecución.

**library_bits**

Especifica el contenido del paquete como un literal hexadecimal, similar a los ensamblados. Esta opción permite a los usuarios crear una biblioteca para modificar la biblioteca si dispone del permiso requerido, pero no tiene acceso de la ruta de acceso de archivo a cualquier carpeta que puede tener acceso el servidor.

**PLATAFORMA = WINDOWS**

Especifica la plataforma para el contenido de la biblioteca. El valor predeterminado es la plataforma de host en el que se ejecuta SQL Server. Por lo tanto, el usuario no tiene que especificar el valor. Es necesario en caso de que se admiten varias plataformas, o el usuario debe especificar una plataforma diferente. Windows es la única plataforma admitida.

## <a name="remarks"></a>Comentarios

Para el lenguaje R, al utilizar un archivo, los paquetes deben estar preparados en forma de archivos de almacenamiento comprimido con el. Código postal de extensión para Windows. Actualmente, solo la plataforma de Windows es compatible

El `CREATE EXTERNAL LIBRARY` instrucción solo carga los bits de la biblioteca en la base de datos. La biblioteca no está instalada realmente hasta que un usuario ejecuta un script externo después, mediante la ejecución de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  

Bibliotecas de carga en la instancia pueden ser público o privado. Si se crea la biblioteca de un miembro de `dbo`, la biblioteca es pública y se puede compartir con todos los usuarios. En caso contrario, la biblioteca es privada para que solo el usuario.

No se puede usar blobs como origen de datos en la versión de SQL Server 2017.

## <a name="permissions"></a>Permissions

Requiere la `CREATE ANY EXTERNAL LIBRARY` permiso.

Para modificar una biblioteca de requiere el permiso independiente, `ALTER ANY EXTERNAL LIBRARY`.

## <a name="examples"></a>Ejemplos

### <a name="a-add-an-external-library-to-a-database"></a>A. Agregar una biblioteca externa a una base de datos  

En el ejemplo siguiente se agrega una biblioteca externa denominada customPackage a una base de datos.

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

Después de la biblioteca se ha cargado correctamente a la instancia, un usuario ejecuta la `sp_execute_external_script` procedimiento para instalar la biblioteca.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
'
```

### <a name="b-installing-packages-with-dependencies"></a>B. Instalación de paquetes con dependencias

Si `packageB` tiene una dependencia en `packageA`, a continuación, siga los siguientes principios generales:

+ Cargue el paquete de destino y sus dependencias.

    Ambos paquetes deben estar en una carpeta que sea accesible para el servidor.

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    
    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    ```

+ Las dependencias se instalan en primer lugar.

    Si un paquete necesario `packageA` ya se ha cargado a la instancia, es necesario no se haya instalado por separado. Los requisitos de software `packageA` se instalará cuando `sp_execute_external_script` se ejecuta por primera vez para instalar el paquete `packageB`.

    Sin embargo, si los requisitos de software, `packageA`, no está disponible, la instalación del paquete de destino `packageB` se producirá un error.

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load packageB
    library(packageB)
    # call customPackageBFunc
    OutputDataSet <- customPackageBFunc()
    '
    with result sets (([result] int));    
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>C. Crear una biblioteca de una secuencia de bytes

En el ejemplo siguiente se crea una biblioteca pasando actualiza bits como un literal hexadecimal.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

### <a name="d-change-an-existing-package-library"></a>D. Cambiar una biblioteca de paquete existente

El `ALTER EXTERNAL LIBRARY` instrucción DDL se puede utilizar para agregar contenido nuevo de biblioteca o modificar el contenido existente de la biblioteca. Para modificar una biblioteca existente requiere el `ALTER ANY EXTERNAL LIBRARY` permiso.

Para obtener más información, consulte [ALTER biblioteca externa](alter-external-library-transact-sql.md).

### <a name="e-delete-a-package-library"></a>E. Eliminar una biblioteca de paquete

Para eliminar una biblioteca de paquete de la base de datos, ejecute la instrucción:

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

> [!NOTE]
> A diferencia de otras `DROP` instrucciones en [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)], esta instrucción admite un parámetro opcional que especifica la entidad de usuario. Esta opción permite a los usuarios con las funciones de propiedad eliminar las bibliotecas cargadas por usuarios normales.

## <a name="see-also"></a>Vea también

[BIBLIOTECA externa ALTER (Transact-SQL)](alter-external-library-transact-sql.md)  
[QUITAR biblioteca externa (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
