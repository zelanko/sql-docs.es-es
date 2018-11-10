---
title: Tipos de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 9/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 71c0f046ad2f831cdff7136bd92059fd4a24bfce
ms.sourcegitcommit: b58d514879f182fac74d9819918188f1688889f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2018
ms.locfileid: "50970436"
---
# <a name="data-types-transact-sql"></a>Tipos de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

> [!div class="nextstepaction"]
> [Ayude a mejorar la documentación de SQL Server](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cada columna, variable local, expresión y parámetro tiene un tipo de datos relacionado. Un tipo de datos es un atributo que especifica el tipo de datos que el objeto puede contener: datos de enteros, datos de caracteres, datos de moneda, datos de fecha y hora, cadenas binarias, etc.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un conjunto de tipos de datos del sistema que define todos los tipos de datos que pueden utilizarse con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También puede definir sus propios tipos de datos en [!INCLUDE[tsql](../../includes/tsql-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Los tipos de datos de alias están basados en los tipos de datos proporcionados por el sistema. Para obtener más información acerca de los tipos de datos de alias, vea [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md). Los tipos definidos por el usuario obtienen sus características de los métodos y los operadores de una clase que se crean mediante uno de los lenguajes de programación compatibles con [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].
  
Cuando dos expresiones que tienen tipos de datos, intercalaciones, precisión, escala o longitud diferentes son combinadas por un operador, las características del resultado vienen determinadas por lo siguiente:
-   El tipo de datos del resultado viene determinado por la aplicación de las reglas de precedencia de tipos de datos a los tipos de datos de las expresiones de entrada. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
-   La intercalación del resultado viene determinada por las reglas de precedencia de intercalación cuando el tipo de datos del resultado es **char**, **varchar**, **text**, **nchar**, **nvarchar** o **ntext**. Para más información, vea [Prioridad de intercalación &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md).  
-   La precisión, escala y longitud del resultado dependen de la precisión, escala y longitud de las expresiones de entrada. Para más información, vea [Precisión, escala y longitud &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona sinónimos de tipos de datos para la compatibilidad con ISO. Para obtener más información, vea [Sinónimos de tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
## <a name="data-type-categories"></a>Categorías de tipos de datos
Los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se organizan en las siguientes categorías:
  
|||  
|-|-|  
|Numéricos exactos|Cadenas de caracteres Unicode|  
|Numéricos aproximados|Cadenas binarias|  
|Fecha y hora|Otros tipos de datos|  
|Cadenas de caracteres||  
  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], según las características de almacenamiento, algunos tipos de datos están designados como pertenecientes a los siguientes grupos:
-   Tipos de datos de valores grandes: **varchar(max)** y **nvarchar(max)**  
-   Tipos de datos de objetos grandes: **text**, **ntext**, **image**, **varbinary(max)** y **xml**  
  
    > [!NOTE]  
    >  sp_help devuelve -1 como longitud de los tipos de datos **xml** y de valores grandes.  
  
### <a name="exact-numerics"></a>Numéricos exactos
  
|||  
|-|-|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|[smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)||  
  
### <a name="approximate-numerics"></a>Numéricos aproximados
  
|||  
|-|-|  
|[float](../../t-sql/data-types/float-and-real-transact-sql.md)|[real](../../t-sql/data-types/float-and-real-transact-sql.md)|  
  
### <a name="date-and-time"></a>Fecha y hora
  
|||  
|-|-|  
|[date](../../t-sql/data-types/date-transact-sql.md)|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|[time](../../t-sql/data-types/time-transact-sql.md)|  
  
### <a name="character-strings"></a>Cadenas de caracteres
  
|||  
|-|-|  
|[char](../../t-sql/data-types/char-and-varchar-transact-sql.md)|[varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|[texto](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="unicode-character-strings"></a>Cadenas de caracteres Unicode
  
|||  
|-|-|  
|[nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|[nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
|[ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="binary-strings"></a>Cadenas binarias
  
|||  
|-|-|  
|[binario](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|[imagen](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="other-data-types"></a>Otros tipos de datos
  
|||  
|-|-|  
|[cursor](../../t-sql/data-types/cursor-transact-sql.md)|[rowversion](../../t-sql/data-types/rowversion-transact-sql.md)|  
|[hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)|  
|[sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)|[xml](../../t-sql/xml/xml-transact-sql.md)|  
|[Tipos de geometría espacial](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) |[Tipos de geografía espacial](../../t-sql/spatial-geography/spatial-types-geography.md)|  
|[table](../../t-sql/data-types/table-transact-sql.md) | |
  
## <a name="see-also"></a>Vea también
[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funciones &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  
