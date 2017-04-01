---
title: "DAY (expresi&#243;n de SSIS) | Microsoft Docs"
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
  - "DAY, función"
  - "fechas [Integration Services], DAY"
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# DAY (expresi&#243;n de SSIS)
  Devuelve un entero que representa la parte del día de una fecha.  
  
## Sintaxis  
  
```  
  
DAY(date)  
```  
  
## Argumentos  
 *date*  
 Expresión que devuelve una fecha válida o una cadena con formato de fecha.  
  
## Tipos de resultado  
 DT_I4  
  
## Comentarios  
 DAY devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  La expresión no puede validarse cuando un literal de fecha se convierte explícitamente en uno de estos tipos de datos de fecha: DT_DBTIMESTAMPOFFSET y DT_DBTIMESTAMP2.  
  
 Utilizar la función DAY es más sencillo pero equivalente a utilizar la función DATEPART("Day", date).  
  
## Ejemplos de expresiones  
 Este ejemplo devuelve el número del día de un literal de fecha. Si la fecha tiene el formato "mm/dd/aaaa", este ejemplo devuelve 23.  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este ejemplo devuelve el entero que representa el día en la columna **ModifiedDate** .  
  
```  
DAY(ModifiedDate)  
```  
  
 Este ejemplo devuelve el entero que representa el día de la fecha actual.  
  
```  
DAY(GETDATE())  
```  
  
## Vea también  
 [DATEADD &#40;expresión de SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;expresión de SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;expresión de SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [MONTH &#40;expresión de SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;expresión de SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  