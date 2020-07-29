---
title: Funciones deterministas y no deterministas | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7df37d9b9339ef98e438e15678c0781df2875a18
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247268"
---
# <a name="deterministic-and-nondeterministic-functions"></a>Funciones deterministas y no deterministas
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Las funciones deterministas devuelven siempre el mismo resultado cada vez que se invocan con un conjunto específico de valores de entrada y cuando el estado de la base de datos es el mismo. Las funciones no deterministas pueden devolver resultados diferentes cada vez que se llaman con un conjunto específico de valores de entrada aunque el estado de la base de datos a la que tienen acceso permanezca sin cambios. Por ejemplo, la función AVG siempre devuelve el mismo resultado dadas las condiciones indicadas anteriormente pero la función GETDATE, que devuelve el valor datetime actual, siempre devuelve un resultado diferente.  
  
 Son varias las propiedades de las funciones definidas por el usuario que determinan la capacidad de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para indizar los resultados de la función, ya sea mediante índices en columnas calculadas que llaman a la función o mediante vistas indizadas que hacen referencia a la función. El determinismo de una función es una propiedad así. Por ejemplo, no se puede crear un índice clúster en una vista si ésta hace referencia a funciones no deterministas. Para obtener más información sobre las propiedades de las funciones, incluido el determinismo, vea [Funciones definidas por el usuario](../../relational-databases/user-defined-functions/user-defined-functions.md).  
  
 En este tema se identifica el determinismo de las funciones integradas del sistema y el efecto de las funciones definidas por el usuario en la propiedad determinista cuando ésta contiene una llamada a los procedimientos almacenados extendidos.  
  
## <a name="built-in-function-determinism"></a>Determinismo de las funciones integradas  
 El determinismo de las funciones integradas no se ve afectado por el usuario. Las funciones integradas son deterministas o no deterministas según el modo en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]implementa cada función. Por ejemplo, al especificar una cláusula ORDER BY en una consulta, no se cambia el determinismo de una función que se usa en la consulta.  
  
 Todas las funciones integradas de cadena son deterministas, excepto [FORMAT](../../t-sql/functions/format-transact-sql.md). Para obtener una lista de estas funciones, vea [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md).  
  
 Las siguientes funciones integradas procedentes de categorías de funciones integradas que no son de cadena siempre son deterministas.  
  
:::row:::
    :::column:::
        ABS
    :::column-end:::
    :::column:::
        DATEDIFF
    :::column-end:::
    :::column:::
        POWER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ACOS
    :::column-end:::
    :::column:::
        DAY
    :::column-end:::
    :::column:::
        RADIANS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ASIN
    :::column-end:::
    :::column:::
        DEGREES
    :::column-end:::
    :::column:::
        ROUND
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ATAN
    :::column-end:::
    :::column:::
        EXP
    :::column-end:::
    :::column:::
        SIGN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ATN2
    :::column-end:::
    :::column:::
        FLOOR
    :::column-end:::
    :::column:::
        SIN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CEILING
    :::column-end:::
    :::column:::
        ISNULL
    :::column-end:::
    :::column:::
        SQUARE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COALESCE
    :::column-end:::
    :::column:::
        ISNUMERIC
    :::column-end:::
    :::column:::
        SQRT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COS
    :::column-end:::
    :::column:::
        REGISTRO
    :::column-end:::
    :::column:::
        TAN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COT
    :::column-end:::
    :::column:::
        LOG10
    :::column-end:::
    :::column:::
        YEAR
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DATALENGTH
    :::column-end:::
    :::column:::
        MONTH
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DATEADD
    :::column-end:::
    :::column:::
        NULLIF
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
 Las siguientes funciones no siempre son deterministas, pero pueden utilizarse en vistas indizadas o en índices de columnas calculadas si se especifican de una manera determinista.  
  
