---
title: Restricciones del Calendario Gregoriano ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f88842c7426e17af1fdc0533b8b97e2c559de237
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284765"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Restricciones del calendario gregoriano
Los tipos de datos date y datetime y los campos finales de los tipos de datos de intervalo deben ajustarse a las restricciones del calendario gregoriano. Estas restricciones son las siguientes:  
  
-   El valor del campo de mes debe estar entre 1 y 12, ambos inclusive.  
  
-   El valor del campo de día debe estar en el intervalo de 1 al número de días del mes. El número de días del mes se determina a partir de los valores de los campos de año y mes y puede ser 28, 29, 30 o 31. (El número de días en el mes también puede depender de si es un año bisiesto.)  
  
-   El valor del campo de hora debe estar entre 0 y 23, ambos inclusive.  
  
-   El valor del campo de minutos debe estar entre 0 y 59, ambos inclusive.  
  
-   Para el campo de segundos finales de tipos de datos de intervalo, el valor del campo de segundos debe estar entre 0 y 59.9(*n*), ambos inclusive, donde *n* es el número de dígitos en la precisión de fracciones de segundo.  
  
-   Para el campo de segundos finales de tipos de datos datetime, el valor del campo seconds debe estar entre 0 y 61.9(*n*), ambos inclusive, donde *n* especifica el número de dígitos "9" y el valor de *n* es la precisión de fracciones de segundo. (El intervalo de segundos permite que hasta dos segundos bisiestos mantengan la sincronización del tiempo sideral.)
