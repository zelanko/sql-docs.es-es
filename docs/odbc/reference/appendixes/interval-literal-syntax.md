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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188816"
---
# <a name="interval-literal-syntax"></a>Sintaxis de literales de intervalo
La siguiente sintaxis se utiliza para los literales de intervalo en ODBC.  
  
 *interval-literal ::= INTERVAL* [+*&#124;*-] *interval-string interval-qualifier*  
  
 *interval-string* ::= *quote* { *year-month-literal* &#124; *day-time-literal* } *quote*  
  
 *year-month-literal* ::= *years-value* &#124; [*years-value* -] *months-value*  
  
 *day-time-literal* ::= *day-time-interval* &#124; *time-interval*  
  
 *intervalo de tiempo del día* :: = *días valor* [*horas valor* [:*minutos valor*[:*segundos valor*]]]  
  
 *time-interval* ::= *hours-value* [:*minutes-value* [:*seconds-value* ] ]  
  
 &#124; *minutes-value* [:*seconds-value* ]  
  
 &#124; *seconds-value*  
  
 *years-value* ::= *datetime-value*  
  
 *months-value* ::= *datetime-value*  
  
 *days-value* ::= *datetime-value*  
  
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
  
 *datetime-field* ::= *non-second-datetime-field* &#124; SECOND  
  
 *non-second-datetime-field* ::= YEAR &#124; MONTH &#124; DAY &#124; HOUR &#124; MINUTE  
  
 *interval-fractional-seconds-precision* ::= *unsigned-integer*  
  
 *interval-leading-field-precision* ::= *unsigned-integer*  
  
 *quote* ::= '  
  
 *entero unsigned* :: = *dígitos...*
