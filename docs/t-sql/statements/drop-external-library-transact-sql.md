---
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
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
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: 2758b728792c48ef309eb08f545ea4a6953c9e9d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "73530819"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Elimina una biblioteca de paquetes existente. Los tiempos de ejecución externos admitidos, como R, Python o Java, usan bibliotecas de paquetes.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
> [!NOTE]
> En SQL Server 2017, se admiten el lenguaje R y la plataforma Windows. En SQL Server 2019 y versiones posteriores se admiten R, Python y Java en las plataformas Windows y Linux. 
::: moniker-end

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

## <a name="remarks"></a>Observaciones

A diferencia de otras instrucciones `DROP` de SQL Server, esta instrucción admite la especificación de una cláusula AUTHORIZATION opcional. Esto permite a los **dbo** o a los usuarios con el rol **db_owner** quitar una biblioteca de paquetes cargada por un usuario normal en la base de datos.

## <a name="examples"></a>Ejemplos

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Agregue el paquete de R personalizado, `customPackage`, a una base de datos:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```
::: moniker-end

Elimine la biblioteca `customPackage`.

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>Consulte también

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
