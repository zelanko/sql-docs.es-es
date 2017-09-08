---
title: "_ (Comodín - coincidir un carácter) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e47fdb9e12a632323971558d2e894fb7b181498e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (comodín, coincidir un carácter) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Utilice el carácter de subrayado `_` para que coincida con cualquier carácter individual en una operación de comparación de cadenas que implica la coincidencia de patrones, como `LIKE` y `PATINDEX`.  
  
## <a name="examples"></a>Ejemplos  

## <a name="a-simple-example"></a>R: ejemplo sencillo de   

El ejemplo siguiente devuelve todos los nombres que comienzan por la letra de la base de datos `m` y tener la letra `d` como la tercera letra. El carácter de subrayado especifica que el segundo carácter del nombre puede ser cualquier letra. El `model` y `msdb` las bases de datos cumplan este criterio. El `master` base de datos no lo hace.

```tsql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
Puede tener bases de datos adicionales que cumplan este criterio.

Puede usar varios caracteres de subrayado para representar varios caracteres. Cambiar el `LIKE` criterios para incluir dos caracteres de subrayado `'m__%` incluye la base de datos maestra en el resultado.

### <a name="b-more-complex-example"></a>B: ejemplo más complejo
 En el siguiente ejemplo se utiliza el operador `_` para buscar todas las personas de la tabla `Person` con un nombre de tres letras que termina en `an`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: escape el carácter de subrayado   
El ejemplo siguiente devuelve los nombres de los roles fijos de base de datos como `db_owner` y `db_ddladmin`, pero también devuelve la `dbo` usuario. 

```tsql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

El carácter de subrayado en la tercera posición de carácter se toma como un carácter comodín y no se filtran solo las entidades a partir de las letras `db_`. Como escape el carácter de subrayado entre corchetes `[_]`. 

```tsql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
Ahora el `dbo` se excluye el usuario.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>Vea también  
 [COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (Caracteres comodín para coincidir)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (Comodín - caracteres para coincidir)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; (Comodín - caracteres no coincidentes)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
  

