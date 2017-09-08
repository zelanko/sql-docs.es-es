---
title: QUITAR biblioteca externa (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 143e9ac0dbe042ebbb034dff847cfc01ea5a5411
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-library-transact-sql"></a>QUITAR biblioteca externa (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

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

Agregar ggplot2 a una base de datos:

```sql
CREATE EXTERNAL LIBRARY ggplot2 
FROM 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\ggplot2.zip';
```

Eliminar la biblioteca ggplot2.

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

## <a name="see-also"></a>Vea también  
[Crear biblioteca externa (Transact-SQL)](create-external-library-transact-sql.md)  
[BIBLIOTECA externa ALTER (Transact-SQL)](alter-external-library-transact-sql.md)  
[Sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[Sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  


