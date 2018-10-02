---
title: Sinónimos de tipos de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
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
manager: craigg
ms.openlocfilehash: 482177b87fb4d62cbebb64361e0b26ed9a681c1f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816563"
---
# <a name="data-type-synonyms-transact-sql"></a>Sinónimos de tipos de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Los sinónimos de tipos de datos se incluyen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por compatibilidad con ISO. En la siguiente tabla se incluyen los sinónimos y los tipos de datos de sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a los que se asignan.
  
|Synonym (Sinónimo)|Tipo de datos de sistema de SQL Server|  
|---|---|
|**Variable binaria**|**varbinary**|  
|**char varying**|**varchar**|  
|**carácter**|**char**|  
|**carácter**|**char(1)**|  
|**character(** *n* **)**|**char(n)**|  
|**character varying(** *n* **)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Doble precisión**|**float**|  
|**float**[**(***n***)**] for *n* = 1-7|**real**|  
|**float**[**(***n***)**] for *n* = 8-15|**float**|  
|**integer**|**int**|  
|**carácter nacional (** *n* **)**|**nchar(n)**|  
|**carácter nacional (** *n* **)**|**nchar(n)**|  
|**national character varying(** *n* **)**|**nvarchar(n)**|  
|**national char varying(** *n* **)**|**nvarchar(n)**|  
|**texto nacional**|**ntext**|  
|**timestamp**|rowversion|  
  
Los sinónimos de tipos de datos pueden utilizarse en lugar del nombre del tipo de datos base correspondiente en las instrucciones del lenguaje de definición de datos (DDL), como CREATE TABLE, CREATE PROCEDURE o DECLARE *@variable*. Sin embargo, los sinónimos no tienen visibilidad después de crear el objeto. Una vez creado el objeto, se le asigna el tipo de datos base asociado al sinónimo. No hay ningún registro de que el sinónimo se haya especificado en la instrucción que ha creado el objeto.
  
A todos los objetos que proceden del objeto original, como las columnas del conjunto de resultados o las expresiones, se les asigna el tipo de datos base. Todas las funciones de metadatos subsiguientes ejecutadas en el objeto original y cualquier objeto derivado informarán del tipo de datos base y no del sinónimo. Este comportamiento se produce con las operaciones de metadatos como **sp_help** y otros procedimientos almacenados del sistema, las vistas del esquema de información o las diferentes operaciones de metadatos de la API de acceso a datos que informan de los tipos de datos de las columnas de tablas o conjuntos de resultados.
  
Por ejemplo, puede crear una tabla si especifica `national character varying`:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol` se asigna a un tipo de datos **nvarchar(10)** y todas las funciones de metadatos posteriores informan de la columna como columna **nvarchar(10)**. Las funciones de metadatos nunca informarán de ellos como columna **variable de carácter nacional (10)**.
  
## <a name="see-also"></a>Vea también
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
