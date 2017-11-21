---
title: SWITCHOFFSET (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 12/02/2015
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
- SWITCHTZ
- SWITCHTZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- functions [SQL Server], time
- functions [SQL Server], date and time
- SWITCHOFFSET function [SQL Server]
- time [SQL Server], functions
- date and time [SQL Server], SWITCHOFFSET
- time zones [SQL Server]
ms.assetid: 32a48e36-0aa4-4260-9fe9-cae9197d16c5
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 3c81153c233e68d12347dc47ae9c232f4a5ee030
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un **datetimeoffset** valor que se cambia desde el desplazamiento de zona horaria almacenado a un nuevo ajuste de zona horaria especificada.  
  
 Para obtener información general de todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora y funciones, vea [funciones y tipos de datos de hora y fecha &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
## <a name="arguments"></a>Argumentos  
 *DATETIMEOFFSET*  
 Es una expresión que se pueda resolver como un **DateTimeOffset (n)** valor.  
  
 *zona horaria*  
 Es una cadena de caracteres en formato [+|-]TZH:TZM o un entero con signo (de minutos) que representa el ajuste de zona horaria y se supone que reconoce y está ajustado para el horario de verano.  
  
## <a name="return-type"></a>Tipo devuelto  
 **DateTimeOffset** con la precisión fraccionaria de los *DATETIMEOFFSET* argumento.  
  
## <a name="remarks"></a>Comentarios  
 Use SWITCHOFFSET para seleccionar un **datetimeoffset** valor en un desplazamiento de zona horaria es diferente del desplazamiento de zona horaria que se almacenó originalmente. SWITCHOFFSET no actualiza la suma de comprobación *valor time_zone* valor.  
  
 SWITCHOFFSET se puede usar para actualizar una **datetimeoffset** columna.  
  
 Si se usa SWITCHOFFSET con la función GETDATE(), es posible que la consulta se ejecute lentamente. Esto se debe a que el optimizador de consultas no puede obtener estimaciones de cardinalidad precisas para el valor datetime. Para resolver este problema, use la sugerencia de consulta OPTION (RECOMPILE) para obligar al optimizador de consultas a que vuelva a compilar un plan de consulta la próxima vez que se ejecute la misma consulta. De este modo, el optimizador tendrá estimaciones de cardinalidad precisas y generará un plan de consulta más eficaz. Para obtener más información acerca de la sugerencia de consulta RECOMPILE, vea [sugerencias de consulta &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-query.md).  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `SWITCHOFFSET` para mostrar un ajuste de zona horaria diferente del valor almacenado en la base de datos.  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="see-also"></a>Vea también  
 [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [EN la zona HORARIA &#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  



