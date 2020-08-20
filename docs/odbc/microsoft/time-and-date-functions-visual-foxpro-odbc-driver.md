---
description: Hora y funciones de fecha (el controlador ODBC de Visual FoxPro)
title: Funciones de fecha y hora (controlador ODBC de Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d537411481a8bc6c9065e8e86c216c8c0637e565
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500078"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Hora y funciones de fecha (el controlador ODBC de Visual FoxPro)
En la tabla siguiente se enumeran las funciones de fecha y hora de ODBC compatibles con el controlador ODBC de Visual FoxPro; Cuando la gramática de Visual FoxPro para la misma función difiere de la sintaxis de ODBC, se muestra el equivalente de Visual FoxPro.  
  
|Gramática de ODBC|Gramática de Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE *()*|FECHA *()*|  
|CURTIME *()*|HORA *()*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH (*date_exp)*|DÍA *()*|  
|HORA *(time_exp)*||  
|MINUTO *(time_exp)*||  
|MES *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|AHORA *()*|DATETIME *()*|  
|SEGUNDO *(time_exp)*|S *(time_exp)*|  
|SEMANA *(date_exp)*||  
|AÑO *(date_exp)*||  
  
 No se admiten las siguientes funciones de fecha y hora:  
  
 DAYOFYEAR *(date_exp)*  
  
 TRIMESTRE *(date_exp)*  
  
 TIMESTAMPADD *(intervalo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(intervalo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Secuencias de escape ODBC  
 El controlador también admite la secuencia de escape de ODBC para los datos de fecha y marca de tiempo. La sintaxis de la cláusula escape es la siguiente:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 En esta sintaxis, **d** indica que el *valor* es una fecha con el formato *AAAA-MM-DD* y que **TS** indica que el *valor* es una marca de tiempo en el *AAAA-MM-DD HH: mm: SS*[.* f...*] Aplique. La sintaxis abreviada para los datos de fecha y marca de tiempo es la siguiente:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Por ejemplo, cada una de las siguientes instrucciones actualiza la tabla ALLTYPES mediante la sintaxis abreviada de fecha y marca de tiempo en un comando de actualización de SQL compatible:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Observaciones  
 Para obtener más información acerca de las secuencias de escape, vea [secuencias de escape en ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) en la *Referencia del programador de ODBC*.
