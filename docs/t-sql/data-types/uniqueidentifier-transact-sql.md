---
title: uniqueidentifier (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- uniqueidentifier
- uniqueidentifier_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- globally unique identifiers [SQL Server]
- GUIDs [SQL Server]
ms.assetid: b026035b-f3d2-4d70-989d-3884b4ca0233
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 1450aa86e3f47ef27be5acd5b5410fe40dd5983e
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

Es un GUID de 16 bytes.
  
## <a name="remarks"></a>Comentarios  
Una columna o una variable local de **uniqueidentifier** tipo de datos se puede inicializar en un valor de las maneras siguientes:
-   Mediante la función NEWID.  
-   Mediante la conversión de una constante de cadena con el formato *xxxxxxxx*-*xxxx*-*xxxx*-*xxxx* - *xxxxxxxxxxxx*, donde cada *x* es un dígito hexadecimal en el intervalo 0-9 o a-f. Por ejemplo, 6F9619FF-8B86-D011-B42D-00C04FC964FF es válido **uniqueidentifier** valor.  
  
Operadores de comparación se pueden utilizar con **uniqueidentifier** valores. No obstante, no se implementa la ordenación mediante la comparación de los patrones de bits de los dos valores. Las únicas operaciones que se pueden realizar con un **uniqueidentifier** valor son comparaciones (=, <>, \<, >, \<=, > =) y la comprobación de NULL (IS NULL e IS NOT NULL). No es posible utilizar otros operadores aritméticos. Todas las restricciones de columna y propiedades, excepto IDENTITY, se pueden usar en el **uniqueidentifier** tipo de datos.
  
Replicación de mezcla y replicación transaccional con suscripciones de actualización usan **uniqueidentifier** columnas para garantizar que filas se identifican de forma única en varias copias de la tabla.
  
## <a name="converting-uniqueidentifier-data"></a>Convertir datos uniqueidentifier  
El **uniqueidentifier** tipo se considera un tipo de carácter para los fines de conversión de una expresión de caracteres y, por tanto, está sujeto a las reglas de truncamiento para convertir a un tipo de carácter. Es decir, cuando se convierten expresiones de carácter a un tipo de datos de carácter de un tamaño distinto, se truncan los valores que son demasiado grandes para el nuevo tipo de datos. Vea la sección Ejemplos.
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones

Estas herramientas y características no son compatibles con el `uniqueidentifier` tipo de datos:
- PolyBase
- [herramienta de carga de dwloader](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader) para almacenamiento de datos paralelos

## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se convierte un valor `uniqueidentifier` a un tipo de datos `char`.
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
En el ejemplo siguiente se muestra el truncamiento de los datos cuando el valor es demasiado largo para el tipo de datos al que se va a convertir. Dado que la **uniqueidentifier** tipo está limitado a 36 caracteres, se truncan los caracteres que superan esa longitud.
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[NEWID &#40; Transact-SQL &#41;](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID &#40; Transact-SQL &#41; ](../../t-sql/functions/newsequentialid-transact-sql.md) 
 [Establecer @local_variable &#40; Transact-SQL &#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  

