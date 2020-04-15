---
title: Sintaxis literal de intervalos ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3387b07a8e769206a6a495addff4287000691fec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290575"
---
# <a name="interval-literal-syntax"></a>Sintaxis de literales de intervalo
La sintaxis siguiente se utiliza para los literales de intervalo en ODBC.  
  
 *interval-literal ::- INTERVAL* [+*&#124;*-] *interval-string interval-qualifier*  
  
 *interval-string* ::- *cita* - *año-mes-literal* &#124; *día-tiempo-literal* - *cita*  
  
 *año-mes-literal* ::- *valor de años* &#124; [*años-valor* -] *valor de meses-*  
  
 *día-tiempo-literal* ::- *intervalo de tiempo* del día &#124; intervalo de *tiempo*  
  
 *intervalo de tiempo de día* ::- *días-valor* [*horas-valor* [:*minutos-valor*[:*segundo-valor*]]]  
  
 *intervalo de tiempo* ::- *valor de horas* [:*minutos-valor* [:*segundo-valor* ] ]  
  
 &#124; *minutos-valor* [:*segundo-valor* ]  
  
 &#124; *segundos de valor*  
  
 *valor de años* *datetime-value* ::  
  
 *valor de meses* :: *datetime-value*  
  
 *días-valor* ::- *datetime-value*  
  
 *horas-valor* ::- *datetime-value*  
  
 *valores de minutos* *datetime-value* ::  
  
 *segundo-valor* *::-segundos-valor entero* [.[ *segundos-fracción*] ]  
  
 *segundos-valor entero* ::- *unsigned-integer*  
  
 *fracción de segundos* :: *unsigned-integer*  
  
 *valor de fecha* y *unsigned-integer* hora ::  
  
 *intervalo-calificador* ::- *campo de inicio* PARA el campo *final* &#124; campo de *fecha única*  
  
 *start-field* ::- *non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *campo final* ::- *campo no-segundo-fecha-hora-campo* &#124; SECOND[(*interval-fractional-seconds-precision*)]  
  
 *campo de fecha* única::- *campo no-segundo-fecha-hora* [(*interval-leading-field-precision*)] &#124; SECOND[(*interval-leading-field-precision* [, (*interval-fractional-seconds-precision*)]  
  
 *campo datetime ::-* campo que no es *de segundo-segundo-fecha-campo* &#124; SEGUNDO  
  
 campo de *no-segundo-fecha-hora* ::-Año &#124; MES &#124; DIA &#124; HORA &#124; MINUTO  
  
 *interval-fractional-seconds-precision* ::- *unsigned-integer*  
  
 *interval-leading-field-precision* ::- *unsigned-integer*  
  
 *cita* ::' '  
  
 *unsigned-integer* ::- *digit...*
