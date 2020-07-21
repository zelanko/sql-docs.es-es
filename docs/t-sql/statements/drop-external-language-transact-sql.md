---
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
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6f4b6ee38ed70da600ef007f168cd7e95a010278
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85766366"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

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
