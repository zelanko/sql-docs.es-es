---
title: '@@DATEFIRST (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SET DATEFIRST
- first day of week [SQL Server]
- dates [SQL Server], first day of week
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- date and time [SQL Server], DATEFIRST
- DATEFIRST option [SQL Server]
- date and time [SQL Server], @@DATEFIRST
- weekdays [SQL Server]
- '@@DATEFIRST function [SQL Server]'
- functions [SQL Server], date and time
- options [SQL Server], date
ms.assetid: a178868e-49d5-4bd5-a5e2-1283409c8ce6
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 2dfe63f2d59cb3e3a1b563d524693af0d3dd1b51
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40datefirst-transact-sql"></a>&#x40;&#x40; DATEFIRST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el valor actual, para una sesión de [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
Para obtener información general de todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora y funciones, vea [funciones y tipos de datos de hora y fecha &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```
@@DATEFIRST  
```  
  
## <a name="return-type"></a>Tipo devuelto  
**tinyint**
  
## <a name="remarks"></a>Comentarios  
SET DATEFIRST especifica el primer día de la semana. El valor predeterminado para inglés inglés de EE.UU. es 7, domingo.
  
Esta configuración de idioma afecta a la interpretación de cadenas de caracteres cuando se convierten en valores de fecha para el almacenamiento en la base de datos y la presentación de los valores de fecha que se almacenan en la base de datos. Esta configuración no afecta al formato de almacenamiento de datos de fecha. En el siguiente ejemplo, el idioma se establece primero en `Italian`. La instrucción `SELECT @@DATEFIRST;` devuelve `1`. A continuación, el idioma se establece en `us_english`. La instrucción `SELECT @@DATEFIRST;` devuelve `7`.
  
```sql
SET LANGUAGE Italian;  
GO  
SELECT @@DATEFIRST;  
GO  
SET LANGUAGE us_english;  
GO  
SELECT @@DATEFIRST;  
```  
  
## <a name="examples"></a>Ejemplos  
En el siguiente ejemplo se establece como primer día de la semana el `5` (viernes) y se supone que el día actual, `Today`, es sábado. La instrucción `SELECT` devuelve el valor de `DATEFIRST` y el número del día actual de la semana.
  
```sql
SET DATEFIRST 5;  
SELECT @@DATEFIRST AS 'First Day'  
    ,DATEPART(dw, SYSDATETIME()) AS 'Today';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
First Day         Today  
----------------  --------------  
5                 2  
```  
  
## <a name="example"></a>Ejemplo
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>Vea también
[Funciones de configuración &#40; Transact-SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  


