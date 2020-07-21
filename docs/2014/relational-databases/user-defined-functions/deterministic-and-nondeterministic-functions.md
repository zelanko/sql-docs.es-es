---
title: Funciones deterministas y no deterministas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- built-in functions [SQL Server]
- nondeterministic functions
- extended stored procedures [SQL Server], functions that call
- deterministic functions
- user-defined functions [SQL Server], deterministic
ms.assetid: 2f3ce5f5-c81c-4470-8141-8144d4f218dd
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e755532e06d64e273408c7e81936a1c2d370697
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066405"
---
# <a name="deterministic-and-nondeterministic-functions"></a>Funciones deterministas y no deterministas
  Las funciones deterministas devuelven siempre el mismo resultado cada vez que se invocan con un conjunto específico de valores de entrada y cuando el estado de la base de datos es el mismo. Las funciones no deterministas pueden devolver resultados diferentes cada vez que se llaman con un conjunto específico de valores de entrada aunque el estado de la base de datos a la que tienen acceso permanezca sin cambios. Por ejemplo, la función AVG siempre devuelve el mismo resultado dadas las condiciones indicadas anteriormente pero la función GETDATE, que devuelve el valor datetime actual, siempre devuelve un resultado diferente.  
  
 Son varias las propiedades de las funciones definidas por el usuario que determinan la capacidad de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para indizar los resultados de la función, ya sea mediante índices en columnas calculadas que llaman a la función o mediante vistas indizadas que hacen referencia a la función. El determinismo de una función es una propiedad así. Por ejemplo, no se puede crear un índice clúster en una vista si ésta hace referencia a funciones no deterministas. Para obtener más información sobre las propiedades de las funciones, incluido el determinismo, vea [Funciones definidas por el usuario](user-defined-functions.md).  
  
 En este tema se identifica el determinismo de las funciones integradas del sistema y el efecto de las funciones definidas por el usuario en la propiedad determinista cuando ésta contiene una llamada a los procedimientos almacenados extendidos.  
  
