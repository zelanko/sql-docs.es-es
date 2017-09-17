---
title: EN la zona HORARIA (Transact-SQL) | Documentos de Microsoft
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0983cbd76b1ec3a71985537f098f8faf002b93e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="at-time-zone-transact-sql"></a>EN la zona HORARIA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Convierte un *inputdate* a los correspondientes *datetimeoffset* valor en la zona horaria de destino. Si *inputdate* es siempre sin información de desplazamiento, la función aplica el desplazamiento de la zona horaria, suponiendo que *inputdate* valor se proporciona en la zona horaria de destino. Si *inputdate* se proporciona como un *datetimeoffset* valor, que **AT TIME ZONE** cláusula lo convierte en la zona horaria de destino mediante las reglas de conversión de zona horaria.  
  
 **EN la zona HORARIA** implementación se basa en un mecanismo de Windows para convertir **datetime** valores en distintas zonas horarias.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>Argumentos  
 *inputdate*  
 Es una expresión que se pueda resolver como un **smalldatetime**, **datetime**, **datetime2**, o **datetimeoffset** valor.  
  
 *zona horaria*  
 Nombre de la zona horaria de destino. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]se basa en las zonas horarias que se almacenan en el registro de Windows. Todas las zonas horarias instaladas en el equipo se almacenan en el subárbol del registro siguientes: **KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones**. Una lista de zonas horarias instaladas también se expone a través de la [sys.time_zone_info &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) vista.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve el tipo de datos de **datetimeoffset**  
  
## <a name="return-value"></a>Valor devuelto  
 El **datetimeoffset** valor en la zona horaria de destino.  
  
## <a name="remarks"></a>Comentarios  
 **EN la zona HORARIA** aplica reglas específicas para la conversión de valores de entrada en **smalldatetime**, **datetime** y **datetime2** tipos de datos, que se encuentran en un intervalo que se ve afectado por el cambio de horario de verano:  
  
-   Cuando el reloj está configurado con antelación, a continuación, hay una diferencia en la hora local que duración depende de la duración del ajuste del reloj (normalmente 1 hora, pero puede ser 30 o 45 minutos, dependiendo de la zona horaria). En ese caso, los puntos en el tiempo que pertenecen a este intervalo se convierten con el desplazamiento *después* cambio de horario de verano.  
  
    ```  
    /*  
        Moving to DST in "Central European Standard Time" zone: 
        offset changes from +01:00 -> +02:00   
        Change occurred on March 29th, 2015 at 02:00:00.   
        Adjusted local time became 2015-03-29 03:00:00.  
    */  
    
    --Time before DST change has standard time offset (+01:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T01:01:00', 126)     
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 01:01:00 +01:00   
  
    /*
      Adjusted time from the "gap interval" (between 02:00 and 03:00)
      is moved 1 hour ahead and presented with the summer time offset
      (after the DST change) 
    */
    SELECT CONVERT(datetime2(0), '2015-03-29T02:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00
      
    --Time after 03:00 is presented with the summer time offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00  
  
    ```  
  
- Cuando el reloj se vuelve a establecer, 2 horas de hora local se superponen en una hora.  En ese caso, se presentan los puntos en el tiempo que pertenecen al intervalo superpuesto con el desplazamiento *antes de* el cambio del reloj:  
  
    ```  
    /*  
        Moving back from DST to standard time in 
        "Central European Standard Time" zone: 
        offset changes from +02:00 -> +01:00.  
        Change occurred on October 25th, 2015 at 03:00:00.   
        Adjusted local time became 2015-10-25 02:00:00   
    */  
    
    --Time before the change has DST offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-10-25T01:01:00', 126)      
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 01:01:00 +02:00  
    
    /*
      Time from the "overlapped interval" is presented with standard time 
      offset (before the change)    
    */
    SELECT CONVERT(datetime2(0), '2015-10-25T02:00:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 02:00:00 +02:00  
    
    
    --Time after 03:00 is regularly presented with the standard time offset (+01:00)    
    SELECT CONVERT(datetime2(0), '2015-10-25T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 03:01:00 +01:00
  
    ```  

Puesto que parte de la información (por ejemplo, las reglas de zona horaria) se mantiene fuera de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y están sujetos a cambios ocasionales, el **AT TIME ZONE** función se clasifica como no deterministas. 
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. Agregar ajuste de zona horaria de destino a la fecha y hora sin información de desplazamiento  
 Use **AT TIME ZONE** para agregar desplazamiento basándose en reglas de zona horaria cuando sepa que el original **datetime** valores se proporcionan en la misma zona horaria:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>B. Convertir valores entre las diferentes zonas horarias  
 En el ejemplo siguiente se convierte los valores entre zonas horarias diferentes:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>C. Consultar las tablas temporales con la zona horaria local  
 El siguiente ejemplo, selecciona datos de una tabla temporal.  
  
```  
USE AdventureWorks2016;  
GO  
  
DECLARE @ASOF datetimeoffset;  
SET @ASOF = DATEADD (month, -1, GETDATE()) AT TIME ZONE 'UTC';  
  
-- Query state of the table a month ago projecting period   
-- columns as Pacific Standard Time  
SELECT BusinessEntityID, PersonType, NameStyle, Title,   
    FirstName, MiddleName,  
    ValidFrom AT TIME ZONE 'Pacific Standard Time' 
FROM  Person.Person_Temporal  
FOR SYSTEM_TIME AS OF @ASOF;  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de fecha y hora](../../t-sql/data-types/date-and-time-types.md)   
 [Datos de fecha y hora funciones y tipos de &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  

