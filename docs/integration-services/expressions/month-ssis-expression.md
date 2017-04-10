---
title: "MONTH (expresi&#243;n de SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "fechas [Integration Services], MONTH"
  - "MONTH, función"
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# MONTH (expresi&#243;n de SSIS)
  Devuelve un entero que representa la parte del mes de una fecha.  
  
## Sintaxis  
  
```  
  
MONTH(date)  
```  
  
## Argumentos  
 *date*  
 Fecha con cualquier formato de fecha.  
  
## Tipos de resultado  
 DT_I4  
  
## Comentarios  
 MONTH devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  La expresión no puede validarse cuando un literal de fecha se convierte explícitamente en uno de estos tipos de datos de fecha: DT_DBTIMESTAMPOFFSET y DT_DBTIMESTAMP2.  
  
 Utilizar la función MONTH es más sencillo pero equivalente a utilizar la función DATEPART("Month", date).  
  
## Ejemplos de expresiones  
 Este ejemplo devuelve el número del mes de un literal de fecha. Si la fecha tiene el formato "mm/dd/aaaa", este ejemplo devuelve 11.  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este ejemplo devuelve el entero que representa el mes en la columna **ModifiedDate** .  
  
```  
MONTH(ModifiedDate)  
```  
  
 Este ejemplo devuelve el entero que representa el mes de la fecha actual.  
  
```  
MONTH(GETDATE())  
```  
  
## Vea también  
 [DATEADD &#40;expresión de SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;expresión de SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;expresión de SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;expresión de SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [YEAR &#40;expresión de SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  