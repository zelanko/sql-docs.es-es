---
title: CREATE EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/25/2018
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
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: e28716314837225586cf4bd1f80a37c5c6b824ab
ms.sourcegitcommit: 6e819406554efbd17bbf84cf210d8ebeddcf772d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2018
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

Carga los paquetes de R en una base de datos desde la ruta de acceso de archivo o la secuencia de bytes especificada.

Esta instrucción actúa como un mecanismo genérico para que el administrador de base de datos pueda cargar los artefactos necesarios para cualquier tiempo de ejecución de lenguaje externo nuevo (R, Python, Java, etc.) y plataformas de sistemas operativos compatibles con [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. 

Actualmente, solo se admiten el lenguaje R y la plataforma Windows. Está previsto incluir la compatibilidad con Python y Linux en una versión posterior.

## <a name="syntax"></a>Sintaxis

```text
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

**library_name**

Las bibliotecas se agregan a la base de datos dentro del ámbito del usuario. Es decir, los nombres de biblioteca se consideran únicos dentro del contexto de un usuario o propietario específico, además de ser únicos también de cada usuario. Por ejemplo, dos usuarios, **RUser1** y **RUser2**, pueden cargar individualmente y por separado la biblioteca de R `ggplot2`.

Los nombres de biblioteca no se pueden asignar de forma arbitraria; en este sentido, los nombres de biblioteca deben ser los mismos que los nombres necesarios para cargar la biblioteca de R desde R.

**owner_name**

Especifica el nombre del usuario o rol que es propietario de la biblioteca externa. Si no se especifica, la propiedad se otorga al usuario actual.

Las bibliotecas que pertenecen al propietario de la base de datos se consideran globales en la base de datos y en tiempo de ejecución. Dicho de otro modo, los propietarios de bases de datos pueden crear bibliotecas que contienen un conjunto común de bibliotecas o paquetes que se comparten entre varios usuarios. Cuando un usuario distinto del usuario `dbo` crea una biblioteca externa, esta es privada exclusivamente de ese usuario.

Cuando el usuario **RUser1** ejecuta un script de R, el valor de `libPath` puede contener varias rutas de acceso. La primera ruta de acceso es siempre la ruta de acceso a la biblioteca compartida creada por el propietario de la base de datos. La segunda parte de `libPath` especifica la ruta de acceso que contiene paquetes cargados individualmente por **RUser1**.

**file_spec**

Especifica el contenido del paquete para una plataforma específica. Solo se admite un artefacto de archivo por cada plataforma.

El archivo se puede especifica como una ruta de acceso local o una ruta de acceso de red.

Opcionalmente, se puede especificar una plataforma de sistema operativo para el archivo. Solo se permite un artefacto de archivo o contenido para cada plataforma de sistema operativo para un determinado lenguaje o tiempo de ejecución.

**library_bits**

Especifica el contenido del paquete como un literal hexadecimal, similar a los ensamblados. 

Esta opción es útil si necesita crear una biblioteca o modificar una ya existente (y tiene los permisos necesarios para hacerlo), pero el sistema de archivos en el servidor está restringido y no puede copiar los archivos de la biblioteca en una ubicación a la que pueda tener acceso el servidor.

**PLATFORM = WINDOWS**

Especifica la plataforma para el contenido de la biblioteca. El valor se establece de forma predeterminada en la plataforma de host en la que SQL Server se ejecuta, con lo cual no es necesario que el usuario lo especifique. Es necesario en caso de que se admitan varias plataformas o si el usuario debe especificar una plataforma diferente. 

En SQL Server 2017, Windows es la única plataforma admitida.

## <a name="remarks"></a>Notas

En el lenguaje R, cuando se usa un archivo, los paquetes deben estar preparados en forma de archivos de almacenamiento comprimidos con la extensión .ZIP para Windows. Actualmente, solo se admite la plataforma Windows. 

La instrucción `CREATE EXTERNAL LIBRARY` carga los bits de biblioteca en la base de datos. La biblioteca se instala cuando un usuario ejecuta un script externo con [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y llama al paquete o a la biblioteca.

Las bibliotecas cargadas en la instancia pueden ser públicas o privadas. Si es un miembro de `dbo` quien ha creado la biblioteca, esta será pública y se podrá compartir con todos los usuarios. En caso contrario, será privada exclusivamente del usuario.

No se pueden usar blobs como origen de datos en la versión de SQL Server 2017.

## <a name="permissions"></a>Permisos

Requiere el permiso `CREATE ANY EXTERNAL LIBRARY`.

Para modificar una biblioteca, se necesita el permiso `ALTER ANY EXTERNAL LIBRARY`.

## <a name="examples"></a>Ejemplos

### <a name="a-add-an-external-library-to-a-database"></a>A. Agregar una biblioteca externa a una base de datos  

En el siguiente ejemplo se agrega una biblioteca externa denominada `customPackage` a una base de datos.

```sql
CREATE EXTERNAL LIBRARY customPackage
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip') WITH (LANGUAGE = 'R');
```  

Después de que la biblioteca se haya cargado correctamente en la instancia, un usuario ejecuta el procedimiento `sp_execute_external_script` para instalar esa biblioteca.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
```

### <a name="b-installing-packages-with-dependencies"></a>B. Instalar paquetes con dependencias

Si el paquete que se va a instalar tiene dependencias, es fundamental analizar las dependencias de primer y de segundo nivel, así como procurar que todos los paquetes necesarios estén disponibles _antes de_ intentar instalar el paquete de destino.

Por ejemplo, imagine que quiere instalar un nuevo paquete, `packageA`:

+ `packageA` tiene una dependencia en `packageB`.
+ `packageB` tiene una dependencia en `packageC`.

Para instalar `packageA` correctamente, debe crear bibliotecas para `packageB` y `packageC` al mismo tiempo que agrega `packageA` a SQL Server. Asegúrese de comprobar también las versiones de paquete necesarias.

En la práctica, las dependencias de paquete de los paquetes más conocidos suelen ser mucho más complicadas que en este sencillo ejemplo. Por ejemplo, ggplot2 podría necesitar más de 30 paquetes y estos, a su vez, podrían requerir más paquetes que no están disponibles en el servidor. Cualquier paquete que falte o versión de paquete incorrecta puede hacer que la instalación no se lleve a cabo.

Dado que puede ser difícil determinar todas las dependencias únicamente consultando el manifiesto del paquete, se recomienda usar un paquete como [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) o [iGraph](http://igraph.org/redirect.html) para identificar todos los paquetes que pueden ser necesarios para que la instalación se lleve a cabo correctamente.

+ Cargue el paquete de destino y sus dependencias. Todos los archivos deben estar en una carpeta que sea accesible para el servidor.

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    GO

    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    GO

    CREATE EXTERNAL LIBRARY packageC FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageC.zip') 
    WITH (LANGUAGE = 'R');
    GO
    ```

+ Instale primero los paquetes necesarios.

    Si un paquete necesario ya se ha cargado en la instancia, no tendrá que agregarlo de nuevo. Bastará con comprobar que su versión es la correcta. 
    
    Los paquetes necesarios `packageC` y `packageB` se instalan en el orden correcto cuando `sp_execute_external_script` se ejecuta por primera vez para instalar el paquete `packageA`.

    Pero si alguno de los paquetes necesarios no está disponible, la instalación del paquete de destino `packageA` no se llevará a cabo.

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load the desired package packageA
    library(packageA)
    # call function from package
    OutputDataSet <- packageA.function()
    '
    with result sets (([result] int));    
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>C. Crear una biblioteca a partir de una secuencia de bytes

Si no tiene la posibilidad de guardar los archivos del paquete en una ubicación en el servidor, también puede pasar el contenido del paquete en una variable. En el siguiente ejemplo se crea una biblioteca pasando los bits como un literal hexadecimal.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

Los valores hexadecimales se han truncado aquí para facilitar la lectura.

### <a name="d-change-an-existing-package-library"></a>D. Cambiar una biblioteca de paquetes existente

La instrucción DDL `ALTER EXTERNAL LIBRARY` sirve para agregar nuevo contenido de biblioteca o para modificar el contenido de biblioteca ya existente. Para modificar una biblioteca existente, se necesita el permiso `ALTER ANY EXTERNAL LIBRARY`.

Para más información, vea [ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md).

### <a name="e-delete-a-package-library"></a>E. Eliminar una biblioteca de paquetes

Ejecute la siguiente instrucción para eliminar una biblioteca de paquetes de la base de datos:

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

> [!NOTE]
> A diferencia de otras instrucciones `DROP` de [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)], esta instrucción permite especificar un parámetro opcional que indica la entidad del usuario. Con esta opción, los usuarios con roles de propiedad pueden eliminar las bibliotecas cargadas por usuarios normales.

## <a name="see-also"></a>Vea también

[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
