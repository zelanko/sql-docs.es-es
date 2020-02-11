---
title: Restricciones del calendario gregoriano | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f67d313f5a1261dba1f88e9ef3a70d30c1cd503
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019177"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Restricciones del calendario gregoriano
Los tipos de datos Date y DateTime, y los campos finales de tipos de datos de intervalo, deben cumplir las restricciones del calendario gregoriano. Estas restricciones son las siguientes:  
  
-   El valor del campo month debe estar entre 1 y 12, ambos inclusive.  
  
-   El valor del campo Day debe estar en el intervalo comprendido entre 1 y el número de días del mes. El número de días del mes se determina a partir de los valores de los campos Year y months y puede ser 28, 29, 30 o 31. (El número de días del mes también puede depender de si se trata de un año bisiesto).  
  
-   El valor del campo hour debe estar entre 0 y 23, ambos incluidos.  
  
-   El valor del campo minute debe estar comprendido entre 0 y 59, ambos incluidos.  
  
-   En el caso del campo de segundos final de los tipos de datos de intervalo, el valor del campo de segundos debe estar entre 0 y 59,9 (*n*), ambos inclusive, donde *n* es el número de dígitos de la precisión de fracciones de segundo.  
  
-   En el caso de los segundos de los tipos de datos datetime finales, el valor del campo de segundos debe estar entre 0 y 61,9 (*n*), ambos inclusive, donde *n* especifica el número de dígitos "9" y el valor de *n* es la precisión de fracciones de segundo. (El intervalo de segundos permite un máximo de dos segundos bisiestos para mantener la sincronización de la hora de Sidereal).
