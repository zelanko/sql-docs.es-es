---
description: 'DROP EXTERNAL LANGUAGE (Transact-SQL): SQL Server'
title: DROP EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2019
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d159d4b61e9fa8a171873d7c1a8f6466452e8fe9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88358461"
---
# <a name="drop-external-language-transact-sql"></a>DROP EXTERNAL LANGUAGE (Transact-SQL)  
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Elimina un lenguaje externo existente.

## <a name="syntax"></a>Sintaxis

```text
DROP EXTERNAL LANGUAGE <language_name>
```

### <a name="arguments"></a>Argumentos

**language_name**

Los lenguajes son objetos del ámbito de la base de datos. Los nombres del lenguaje deben ser únicos en la base de datos.

## <a name="permissions"></a>Permisos

Para eliminar un lenguaje necesita el privilegio ALTER ANY EXTERNAL LANGUAGE. De forma predeterminada, cualquier propietario de base de datos o el propietario del objeto también puede eliminar un lenguaje externo.

> [!NOTE]
> Tenga en cuenta que antes de quitar un lenguaje externo, deberá quitar las bibliotecas externas que hacen referencia a dicho lenguaje.

### <a name="return-values"></a>Valores devueltos

Si la instrucción se ejecuta correctamente, se devuelve un mensaje informativo.

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Observaciones

Para poder eliminar un lenguaje externo, primero es necesario eliminar todas las bibliotecas externas relacionadas con dicho lenguaje.

## <a name="examples"></a>Ejemplos

Crear un lenguaje externo **Java**:

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

Quitar el lenguaje externo:

```sql
DROP EXTERNAL LANGUAGE Java;
```

## <a name="see-also"></a>Consulte también

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
