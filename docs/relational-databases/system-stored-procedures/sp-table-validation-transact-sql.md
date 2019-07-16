---
title: sp_table_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42d2535dedb1161a78362f17a1ad7c79ca49bb87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096123"
---
# <a name="sptablevalidation-transact-sql"></a>sp_table_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Devuelve el recuento de filas o la suma de comprobación de una tabla o vista indizada, o bien compara el recuento de filas o la suma de comprobación proporcionados con los de la tabla o vista indizada especificada. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicaciones y en el suscriptor de la base de datos de suscripciones. *No se admite para publicadores de Oracle*.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_table_validation [ @table = ] 'table'  
    [ , [ @expected_rowcount = ] type_of_check_requested OUTPUT]  
    [ , [ @expected_checksum = ] expected_checksum OUTPUT]  
    [ , [ @rowcount_only = ] rowcount_only ]  
    [ , [ @owner = ] 'owner' ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @table_name = ] table_name ]  
    [ , [ @column_list = ] 'column_list' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table = ] 'table'` Es el nombre de la tabla. *tabla* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @expected_rowcount = ] expected_rowcountOUTPUT` Especifica si se debe devolver el número esperado de filas de la tabla. *expected_rowcount* es **int**, su valor predeterminado es null. Si es NULL, el recuento de filas real se devuelve como parámetro de salida. Si se proporciona un valor, dicho valor se compara con el recuento de filas real para identificar posibles diferencias.  
  
`[ @expected_checksum = ] expected_checksumOUTPUT` Especifica si se devuelve la suma de comprobación esperada para la tabla. *expected_checksum* es **numérico**, su valor predeterminado es null. Si es NULL, la suma de comprobación real se devuelve como parámetro de salida. Si se proporciona un valor, dicho valor se compara con la suma de comprobación real para identificar posibles diferencias.  
  
`[ @rowcount_only = ] type_of_check_requested` Especifica qué tipo de suma de comprobación o recuento de filas para realizar. *type_of_check_requested* es **smallint**, su valor predeterminado es **1**.  
  
 Si **0**, realizar un recuento de filas y un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suma de comprobación compatible con 7.0.  
  
 Si **1**, realizar solo una comprobación del recuento de filas.  
  
 Si **2**, realizar un recuento de filas y binario de suma de comprobación.  
  
`[ @owner = ] 'owner'` Es el nombre del propietario de la tabla. *propietario* es **sysname**, su valor predeterminado es null.  
  
`[ @full_or_fast = ] full_or_fast` Es el método utilizado para calcular el recuento de filas. *full_or_fast* es **tinyint**, su valor predeterminado es **2**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Realiza un recuento completo mediante COUNT(*).|  
|**1**|Un recuento rápido desde **sysindexes.rows**. Recuento de filas en **sysindexes** es mucho más rápido que el recuento de filas en la tabla real. Sin embargo, dado que **sysindexes** constantemente actualizado, el recuento de filas puede no ser exacto.|  
|**2** (predeterminado)|Realiza un recuento rápido condicional intentando primero el método rápido. Si el método rápido muestra diferencias, se utiliza el método completo. Si *expected_rowcount* es NULL y el procedimiento almacenado que se usa para obtener el valor, una completa COUNT(*) siempre se utiliza.|  
  
`[ @shutdown_agent = ] shutdown_agent` Si se está ejecutando el agente de distribución **sp_table_validation**, especifica si el agente de distribución debe cerrarse inmediatamente tras la finalización de la validación. *shutdown_agent* es **bit**, su valor predeterminado es **0**. Si **0**, el agente de replicación no se cierra. Si **1**, se produce el error 20578 y el agente de replicación se señala a apagar. Este parámetro se omite cuando **sp_table_validation** es ejecutado directamente por un usuario.  
  
`[ @table_name = ] table_name` Es el nombre de tabla de la vista utilizada para los mensajes de salida. *table_name* es **sysname**, su valor predeterminado es **@table** .  
  
`[ @column_list = ] 'column_list'` Es la lista de columnas que se debe usar en la función de suma de comprobación. *column_list* es **nvarchar (4000)** , su valor predeterminado es null. Habilita la validación de artículos de mezcla para especificar una lista de columnas que excluya las columnas calculadas y de marca de tiempo.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Si realiza una validación de suma de comprobación y la suma de comprobación esperada es igual a la suma de comprobación en la tabla, **sp_table_validation** devuelve un mensaje que la tabla ha pasado la validación de suma de comprobación. De lo contrario, devuelve un mensaje que indica que la tabla puede no estar sincronizada e informa de la diferencia entre el número de filas real y el esperado.  
  
 Si realiza una validación de recuento de filas y el número de filas esperado es igual al número de la tabla, **sp_table_validation** devuelve un mensaje que la tabla ha pasado la validación del recuento de filas. De lo contrario, devuelve un mensaje que indica que la tabla puede no estar sincronizada e informa de la diferencia entre el número de filas real y el esperado.  
  
## <a name="remarks"></a>Comentarios  
 **sp_table_validation** se utiliza en todos los tipos de replicación. **sp_table_validation** no se admite para publicadores de Oracle.  
  
 La suma de comprobación calcula una prueba de redundancia cíclica (CRC, Cyclic Redundancy Check) de 32 bits sobre la imagen completa de la fila en la página. No comprueba las columnas de forma selectiva y no puede operar sobre vistas ni particiones verticales de la tabla. Además, la suma de comprobación omite el contenido de **texto** y **imagen** columnas (por diseño).  
  
 Al realizar una suma de comprobación, la estructura de la tabla debe ser idéntica en los dos servidores; es decir, las tablas deben tener las mismas columnas y en el mismo orden, el mismo tipo de datos y la misma longitud, y las mismas condiciones NULL o NOT NULL. Por ejemplo, si el publicador ejecutó CREATE TABLE y, a continuación, ALTER TABLE para agregar columnas, pero el script aplicado en el suscriptor es simplemente CREATE TABLE, la estructura NO será la misma. Si no está seguro de que la estructura de las dos tablas es idéntica, examine [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) y confirme que el desplazamiento de cada tabla es el mismo.  
  
 Valores de punto flotante suelen provocar diferencias de suma de comprobación de si el modo de carácter **bcp** se utilizó, que es el caso si la publicación tiene que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores. Dichas diferencias se deben a pequeñas e inevitables diferencias de precisión en la conversión desde y hacia el modo de carácter.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar **sp_table_validation**, debe tener permisos SELECT en la tabla que se está validando.  
  
## <a name="see-also"></a>Vea también  
 [CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
