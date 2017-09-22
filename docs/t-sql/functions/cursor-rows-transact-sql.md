---
title: '@@CURSOR_ROWS (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CURSOR_ROWS'
- '@@CURSOR_ROWS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CURSOR_ROWS function'
- cursors [SQL Server], last-opened
- last-opened cursor
- asynchronous cursors [SQL Server]
ms.assetid: 31bd7a97-7f28-42a8-ba24-24d16d22973d
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 10a3a6cabae8d25de670cbacb037a62f4c5a2d54
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40cursorrows-transact-sql"></a>& #x 40; & #x 40; @Cursor_rows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el número de filas certificadas que se encuentran en el último cursor abierto en la conexión. Para mejorar el rendimiento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede rellenar asincrónicamente los cursores estáticos y de conjunto de claves de gran tamaño. @@CURSOR_ROWS se puede llamar para determinar que el número de filas que se incluyen en un cursor se recupera en el momento @@CURSOR_ROWS se llama.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```
@@CURSOR_ROWS  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto
**integer**
  
## <a name="return-value"></a>Valor devuelto  
  
|Valor devuelto|Description|  
|---|---|
|-*m*|El cursor se rellena de forma asincrónica. El valor devuelto (-*m*) es el número de filas actualmente en el conjunto de claves.|  
|-1|El cursor es dinámico. Como los cursores dinámicos reflejan todos los cambios, el número de filas correspondientes al cursor cambia constantemente. Nunca se puede afirmar que se han recuperado todas las filas que correspondan.|  
|0|No se han abierto cursores, no hay filas calificadas para el último cursor abierto, o éste se ha cerrado o su asignación se ha cancelado.|  
|*n*|El cursor está completamente relleno. El valor devuelto (*n*) es el número total de filas del cursor.|  
  
## <a name="remarks"></a>Comentarios  
El número devuelto por@CURSOR_ROWS es negativo si el último cursor se abrió de forma asincrónica. Controlador de conjunto de claves o cursores estáticos se abren de forma asincrónica si el valor de sp_configure cursor threshold es mayor que 0 y el número de filas en el conjunto de resultados del cursor es mayor que el umbral de cursor.
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente declara un cursor y utiliza `SELECT` para mostrar el valor de `@@CURSOR_ROWS`. La opción tiene el valor `0` antes de abrir el cursor y el valor `-1` para indicar que el conjunto de claves del cursor se está rellenando de forma asincrónica.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@CURSOR_ROWS;  
DECLARE Name_Cursor CURSOR FOR  
SELECT LastName ,@@CURSOR_ROWS FROM Person.Person;  
OPEN Name_Cursor;  
FETCH NEXT FROM Name_Cursor;  
SELECT @@CURSOR_ROWS;  
CLOSE Name_Cursor;  
DEALLOCATE Name_Cursor;  
GO             
```  
  
Los conjuntos de resultados son los siguientes.
  
`-----------`
  
 `0`  
  
`LastName`
  
`---------------`
  
`Sanchez`
  
`-----------`
  
 `-1`  
  
## <a name="see-also"></a>Vea también
[Funciones de cursor &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[Abrir &#40; Transact-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  

