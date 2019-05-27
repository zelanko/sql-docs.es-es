---
title: DATETIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIMEFROMPARTS_TSQL
- DATETIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEFROMPARTS function
ms.assetid: 6008148b-bf75-4c98-9392-68a89fa0711c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 505b1ac04eae49c58a4166fcceba8ec9bf53a66a
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945727"
---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Esta función devuelve un valor **datetime** para los argumentos de fecha y hora especificados.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
```  
  
## <a name="arguments"></a>Argumentos  
*year*  
Expresión entera que especifica un año.
  
*month*  
Expresión entera que especifica un mes.
  
*day*  
Expresión entera que especifica un día.
  
*hour*  
Expresión entera que especifica las horas.
  
*minute*  
Expresión entera que especifica los minutos.
  
*segundos*  
Expresión entera que especifica los segundos.
  
*milliseconds*  
Expresión entera que especifica los milisegundos.
  
## <a name="return-types"></a>Tipos de valores devueltos
**datetime**
  
## <a name="remarks"></a>Notas  
`DATETIMEFROMPARTS` devuelve un valor **datetime** totalmente inicializado. `DATETIMEFROMPARTS` producirá un error si al menos uno de los argumentos obligatorios tiene un valor no válido. `DATETIMEFROMPARTS` devuelve NULL si al menos uno de los argumentos obligatorios tiene un valor NULL.
  
Esta función admite la conexión remota a servidores de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y versiones posteriores. No admitirá la conexión remota a servidores que tengan una versión inferior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Ejemplos  
  
```sql
SELECT DATETIMEFROMPARTS ( 2010, 12, 31, 23, 59, 59, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)
  
  

