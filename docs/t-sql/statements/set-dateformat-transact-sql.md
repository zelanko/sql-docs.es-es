---
title: SET DATEFORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEFORMAT
- SET DATEFORMAT
- SET_DATEFORMAT_TSQL
- DATEFORMAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], formats
- dates [SQL Server], ordering date parts
- SET DATEFORMAT option [SQL Server]
- DATEFORMAT option [SQL Server]
- date and time [SQL Server], SET DATEFORMAT
- options [SQL Server], date
- date and time [SQL Server], DATEFORMAT
- dateparts [SQL Server], dateformat
ms.assetid: da217878-7ec4-477e-aa13-604073c948f8
caps.latest.revision: 49
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 7d0114bb98134b86b92bae634f2746abce163279
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456649"
---
# <a name="set-dateformat-transact-sql"></a>SET DATEFORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Establece el orden de las partes correspondientes al mes, día y año de una fecha para interpretar las cadenas de caracteres **date**, **smalldatetime**, **datetime**, **datetime2** y **datetimeoffset**.  
  
 Para ver información general sobre todos los tipos de datos y funciones de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], vea [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SET DATEFORMAT { format | @format_var }   
```  
  
## <a name="arguments"></a>Argumentos  
 *format* | **@***format_var*  
 Es el orden de las partes de la fecha. Los parámetros válidos son **mdy**, **dmy**, **ymd**, **ydm**, **myd** y **dym**. Puede ser Unicode o juegos de caracteres de doble byte (DBCS) convertidos a Unicode. El valor predeterminado para inglés de EE. UU. es **mdy**. Para más información sobre el DATEFORMAT predeterminado de todos los lenguajes admitidos, vea [sp_helplanguage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md).  
  
## <a name="remarks"></a>Notas  
 El DATEFORMAT **ydm** no se admite en los tipos de datos **date**, **datetime2** y **datetimeoffset**.  
  
 El efecto de la configuración DATEFORMAT en la interpretación de cadenas de caracteres puede ser distinto para los valores **datetime** y **smalldatetime** y para los valores **date**, **datetime2** y **datetimeoffset**, dependiendo del formato de cadena. Esta configuración de idioma afecta a la interpretación de cadenas de caracteres cuando se convierten en valores de fecha para el almacenamiento en la base de datos. No afecta a la presentación de valores de tipo de datos de fecha que se almacenan en el formato de base de datos o de almacenamiento.  
  
 Algunos formatos de cadenas de caracteres, por ejemplo ISO 8601, se interpretan independientemente del valor DATEFORMAT.  
  
 La opción SET DATEFORMAT se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 SET DATEFORMAT anula la configuración de formato de fecha implícita de [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente utiliza cadenas de fecha diferentes como entradas en sesiones con el mismo valor `DATEFORMAT`.  
  
```  
-- Set date format to day/month/year.  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar datetime2 = '31/12/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: 2008-12-31 09:01:01.123  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar datetime2 = '12/31/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: Msg 241: Conversion failed when converting date and/or time -- from character string.  
  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

