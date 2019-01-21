---
title: TODATETIMEOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4d2234f6f8d9fa54ccbbae35e1e1dfc7568cc8ff
ms.sourcegitcommit: 1f53b6a536ccffd701fc87e658ddac714f6da7a2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2019
ms.locfileid: "54206231"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un valor de tipo **datetimeoffset** que se traduce a partir de una expresión **datetime2**.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que se resuelve en un valor de tipo [datetime2](../../t-sql/data-types/datetime2-transact-sql.md).  
  
> [!NOTE]  
>  La expresión no puede ser del tipo **text**, **ntext** o **image**, ya que estos tipos no se pueden convertir implícitamente en **varchar** o **nvarchar**.  
  
 *time_zone*  
 Es una expresión que representa el desplazamiento de zona horaria en minutos (si es un entero), por ejemplo -120, o las horas y los minutos (si es una cadena), como "+13:00". El intervalo es de +14 a -14 (en horas). La expresión se interpreta en la hora local para el valor time_zone especificado.  
  
> [!NOTE]  
>  Si la expresión es una cadena de caracteres, debe tener el formato {+|-}TZH:THM.  
  
## <a name="return-type"></a>Tipo devuelto  
 **datetimeoffset**. La precisión fraccionaria es la misma que la del argumento *datetime*.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. Cambiar el ajuste de zona horaria de la fecha y hora actuales  
 En el ejemplo siguiente se cambia el ajuste de zona horaria de la fecha y hora actuales a la zona horaria `-07:00`.  
  
```  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2007-08-30 15:51:34.7030000 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>b. Cambiar el ajuste de zona horaria en minutos  
 En el ejemplo siguiente se cambia la zona horaria actual a `-120` minutos.  
  
```  
DECLARE @todaysDate datetime2;  
SET @todaysDate = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDate, -120);  
-- RETURNS 2007-08-30 15:52:37.8770000 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. Agregar un ajuste de zona horaria de 13 horas  
 En el ejemplo siguiente se agrega un ajuste de zona horaria de 13 horas a una fecha y hora.  
  
```  
DECLARE @dateTime datetimeoffset(7)= '2007-08-28 18:00:30';  
SELECT TODATETIMEOFFSET (@dateTime, '+13:00');  
-- RETURNS 2007-08-28 18:00:30.0000000 +13:00  
```  
  
## <a name="see-also"></a>Consulte también  
 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  

