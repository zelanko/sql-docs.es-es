---
title: sp_sequence_get_range (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/08/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_sequence_get_range
- sp_sequence_get_range_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sequence number object, sp_sequence_get_range procedure
- sp_sequence_get_range
ms.assetid: 8ca6b0c6-8d9c-4eee-b02f-51ddffab4492
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2b2dc833e0d80aecc82e4d2382b33f1b93df193
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spsequencegetrange-transact-sql"></a>sp_sequence_get_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-asdw-xxx-md.md)]

  Devuelve un intervalo de valores de secuencia de un objeto de secuencia. El objeto de secuencia genera y emite el número de valores solicitados y proporciona a la aplicación metadatos relacionados con el intervalo.  
  
 Para obtener más información acerca de los números de secuencia, vea [números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
||  
|-|  
|**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_sequence_get_range [ @sequence_name = ] N'<sequence>'   
     , [ @range_size = ] range_size  
     , [ @range_first_value = ] range_first_value OUTPUT   
    [, [ @range_last_value = ] range_last_value OUTPUT ]  
    [, [ @range_cycle_count = ] range_cycle_count OUTPUT ]  
    [, [ @sequence_increment = ] sequence_increment OUTPUT ]  
    [, [ @sequence_min_value = ] sequence_min_value OUTPUT ]  
    [, [ @sequence_max_value = ] sequence_max_value OUTPUT ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@sequence_name**  =] **N**'*secuencia*'  
 Nombre del objeto de secuencia. El esquema es opcional. *sequence_name* es **nvarchar(776)**.  
  
 [  **@range_size**  =] *range_size*  
 Número de valores que se van a capturar de la secuencia. **@range_size**es **bigint**.  
  
 [  **@range_first_value**  =] *range_first_value*  
 El parámetro de salida devuelve el primer valor (mínimo o máximo) del objeto de secuencia que se usa para calcular el intervalo solicitado. **@range_first_value**es **sql_variant** con el mismo tipo base que el objeto de secuencia utilizado en la solicitud.  
  
 [  **@range_last_value**  =] *range_last_value*  
 El parámetro de salida opcional devuelve el último valor del intervalo solicitado. **@range_last_value**es **sql_variant** con el mismo tipo base que el objeto de secuencia utilizado en la solicitud.  
  
 [  **@range_cycle_count**  =] range_cycle_count  
 El parámetro de salida opcional devuelve el número de veces que se recorre el objeto de secuencia para devolver el intervalo solicitado. **@range_cycle_count**es **int**.  
  
 [  **@sequence_increment**  =] *sequence_increment*  
 El parámetro de salida opcional devuelve el incremento del objeto de secuencia utilizado para calcular el intervalo solicitado. **@sequence_increment**es **sql_variant** con el mismo tipo base que el objeto de secuencia utilizado en la solicitud.  
  
 [  **@sequence_min_value**  =] *sequence_min_value*  
 El parámetro de salida opcional devuelve el valor mínimo del objeto de secuencia. **@sequence_min_value**es **sql_variant** con el mismo tipo base que el objeto de secuencia utilizado en la solicitud.  
  
 [  **@sequence_max_value**  =] *sequence_max_value*  
 El parámetro de salida opcional devuelve el valor máximo del objeto de secuencia. **@sequence_max_value**es **sql_variant** con el mismo tipo base que el objeto de secuencia utilizado en la solicitud.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_sequence_get_rangeis en sys. esquema y se puede hacer referencia como sys.sp_sequence_get_range.  
  
### <a name="cycling-sequences"></a>Secuencias con recorrido  
 Si es necesario, el objeto de secuencia hará el recorrido el número adecuado de veces para atender el intervalo solicitado. El número de veces que se recorre se devuelve al autor de llamada a través del parámetro `@range_cycle_count`.  
  
> [!NOTE]  
>  Al hacer el recorrido, un objeto de flujo se reinicia desde el valor mínimo en el caso de una secuencia ascendente y desde el valor máximo si se trata de una secuencia descendente, no desde el valor inicial del objeto de secuencia.  
  
### <a name="non-cycling-sequences"></a>Secuencias sin recorrido  
 Si el número de valores del intervalo solicitado es mayor que los valores disponibles restantes en el objeto de secuencia, el intervalo solicitado no se deduce del objeto de secuencia y se devuelve el siguiente error 11732:  
  
 `The requested range for sequence object '%.*ls' exceeds the maximum or minimum limit. Retry with a smaller range.`  
  
## <a name="permissions"></a>Permissions  
 Se necesita el permiso UPDATE en el objeto de secuencia o el esquema del objeto de secuencia.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes usan un objeto de secuencia denominado Test.RangeSeq. Utilice la siguiente instrucción para crear la secuencia de Test.RangeSeq.  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.RangeSeq  
    AS int   
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 25  
    CYCLE  
    CACHE 10  
;  
```  
  
### <a name="a-retrieving-a-range-of-sequence-values"></a>A. Recuperar un intervalo de valores de secuencia  
 La siguiente instrucción obtiene cuatro números de secuencia del objeto de secuencia Test.RangeSeq y devuelve el primero de los números para el usuario.  
  
```  
DECLARE @range_first_value sql_variant ,   
        @range_first_value_output sql_variant ;  
  
EXEC sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 4  
, @range_first_value = @range_first_value_output OUTPUT ;  
  
SELECT @range_first_value_output AS FirstNumber ;  
  
```  
  
### <a name="b-returning-all-output-parameters"></a>B. Devolver todos los parámetros de salida  
 El ejemplo siguiente devuelve todos los valores de salida del procedimiento sp_sequence_get_range.  
  
```  
DECLARE    
  @FirstSeqNum sql_variant  
, @LastSeqNum sql_variant  
, @CycleCount int  
, @SeqIncr sql_variant  
, @SeqMinVal sql_variant  
, @SeqMaxVal sql_variant ;  
  
EXEC sys.sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 5  
, @range_first_value = @FirstSeqNum OUTPUT   
, @range_last_value = @LastSeqNum OUTPUT   
, @range_cycle_count = @CycleCount OUTPUT  
, @sequence_increment = @SeqIncr OUTPUT  
, @sequence_min_value = @SeqMinVal OUTPUT  
, @sequence_max_value = @SeqMaxVal OUTPUT ;  
  
-- The following statement returns the output values  
SELECT  
  @FirstSeqNum AS FirstVal  
, @LastSeqNum AS LastVal  
, @CycleCount AS CycleCount  
, @SeqIncr AS SeqIncrement  
, @SeqMinVal AS MinSeq  
, @SeqMaxVal AS MaxSeq ;  
  
```  
  
 Cambiar el argumento `@range_size` a un número grande como 75 hará que el objeto de secuencia haga un recorrido. Compruebe el argumento `@range_cycle_count` para determinar si se ha recorrido el objeto de secuencia y, en caso afirmativo, cuántas veces.  
  
### <a name="c-example-using-adonet"></a>C. Ejemplo utilizando ADO.NET  
 En el ejemplo siguiente se obtiene un intervalo de la Test.RangeSeq mediante ADO.NET.  
  
```  
SqlCommand cmd = new SqlCommand();  
cmd.Connection = conn;  
cmd.CommandType = CommandType.StoredProcedure;  
cmd.CommandText = "sys.sp_sequence_get_range";  
cmd.Parameters.AddWithValue("@sequence_name", "Test.RangeSeq");  
cmd.Parameters.AddWithValue("@range_size", 10);  
  
// Specify an output parameter to retreive the first value of the generated range.  
SqlParameter firstValueInRange = new SqlParameter("@range_first_value", SqlDbType.Variant);  
firstValueInRange.Direction = ParameterDirection.Output;  
cmd.Parameters.Add(firstValueInRange);  
  
conn.Open();  
cmd.ExecuteNonQuery();  
  
// Output the first value of the generated range.  
Console.WriteLine(firstValueInRange.Value);  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear secuencia de &#40; Transact-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [Eliminar secuencia &#40; Transact-SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [VALOR siguiente para &#40; Transact-SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
