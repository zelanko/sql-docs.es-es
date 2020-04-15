---
title: Funciones de hora y fecha (controlador ODBC de Visual FoxPro) Microsoft Docs
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
ms.openlocfilehash: 86260f8e7245bed15122d4dbfc4649131674e17f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303066"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Hora y funciones de fecha (el controlador ODBC de Visual FoxPro)
En la tabla siguiente se enumeran las funciones de hora y fecha ODBC admitidas por el controlador ODBC de Visual FoxPro; cuando la gramática de Visual FoxPro para la misma función difiere de la sintaxis ODBC, se muestra el equivalente de Visual FoxPro.  
  
|Gramática ODBC|Gramática Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE *( )*|FECHA *( )*|  
|CURTIME *( )*|TIEMPO *( )*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH(*date_exp)*|DIA *( )*|  
|HORA *(time_exp)*||  
|MINUTO *(time_exp)*||  
|MES *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|AHORA *( )*|FECHAHORA *( )*|  
|SEGUNDO *(time_exp)*|SEC *(time_exp)*|  
|SEMANA *(date_exp)*||  
|Año *(date_exp)*||  
  
 No se admiten las siguientes funciones de fecha y hora:  
  
 DAYOFYEAR *(date_exp)*  
  
 QUARTER *(date_exp)*  
  
 TIMESTAMPADD *(intervalo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(intervalo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Secuencias de escape ODBC  
 El controlador también admite la secuencia de escape ODBC para los datos de fecha y hora. La sintaxis de la cláusula de escape es la siguiente:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 En esta sintaxis, **d** indica que *value* es una fecha en el formato *aaaa-mm-dd* y **ts** indica que *value* es una marca de tiempo en *aaaa-mm-dd hh:mm:ss*[.* f...*] Formato. La sintaxis abreviada para los datos de fecha y marca de tiempo es la siguiente:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Por ejemplo, cada una de las instrucciones siguientes actualiza la tabla ALLTYPES mediante la sintaxis abreviada de fecha y marca de tiempo en un comando UPDATE de SQL compatible:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Observaciones  
 Para obtener más información acerca de las secuencias de escape, vea [Secuencias](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) de escape en ODBC en la *referencia del programador ODBC*.
