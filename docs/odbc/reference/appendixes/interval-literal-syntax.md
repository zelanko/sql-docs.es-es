---
title: Sintaxis de literales de intervalo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d477dbc6b54d7ebd82b7e2ef8611f5f6dd807e83
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694063"
---
# <a name="interval-literal-syntax"></a>Sintaxis de literales de intervalo
La siguiente sintaxis se utiliza para los literales de intervalo en ODBC.  
  
 *literal de intervalo:: = intervalo* [+*&#124;*-] *calificador de intervalo de cadena del intervalo*  
  
 *intervalo de cadena* :: = *oferta* { *literal del mes de año* &#124; *literal de hora del día* } *oferta*  
  
 *literal de mes del año* :: = *años valor* &#124; [*años valor* -] *valor de los meses*  
  
 *literal de hora del día* :: = *intervalo de tiempo del día* &#124; *intervalo de tiempo*  
  
 *intervalo de tiempo del día* :: = *días valor* [*horas valor* [:*minutos valor*[:*segundos valor*]]]  
  
 *intervalo de tiempo* :: = *horas valor* [:*minutos valor* [:*segundos valor* ]]  
  
 &#124;*minutos valor* [:*segundos valor* ]  
  
 &#124;*valor de segundos*  
  
 *valor del año* :: = *valor de fecha y hora*  
  
 *valor de los meses* :: = *valor de fecha y hora*  
  
 *valor de días* :: = *valor de fecha y hora*  
  
 *valor de horas* :: = *valor de fecha y hora*  
  
 *valor de minutos* :: = *valor de fecha y hora*  
  
 *valor de segundos* :: = *valor del entero de segundos* [. [ *fracción de segundos*]]  
  
 *valor de entero de segundos* :: = *entero sin signo*  
  
 *fracción de segundos* :: = *entero sin signo*  
  
 *valor de fecha y hora* :: = *entero sin signo*  
  
 *calificador de intervalo* :: = *inicio campo* TO *final campo* &#124; *único campo de fecha y hora*  
  
 *campo de inicio* :: = *segundo no-datetime-campo* [(*intervalo líderes campo precisión* )]  
  
 *campo de finalización* :: = *segundo no-datetime-campo* &#124; segundo [(*intervalo de fracciones de segundos-precisión*)]  
  
 *único campo de fecha y hora* :: = *segundo no-datetime-campo* [(*intervalo líderes campo precisión*)] &#124; segundo [(*intervalo líderes campo precisión*  [, (*intervalo de fracciones de segundos-precisión*)]  
  
 *campo de fecha y hora* :: = *segundo no-datetime-campo* &#124; segundo  
  
 *segundo no-datetime-campo* :: = año &#124; mes &#124; día &#124; hora &#124; minuto  
  
 *intervalo de fracciones de segundos-precisión* :: = *entero sin signo*  
  
 *intervalo inicial campo precisión* :: = *entero sin signo*  
  
 *oferta* :: = '  
  
 *entero unsigned* :: = *dígitos...*
