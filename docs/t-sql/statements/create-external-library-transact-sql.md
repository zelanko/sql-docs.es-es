---
title: Crear biblioteca externa (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f11a6b7633be392e1f789e12c43f2e5d6e56b47
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-library-transact-sql"></a>Crear biblioteca externa (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

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

**PLATAFORMA = WINDOWS**

Especifica la plataforma para el contenido de la biblioteca. El valor predeterminado es la plataforma de host en el que se ejecuta SQL Server. Por lo tanto, el usuario no tiene que especificar el valor. Es necesario en caso de que se admiten varias plataformas, o el usuario debe especificar una plataforma diferente. Windows es la única plataforma admitida.

## <a name="remarks"></a>Comentarios

Para el lenguaje R, paquetes deben estar preparados en forma de archivos de almacenamiento comprimido con el. Código postal de extensión para Windows. Actualmente, solo la plataforma de Windows es compatible.  

El `CREATE EXTERNAL LIBRARY` instrucción solo carga los bits de la biblioteca en la base de datos. La biblioteca no está instalada realmente hasta que un usuario ejecuta un script externo después, mediante la ejecución de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  

## <a name="permissions"></a>Permissions  
Requiere la `CREATE EXTERNAL LIBRARY` permiso.  

## <a name="examples"></a>Ejemplos

### <a name="a-add-an-external-library-to-a-database"></a>A. Agregar una biblioteca externa a una base de datos  
En el ejemplo siguiente se agrega una biblioteca externa denominada customPackage a una base de datos.   
```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  
A continuación, ejecute el `sp_execute_external_script` procedimiento para instalar la biblioteca.  
```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)

# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
with result sets (([result] int));    
```

### <a name="b-installing-packages-with-dependencies"></a>B. Instalación de paquetes con dependencias

Si `packageB` tiene una dependencia en `packageA`, a continuación, por ejemplo, el código sigue estas entidades de seguridad generales:   
```
CREATE EXTERNAL LIBRARY packageA 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R'); 

CREATE EXTERNAL LIBRARY packageB FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R');
```

`packageA`y `packageB` están instalados cuando `sp_execute_external_script` se ejecuta por primera vez.   
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

Para que funcione, la carpeta donde se guardarán los paquetes debe ser accesible en el servidor. 

### <a name="change-an-existing-package-library"></a>Cambiar una biblioteca de paquete existente

El `ALTER EXTERNAL LIBRARY` instrucción DDL se puede utilizar para agregar contenido nuevo de biblioteca o modificar el contenido existente de la biblioteca.   

### <a name="delete-a-package-library"></a>Eliminar una biblioteca de paquete

Para eliminar una biblioteca de paquete de la base de datos, ejecute la instrucción:

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

> [!NOTE]
> A diferencia de otras `DROP` instrucciones en [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)], esta instrucción admite un parámetro opcional que especifica la entidad de usuario. Esta opción permite a los usuarios con las funciones de propiedad eliminar las bibliotecas cargadas por usuarios normales. 

## <a name="see-also"></a>Vea también  
[BIBLIOTECA externa ALTER (Transact-SQL)](alter-external-library-transact-sql.md)  
[QUITAR biblioteca externa (Transact-SQL)](drop-external-library-transact-sql.md)  
[Sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[Sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

