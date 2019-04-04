---
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86609c0cb3e66397c4c8c8f3a09fba64b14089e4
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492827"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Elimina una biblioteca de paquetes existente. Los tiempos de ejecución externos admitidos, como R, Python o Java, usan bibliotecas de paquetes.

> [!NOTE]
> En SQL Server 2017, se admiten el lenguaje R y la plataforma Windows. En SQL Server 2019 CTP 2.4 se admiten R, Python, Java y Linux en la plataforma Windows. 

## <a name="syntax"></a>Sintaxis

```sql
DROP EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ];
```

### <a name="arguments"></a>Argumentos

**library_name**

Especifica el nombre de una biblioteca de paquetes existente.

Las bibliotecas tienen como ámbito el usuario. Los nombres de biblioteca deben ser únicos dentro del contexto de un usuario o propietario específico.

**owner_name**

Especifica el nombre del usuario o rol que es propietario de la biblioteca externa.

Los propietarios de bases de datos pueden eliminar bibliotecas creadas por otros usuarios.

## <a name="permissions"></a>Permisos

Para eliminar una biblioteca necesita el privilegio ALTER ANY EXTERNAL LIBRARY. De forma predeterminada, cualquier propietario de base de datos o el propietario del objeto también puede eliminar una biblioteca externa.

### <a name="return-values"></a>Valores devueltos

Si la instrucción se ejecuta correctamente, se devuelve un mensaje informativo.

## <a name="remarks"></a>Notas

A diferencia de otras instrucciones `DROP` de SQL Server, esta instrucción admite la especificación de una cláusula AUTHORIZATION opcional. Esto permite a los **dbo** o a los usuarios con el rol **db_owner** quitar una biblioteca de paquetes cargada por un usuario normal en la base de datos.

## <a name="examples"></a>Ejemplos

Agregue el paquete de R personalizado, `customPackage`, a una base de datos:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```

Elimine la biblioteca `customPackage`.

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>Vea también

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

