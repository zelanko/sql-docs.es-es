---
title: "Tipo de datos sinónimos (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1d9b1da2bdc7084268740cd7de2580e64ee9698b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-synonyms-transact-sql"></a>Sinónimos de tipos de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Los sinónimos de tipos de datos se incluyen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por compatibilidad con ISO. En la siguiente tabla se incluyen los sinónimos y los tipos de datos de sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a los que se asignan.
  
|Synonym (Sinónimo)|Tipo de datos de sistema de SQL Server|  
|---|---|
|**Variable binario**|**varbinary**|  
|**carácter variable**|**varchar**|  
|**carácter**|**char**|  
|**carácter**|**Char (1)**|  
|**carácter (**  *n*  **)**|**char(n)**|  
|**carácter variable (**  *n*  **)**|**varchar(n)**|  
|**Diciembre**|**decimal**|  
|**Precisión doble**|**float**|  
|**float**[**(***n***)**] para  *n*  = 1-7|**real**|  
|**float**[**(***n***)**] para  *n*  = 8-15|**float**|  
|**integer**|**int**|  
|**caracteres no nacionales (**  *n*  **)**|**nchar (n)**|  
|**National char (**  *n*  **)**|**nchar (n)**|  
|**national character varying de (**  *n*  **)**|**nvarchar (n)**|  
|**variación Car (**  *n*  **)**|**nvarchar (n)**|  
|**texto nacional**|**ntext**|  
|**timestamp**|rowversion|  
  
Sinónimos de tipos de datos puede utilizarse en lugar del nombre de tipo de datos base correspondiente en instrucciones de DDL (lenguaje) de definición de datos, como CREATE TABLE, CREATE PROCEDURE o DECLARE  *@variable* . Sin embargo, los sinónimos no tienen visibilidad después de crear el objeto. Una vez creado el objeto, se le asigna el tipo de datos base asociado al sinónimo. No hay ningún registro de que el sinónimo se haya especificado en la instrucción que ha creado el objeto.
  
A todos los objetos que proceden del objeto original, como las columnas del conjunto de resultados o las expresiones, se les asigna el tipo de datos base. Todas las funciones de metadatos subsiguientes ejecutadas en el objeto original y cualquier objeto derivado informarán del tipo de datos base y no del sinónimo. Este comportamiento se produce con las operaciones de metadatos como **sp_help** y otro sistema de procedimientos almacenados, las vistas de esquema de información o las distintas operaciones de metadatos de API de acceso a datos que dependen de los tipos de datos de tabla o conjunto de resultados columnas.
  
Por ejemplo, puede crear una tabla si especifica `national character varying`:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol`se asigna un **nvarchar (10)** tipo de datos, y todas las funciones de metadatos posteriores informan de la columna como un **nvarchar (10)** columna. Las funciones de metadatos nunca informarán de ellos como una **varying (10) de caracteres nacionales** columna.
  
## <a name="see-also"></a>Vea también
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