## <a name="built-in-function-determinism"></a>Determinismo de las funciones integradas  
 El determinismo de las funciones integradas no se ve afectado por el usuario. Las funciones integradas son deterministas o no deterministas según el modo en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]implementa cada función. Por ejemplo, al especificar una cláusula ORDER BY en una consulta, no se cambia el determinismo de una función que se usa en la consulta.  
  
 Todas las funciones integradas de cadena son deterministas. Para obtener una lista de estas funciones, vea [Funciones de cadena &#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql).  
  
 Las siguientes funciones integradas procedentes de categorías de funciones integradas que no son de cadena siempre son deterministas.  
  
||||  
|-|-|-|  
|ABS|DATEDIFF|POWER|  
|ACOS|DAY|RADIANS|  
|ASIN|DEGREES|ROUND|  
|ATAN|EXP|SIGN|  
|ATN2|FLOOR|SIN|  
|CEILING|ISNULL|SQUARE|  
|COALESCE|ISNUMERIC|SQRT|  
|COS|REGISTRO|TAN|  
|COT|LOG10|YEAR|  
|DATALENGTH|MONTH||  
|DATEADD|NULLIF||  
  
 Las siguientes funciones no siempre son deterministas, pero pueden utilizarse en vistas indizadas o en índices de columnas calculadas si se especifican de una manera determinista.  
  
|Función|Comentarios|  
|--------------|--------------|  
|todas las funciones de agregado|Todas las funciones de agregado son deterministas a menos que se especifiquen con las cláusulas OVER y ORDER BY. Para obtener una lista de estas funciones, vea [Funciones de agregado &#40;Transact-SQL&#41;](/sql/t-sql/functions/aggregate-functions-transact-sql).|  
|CAST|Determinista, a menos que se utilice con `datetime`, `smalldatetime` o `sql_variant`.|  
|CONVERT|Determinista, a menos que se cumpla una de estas condiciones:<br /><br /> El tipo de origen es `sql_variant`.<br /><br /> El tipo de destino es `sql_variant` y el tipo de origen no es determinista.<br /><br /> El tipo de origen o destino es `datetime` o `smalldatetime`, el otro tipo de origen o destino es una cadena de caracteres, y se especifica un tipo de estilo no determinista. Para que sea determinista, el parámetro de estilo debe ser una constante. Además, los estilos menores o iguales que 100 son no deterministas, salvo los estilos 20 y 21. Los estilos mayores que 100 son deterministas, salvo los estilos 106, 107, 109 y 113.|  
|CHECKSUM|Determinista, excepto CHECKSUM(*).|  
|ISDATE|Determinista solo si se utiliza con la función CONVERT, se especifica el parámetro de estilo CONVERT y el estilo no es igual a 0, 100, 9 ni 109.|  
|RAND|RAND es determinista solo cuando se especifica un parámetro *seed* .|  
  
 Todas las funciones de configuración, cursores, metadatos, seguridad y estadísticas del sistema no son deterministas. Para obtener una lista de estas funciones, vea [Funciones de configuración &#40;Transact-SQL&#41;](/sql/t-sql/functions/configuration-functions-transact-sql), [Funciones de cursor &#40;Transact-SQL&#41;](/sql/t-sql/functions/cursor-functions-transact-sql), [Funciones de metadatos &#40;Transact-SQL&#41;](/sql/t-sql/functions/metadata-functions-transact-sql), [Funciones de seguridad &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql) y [Funciones estadísticas del sistema &#40;Transact-SQL&#41;](/sql/t-sql/functions/system-statistical-functions-transact-sql).  
  
 Las siguientes funciones integradas, procedentes de otras categorías, no son deterministas nunca.  
  
|||  
|-|-|  
|@@CONNECTIONS|GETDATE|  
|@@CPU_BUSY|GETUTCDATE|  
|@@DBTS|GET_TRANSMISSION_STATUS|  
|@@IDLE|LAG|  
|@@IO_BUSY|LAST_VALUE|  
|@@MAX_CONNECTIONS|LEAD|  
|@@PACK_RECEIVED|MIN_ACTIVE_ROWVERSION|  
|@@PACK_SENT|NEWID|  
|@@PACKET_ERRORS|NEWSEQUENTIALID|  
|@@TIMETICKS|NEXT VALUE FOR|  
|@@TOTAL_ERRORS|NTILE|  
|@@TOTAL_READ|PARSENAME|  
|@@TOTAL_WRITE|PERCENTILE_CONT|  
|CUME_DIST|PERCENTILE_DISC|  
|CURRENT_TIMESTAMP|PERCENT_RANK|  
|DENSE_RANK|RAND|  
|FIRST_VALUE|RANK|  
||ROW_NUMBER|  
||TEXTPTR|  
  
## <a name="calling-extended-stored-procedures-from-functions"></a>Llamar a procedimientos almacenados extendidos desde funciones  
 Las funciones que llaman a procedimientos almacenados extendidos no son deterministas porque los procedimientos almacenados extendidos pueden producir efectos secundarios en la base de datos. Los efectos secundarios son cambios de un estado global de la base de datos, como una actualización de una tabla, o de un recurso externo, como un archivo o la red (por ejemplo, la modificación de un archivo o el envío de un mensaje de correo electrónico). No debe confiar en la devolución de un conjunto de resultados coherente al ejecutar un procedimiento almacenado extendido desde una función definida por el usuario. No se recomienda el uso de funciones definidas por el usuario que producen efectos secundarios en la base de datos.  
  
 Cuando se llama desde una función, el procedimiento almacenado extendido no puede devolver conjuntos de resultados al cliente. Las API de Servicios abiertos de datos que devuelven conjuntos de resultados al cliente tienen un código de retorno FAIL.  
  
 El procedimiento almacenado extendido puede volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin embargo, no puede combinar la misma transacción como la función original que invocó el procedimiento almacenado extendido.  
  
 De forma similar a las invocaciones desde un lote o un procedimiento almacenado, el procedimiento almacenado extendido se ejecuta en el contexto de la cuenta de seguridad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El propietario del procedimiento almacenado extendido debe tener esto en cuenta al conceder permisos a otros usuarios para ejecutar el procedimiento.  
  
  
