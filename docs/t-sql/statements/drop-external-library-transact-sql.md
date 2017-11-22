---
title: QUITAR biblioteca externa (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: DROP EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: c157270e83ccfd3277356863b26c49222691e9e3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="drop-external-library-transact-sql"></a>QUITAR biblioteca externa (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Elimina una biblioteca de paquete existente.

## <a name="syntax"></a>Sintaxis  

```
DROP EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ];  
```

### <a name="arguments"></a>Argumentos

**nombre_de_biblioteca**

Especifica el nombre de una biblioteca de paquete existente.

Las bibliotecas tienen como ámbito el usuario. Es decir, nombres de las bibliotecas se consideran únicos dentro del contexto de un usuario específico o un propietario.

**owner_name**

Especifica el nombre del usuario o rol que tiene la biblioteca externa.

Los propietarios de base de datos pueden eliminar bibliotecas creadas por otros usuarios.

### <a name="return-values"></a>Valores devueltos

Si la instrucción se ejecutó correctamente, se devuelve un mensaje informativo.

## <a name="remarks"></a>Comentarios

A diferencia de otras `DROP` las instrucciones en SQL Server, esta instrucción admite la especificación de una cláusula authorization opcional. Esto permite **dbo** o los usuarios de la **db_owner** rol para quitar una biblioteca de paquetes cargados por un usuario normal en la base de datos.

## <a name="examples"></a>Ejemplos

Agregar un paquete de R personalizado, denominado `customPackage`, una base de datos:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 'C:\Users\Username\CustomPackages\customPackage.zip';
```

Eliminar el `customPackage` biblioteca.

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

## <a name="see-also"></a>Vea también  
[Crear biblioteca externa (Transact-SQL)](create-external-library-transact-sql.md)  
[BIBLIOTECA externa ALTER (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

