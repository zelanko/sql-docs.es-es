---
title: DROP EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 29bb832fc1123b5261088b52232b693ca1c10138
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994943"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

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

## <a name="remarks"></a>Notas

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

## <a name="see-also"></a>Vea también

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
