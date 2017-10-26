---
title: Hora y funciones de fecha (el controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bab52b29d54416dca84d18cb0cd2b832da1b4d63
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Hora y funciones de fecha (el controlador ODBC de Visual FoxPro)
En la tabla siguiente se enumera funciones de fecha y hora ODBC compatibles con el controlador ODBC de Visual FoxPro; Cuando la gramática de Visual FoxPro para la misma función difiere de la sintaxis ODBC, se muestra el equivalente de Visual FoxPro.  
  
|Gramática ODBC|Gramática Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE*)*|FECHA*)*|  
|CURTIME*)*|TIEMPO*)*|  
|DAYNAME*(date_exp)*|CDOW*(date_exp)*|  
|DAYOFMONTH (*date_exp)*|DÍA*)*|  
|HORA*(time_exp)*||  
|MINUTO*(time_exp)*||  
|MES*(time_exp)*||  
|MONTHNAME*(date_exp)*|CMONTH*(date_exp)*|  
|AHORA*)*|FECHA Y HORA*)*|  
|SEGUNDO*(time_exp)*|S*(time_exp)*|  
|SEMANA*(date_exp)*||  
|AÑO*(date_exp)*||  
  
 No se admiten las siguientes funciones de fecha y hora:  
  
 DAYOFYEAR *(date_exp)*  
  
 TRIMESTRE *(date_exp)*  
  
 TIMESTAMPADD *(intervalo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF de ODBC *(intervalo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Secuencias de Escape ODBC  
 El controlador también admite la secuencia de escape ODBC para los datos de fecha y hora. La sintaxis de la cláusula de escape es como sigue:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)—  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)—  
```  
  
 En esta sintaxis, **d.** indica que *valor* es una fecha en el *aaaa-mm-dd* formato y **ts** indica que *valor * es una marca de tiempo en el *aaaa-mm-dd hh*[.* f... *] formato. La sintaxis abreviada para datos de fecha y la marca de tiempo es como sigue:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Por ejemplo, cada una de las siguientes instrucciones actualiza la tabla ALLTYPES utilizando la sintaxis abreviada de fecha y hora en un comando SQL UPDATE compatible:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de las secuencias de escape, vea [secuencias de Escape de ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) en el *referencia del programador de ODBC*.

