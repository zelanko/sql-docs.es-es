---
title: COL_LENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COL_LENGTH
- COL_LENGTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lengths [SQL Server], columns
- COL_LENGTH function
- column properties [SQL Server]
- column length [SQL Server]
ms.assetid: cf891206-c49f-40eb-858e-eefd2b638a33
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bf23672374db7d8348154e95ca6228723934aa5a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68064729"
---
# <a name="col_length-transact-sql"></a>COL_LENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esta función devuelve la longitud definida de una columna, en bytes.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COL_LENGTH ( 'table' , 'column' )   
```  
  
## <a name="arguments"></a>Argumentos  
**'** *table* **'**  
El nombre de la tabla para la que se quiere determinar la información de longitud de columna. *table* es una expresión de tipo **nvarchar**.
  
**'** *column* **'**  
El nombre de la columna cuya longitud se quiere determinar. *column* es una expresión de tipo **nvarchar**.
  
## <a name="return-type"></a>Tipo de valor devuelto
**smallint**
  
## <a name="exceptions"></a>Excepciones  
Devuelve NULL si se produce un error o si el autor de la llamada no tiene el permiso correcto para ver el objeto.
  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un usuario solo puede ver los metadatos de los elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos como COL_LENGTH es posible que devuelvan NULL, si el usuario no tiene el permiso correcto para el objeto. Vea [Configuración de visibilidad de los metadatos](../../relational-databases/security/metadata-visibility-configuration.md) para obtener más información.
  
## <a name="remarks"></a>Observaciones  
Para las columnas de tipo **varchar** declaradas con el especificador **max** (**varchar(max)** ), COL_LENGTH devuelve el valor -1.
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se muestran los valores devueltos para una columna de tipo `varchar(40)` y una columna de tipo `nvarchar(40)`:
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE t1(c1 varchar(40), c2 nvarchar(40) );  
GO  
SELECT COL_LENGTH('t1','c1')AS 'VarChar',  
      COL_LENGTH('t1','c2')AS 'NVarChar';  
GO  
DROP TABLE t1;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
VarChar     NVarChar  
40          80  
```  
  
## <a name="see-also"></a>Consulte también
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)
  
  
