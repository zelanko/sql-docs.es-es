---
title: Hora y funciones de fecha (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf8e7552faf9567dab25ee3dc5b7b293034faef0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632775"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Hora y funciones de fecha (el controlador ODBC de Visual FoxPro)
La tabla siguiente muestran funciones de fecha y hora ODBC compatibles con el controlador ODBC de Visual FoxPro; Cuando la gramática de Visual FoxPro para la misma función difiere de la sintaxis ODBC, se muestra el equivalente de Visual FoxPro.  
  
|Gramática ODBC|Gramática Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE *( )*|DATE *( )*|  
|CURTIME *( )*|TIME *( )*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH(*date_exp)*|DAY *( )*|  
|HOUR *(time_exp)*||  
|MINUTE *(time_exp)*||  
|MONTH *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|NOW *( )*|DATETIME *( )*|  
|SECOND *(time_exp)*|SEC *(time_exp)*|  
|WEEK *(date_exp)*||  
|YEAR *(date_exp)*||  
  
 No se admiten las siguientes funciones de fecha y hora:  
  
 DAYOFYEAR *(date_exp)*  
  
 QUARTER *(date_exp)*  
  
 TIMESTAMPADD *(intervalo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF no *(intervalo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Secuencias de escape ODBC  
 El controlador admite también la secuencia de escape ODBC para los datos de fecha y hora. La sintaxis de la cláusula de escape es como sigue:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 En esta sintaxis, **d.** indica que *valor* es una fecha en la *aaaa-mm-dd* formato y **ts** indica que *valor*  es una marca de tiempo en el *aaaa-mm-dd hh: mm:* [.*f...* ] formato. La sintaxis abreviada para datos de fecha y la marca de tiempo es como sigue:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Por ejemplo, cada una de las siguientes instrucciones actualiza la tabla ALLTYPES utilizando la sintaxis abreviada de fecha y hora en un comando SQL UPDATE admitido:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de las secuencias de escape, consulte [secuencias de Escape de ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) en el *referencia del programador de ODBC*.
