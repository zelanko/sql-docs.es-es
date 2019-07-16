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
ms.openlocfilehash: 6352a5ae894adb09f714a78386bfecfa3ce1df77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041624"
---
# <a name="interval-literal-syntax"></a>Sintaxis de literales de intervalo
La siguiente sintaxis se utiliza para los literales de intervalo en ODBC.  
  
 *literal de intervalo:: = intervalo* [+ *&#124;* -] *calificador de intervalo de cadena del intervalo*  
  
 *interval-string* ::= *quote* { *year-month-literal* &#124; *day-time-literal* } *quote*  
  
 *literal de mes del año* :: = *años valor* &#124; [*años valor* -] *valor de los meses*  
  
 *day-time-literal* ::= *day-time-interval* &#124; *time-interval*  
  
 *intervalo de tiempo del día* :: = *días valor* [*horas valor* [:*minutos valor*[:*segundos valor*]]]  
  
 *intervalo de tiempo* :: = *horas valor* [:*minutos valor* [:*segundos valor* ]]  
  
 &#124;*minutos valor* [:*segundos valor* ]  
  
 &#124; *seconds-value*  
  
 *valor del año* :: = *valor de fecha y hora*  
  
 *valor de los meses* :: = *valor de fecha y hora*  
  
 *valor de días* :: = *valor de fecha y hora*  
  
 *valor de horas* :: = *valor de fecha y hora*  
  
 *valor de minutos* :: = *valor de fecha y hora*  
  
 *seconds-value* ::= *seconds-integer-value* [.[*seconds-fraction*] ]  
  
 *seconds-integer-value* ::= *unsigned-integer*  
  
 *seconds-fraction* ::= *unsigned-integer*  
  
 *datetime-value* ::= *unsigned-integer*  
  
 *calificador de intervalo* :: = *inicio campo* TO *final campo* &#124; *único campo de fecha y hora*  
  
 *start-field* ::= *non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *campo de finalización* :: = *segundo no-datetime-campo* &#124; segundo [(*intervalo de fracciones de segundos-precisión*)]  
  
 *único campo de fecha y hora* :: = *segundo no-datetime-campo* [(*intervalo líderes campo precisión*)] &#124; segundo [(*intervalo líderes campo precisión*  [, (*intervalo de fracciones de segundos-precisión*)]  
  
 *campo de fecha y hora* :: = *segundo no-datetime-campo* &#124; segundo  
  
 *segundo no-datetime-campo* :: = año &#124; mes &#124; día &#124; hora &#124; minuto  
  
 *interval-fractional-seconds-precision* ::= *unsigned-integer*  
  
 *interval-leading-field-precision* ::= *unsigned-integer*  
  
 *oferta* :: = '  
  
 *entero unsigned* :: = *dígitos...*
