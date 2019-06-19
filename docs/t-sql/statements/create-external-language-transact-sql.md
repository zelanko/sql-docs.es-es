---
title: CREATE EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
ms.technology: t-sql
ms.topic: language-reference
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 223388d4a3c61dfb90ac9fa5434e9149bc25fae3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65994983"
---
# <a name="create-external-language-transact-sql"></a>CREATE EXTERNAL LANGUAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Registra las extensiones de lenguaje externo en la base de datos desde la secuencia de bytes o la ruta de acceso de archivo especificada. Esta instrucción actúa como un mecanismo genérico para que el administrador de base de datos pueda registrar las extensiones del lenguaje externo nuevo en cualquier plataforma de sistema operativo compatible con SQL Server.

> [!NOTE]
> **R** y **Python** son nombres reservados y no se puede crear ningún lenguaje externo con esos nombres.

## <a name="syntax"></a>Sintaxis

```text
CREATE EXTERNAL LANGUAGE language_name  
[ AUTHORIZATION owner_name ]  
FROM <file_spec> [ ,...2 ]  
WITH (<option_spec>)
[ ; ]  

<file_spec> ::=  
{
    ( CONTENT = { <external_lang_specifier> | <content_bits>,
    FILE_NAME = <external_lang_file_name>
    [ , PLATFORM = <platform> ]
    [ , PARAMETERS = <external_lang_parameters> ]
    [ , ENVIRONMENT_VARIABLES = <external_lang_env_variables> )
}

<external_lang_specifier> :: =  
{
    '[file_path\]os_file_name'  
}

<content_bits> :: =  
{
    varbinary_literal
    | varbinary_expression
}

<external_lang_file_name> :: =  
'extension_file_name'


<platform> :: =
{
    WINDOWS
  | LINUX
}

<external_lang_parameters> :: =  
'extension_specific_parameters'
```

### <a name="arguments"></a>Argumentos

**language_name**

Los lenguajes son objetos del ámbito de la base de datos. Los nombres del lenguaje deben ser únicos en la base de datos.

**owner_name**

Especifica el nombre del usuario o rol que es propietario del lenguaje externo. Si no se especifica, la propiedad se otorga al usuario actual. Dependiendo de los permisos, puede ser que haya que conceder permisos explícitos a otros usuarios para ejecutar scripts mediante un lenguaje específico.

**file_spec**

Especifica el contenido de la extensión del lenguaje. Solo se permite un argumento filespec para un lenguaje específico por plataforma.

**external_lang_specifier**

La ruta de acceso completa al archivo .zip o tar.gz que contiene el código de las extensiones. Este contenido puede ser una ruta de acceso a un archivo .zip (en Windows) o tar.gz (en Linux).

**content_bits**

Especifica el contenido del lenguaje como un literal hexadecimal, similar a los ensamblados.

Esta opción es útil si necesita crear un lenguaje o modificar uno ya existente (y tiene los permisos necesarios para hacerlo), pero el sistema de archivos en el servidor está restringido y no puede copiar los archivos de la biblioteca en una ubicación a la que pueda tener acceso el servidor.

**external_lang_file_name**

Nombre del archivo con extensión .dll o .so. Es necesario para identificar el archivo correcto en casos donde hay varios archivos .dll o .so en el <external_lang_specifier> .zip o tar.gz.

**external_lang_parameters**

Proporciona la posibilidad de conceder un conjunto de parámetros al tiempo de ejecución del lenguaje externo. Los valores de los parámetros se proporcionan para el tiempo de ejecución externo una vez iniciado el proceso externo. Sin embargo, la extensión del lenguaje puede acceder a las variables de entorno antes del inicio del proceso externo.

**external_lang_env_variables**

Proporciona la posibilidad de conceder un conjunto de variables de entorno al tiempo de ejecución del lenguaje externo antes del inicio del proceso externo. Un ejemplo de una variable de entorno sería, por ejemplo, el directorio principal del mismo tiempo de ejecución. Por ejemplo: JRE_HOME.

**platform**

Este parámetro es necesario para escenarios de sistemas operativos híbridos. En una arquitectura híbrida, el lenguaje debe registrarse una vez por cada plataforma. El nombre de la plataforma y del lenguaje será la clave única por el lenguaje externo. Si no se especifica ninguna plataforma, se usará el sistema operativo actual.

## <a name="remarks"></a>Notas

En CTP 3.0, no se admite **PARAMETERS** ni **ENVIRONMENT_VARIABLES**.

## <a name="permissions"></a>Permisos

Requiere el permiso `CREATE EXTERNAL LANGUAGE`. De forma predeterminada, cualquier usuario que tenga **dbo** y sea miembro del rol **db_owner** tiene permisos para crear un lenguaje externo. Para todos los demás usuarios, debe concederles explícitamente permiso con una instrucción [GRANT](https://docs.microsoft.com/sql/t-sql/statements/grant-database-permissions-transact-sql) y especificando CREATE EXTERNAL LANGUAGE como privilegio.

Para modificar una biblioteca, se necesita el permiso `ALTER ANY EXTERNAL LANGUAGE`.

### <a name="execute-external-script-permission"></a>Permiso EXECUTE EXTERNAL SCRIPT

En SQL Server 2019, estamos introduciendo permisos EXECUTE EXTERNAL SCRIPT, para que se pueda conceder la ejecución de scripts externos en determinados idiomas. Anteriormente, solo disponíamos del permiso de base de datos EXECUTE ANY EXTERNAL SCRIPT, que no permitía conceder el permiso de ejecución en un idioma específico.

Esto significa que es necesario conceder permiso a los usuarios que no son de **dbo** para ejecutar un lenguaje específico:

```sql
GRANT EXECUTE EXTERNAL SCRIPT ON EXTERNAL LANGUAGE ::language_name 
TO database_principal_name;
```

### <a name="reference-permissions-to-external-libraries"></a>Permisos de referencia para bibliotecas externas

De forma similar a los ensamblados, los lenguajes externos requieren permisos de referencia para que se establezca un vínculo entre bibliotecas externas y lenguajes externos. Por ejemplo, si se va a quitar un lenguaje externo, en primer lugar el usuario debe asegurarse de que se quitarán todas las bibliotecas externas que hacen referencia a dicho idioma. Puede ver el lenguaje externo en una jerarquía, como un objeto de nivel más alto que las bibliotecas externas.

## <a name="examples"></a>Ejemplos

### <a name="a-create-an-external-language-in-a-database"></a>A. Crear un lenguaje externo en una base de datos  

En el ejemplo siguiente se agrega un lenguaje externo denominada Java a una base de datos de SQL Server en Windows.

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

### <a name="b-create-an-external-language-for-both-windows-and-linux"></a>B. Crear un lenguaje externo para Windows y Linux

Puede especificar hasta dos `<file_spec>`, uno para Windows y otro para Linux.

```sql
CREATE EXTERNAL LANGUAGE Java
FROM
(CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll', PLATFORM = WINDOWS),
(CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so', PLATFORM = LINUX);
GO
```

## <a name="see-also"></a>Vea también

[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[DROP EXTERNAL LANGUAGE (Transact-SQL)](drop-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
