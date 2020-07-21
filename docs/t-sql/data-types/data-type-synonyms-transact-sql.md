---
title: Sinónimos de tipos de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a9e988529cc5a59786504be8566e55a4449a5ee6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732859"
---
# <a name="data-type-synonyms-transact-sql"></a>Sinónimos de tipos de datos (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Los sinónimos de tipos de datos se incluyen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por compatibilidad con ISO. En la siguiente tabla se incluyen los sinónimos y los tipos de datos de sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a los que se asignan.
  
|Synonym (Sinónimo)|Tipo de datos de sistema de SQL Server|  
|---|---|
|**Variable binaria**|**varbinary**|  
|**char varying**|**varchar**|  
|**carácter**|**char**|  
|**carácter**|**char(1)**|  
|**character(** _n_ **)**|**char(n)**|  
|**character varying(** _n_ **)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Doble precisión**|**float**|  
|**float**[ **(** _n_ **)** ] para _n_ = 1-7|**real**|  
|**float**[ **(** _n_ **)** ] para _n_ = 8-15|**float**|  
|**integer**|**int**|  
|**national character(** _n_ **)**|**nchar(n)**|  
|**national char(** _n_ **)**|**nchar(n)**|  
|**national character varying(** _n_ **)**|**nvarchar(n)**|  
|**national char varying(** _n_ **)**|**nvarchar(n)**|  
|**texto nacional**|**ntext**|  
|**timestamp**|rowversion|  
  
Los sinónimos de tipos de datos pueden utilizarse en lugar del nombre del tipo de datos base correspondiente en las instrucciones del lenguaje de definición de datos (DDL), Estas instrucciones incluyen los valores *\@variable* CREATE TABLE, CREATE PROCEDURE y DECLARE. Sin embargo, los sinónimos no tienen visibilidad después de crear el objeto. Una vez creado el objeto, se le asigna el tipo de datos base asociado al sinónimo. No hay ningún registro de que el sinónimo se haya especificado en la instrucción que ha creado el objeto.
  
A todos los objetos que proceden del objeto original, como las columnas del conjunto de resultados o las expresiones, se les asigna el tipo de datos base. Todas las funciones de metadatos ejecutadas en el objeto original y cualquier objeto derivado informarán del tipo de datos base y no del sinónimo.

* Por ejemplo, operaciones de metadatos como **sp_help** y otros procedimientos almacenados en el sistema,
* vistas de esquema de información y
* operaciones de metadatos de API de acceso a datos que informan de los tipos de datos de columnas de conjunto de resultados o tablas.
  
Por ejemplo, puede crear una tabla si especifica `national character varying`:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol` se asigna a un tipo de datos **nvarchar(10)** y todas las funciones de metadatos posteriores informan de la columna como columna **nvarchar(10)** . Las funciones de metadatos nunca informarán de ellos como columna **variable de carácter nacional (10)** .
  
## <a name="see-also"></a>Consulte también
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