|Función|Comentarios|  
|--------------|--------------|  
|todas las funciones de agregado|Todas las funciones de agregado son deterministas a menos que se especifiquen con las cláusulas OVER y ORDER BY. Para obtener una lista de estas funciones, vea [Funciones de agregado &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md).|  
|CAST|Deterministas, a menos que se usen con **datetime**, **smalldatetime**o **sql_variant**.|  
|CONVERT|Determinista, a menos que se cumpla una de estas condiciones:<br /><br /> <br /><br /> El tipo de origen es **sql_variant**.<br /><br /> El tipo de destino es **sql_variant** y su tipo de origen no es determinista.<br /><br /> El tipo de origen o destino es **datetime** o **smalldatetime**, el otro tipo de origen o destino es una cadena de caracteres, y se especifica un tipo de estilo no determinista. Para que sea determinista, el parámetro de estilo debe ser una constante. Además, los estilos menores o iguales que 100 son no deterministas, salvo los estilos 20 y 21. Los estilos mayores que 100 son deterministas, salvo los estilos 106, 107, 109 y 113.|  
|CHECKSUM|Determinista, excepto CHECKSUM(*).|  
|ISDATE|Determinista solo si se utiliza con la función CONVERT, se especifica el parámetro de estilo CONVERT y el estilo no es igual a 0, 100, 9 ni 109.|  
|RAND|RAND es determinista solo cuando se especifica un parámetro *seed* .|  
  
 Todas las funciones de configuración, cursores, metadatos, seguridad y estadísticas del sistema no son deterministas. Para obtener una lista de estas funciones, vea [Funciones de configuración &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md), [Funciones de cursor &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md), [Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md), [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md) y [Funciones estadísticas del sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md).  
  
 Las siguientes funciones integradas, procedentes de otras categorías, no son deterministas nunca.  
  
:::row:::
    :::column:::
        @@CONNECTIONS
    :::column-end:::
    :::column:::
        GETDATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@CPU_BUSY
    :::column-end:::
    :::column:::
        GETUTCDATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@DBTS
    :::column-end:::
    :::column:::
        GET_TRANSMISSION_STATUS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IDLE
    :::column-end:::
    :::column:::
        LAG
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IO_BUSY
    :::column-end:::
    :::column:::
        LAST_VALUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@MAX_CONNECTIONS
    :::column-end:::
    :::column:::
        LEAD
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACK_RECEIVED
    :::column-end:::
    :::column:::
        MIN_ACTIVE_ROWVERSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACK_SENT
    :::column-end:::
    :::column:::
        NEWID
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACKET_ERRORS
    :::column-end:::
    :::column:::
        NEWSEQUENTIALID
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TIMETICKS
    :::column-end:::
    :::column:::
        NEXT VALUE FOR
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_ERRORS
    :::column-end:::
    :::column:::
        NTILE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_READ
    :::column-end:::
    :::column:::
        PARSENAME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_WRITE
    :::column-end:::
    :::column:::
        PERCENTILE_CONT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        AT TIME ZONE
    :::column-end:::
    :::column:::
        PERCENTILE_DISC
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CUME_DIST
    :::column-end:::
    :::column:::
        PERCENT_RANK
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CURRENT_TIMESTAMP
    :::column-end:::
    :::column:::
        RAND
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DENSE_RANK
    :::column-end:::
    :::column:::
        RANK
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        FIRST_VALUE
    :::column-end:::
    :::column:::
        ROW_NUMBER
    :::column-end:::
:::row-end:::   
:::row:::
    :::column:::
        FORMAT
    :::column-end:::
    :::column:::
        TEXTPTR
    :::column-end:::
:::row-end:::
 
## <a name="calling-extended-stored-procedures-from-functions"></a>Llamar a procedimientos almacenados extendidos desde funciones  
 Las funciones que llaman a procedimientos almacenados extendidos no son deterministas porque los procedimientos almacenados extendidos pueden producir efectos secundarios en la base de datos. Los efectos secundarios son cambios de un estado global de la base de datos, como una actualización de una tabla, o de un recurso externo, como un archivo o la red (por ejemplo, la modificación de un archivo o el envío de un mensaje de correo electrónico). No confíe en la devolución de un conjunto de resultados coherente al ejecutar un procedimiento almacenado extendido desde una función definida por el usuario. No se recomienda el uso de funciones definidas por el usuario que producen efectos secundarios en la base de datos.  
  
 Cuando se llama desde una función, el procedimiento almacenado extendido no puede devolver conjuntos de resultados al cliente. Las API de Servicios abiertos de datos que devuelven conjuntos de resultados al cliente tienen un código de retorno FAIL.  
  
 El procedimiento almacenado extendido puede volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin embargo, no puede combinar la misma transacción como la función original que invocó el procedimiento almacenado extendido.  
  
 De forma similar a las invocaciones desde un lote o un procedimiento almacenado, el procedimiento almacenado extendido se ejecuta en el contexto de la cuenta de seguridad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El propietario del procedimiento almacenado extendido debe tener en cuenta los permisos de este contexto de seguridad al conceder permisos a otros usuarios para ejecutar el procedimiento.  
  
  
