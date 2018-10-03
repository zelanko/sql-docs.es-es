---
title: Las restricciones del calendario gregoriano | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 30fbdd17e7ec5eb970948e1c7133020081222614
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847933"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Restricciones del calendario gregoriano
Tipos de datos de fecha y la fecha y hora y los campos al final de intervalo de tipos de datos, deben cumplir las restricciones del calendario gregoriano. Estas restricciones son los siguientes:  
  
-   El valor del campo de mes debe ser entre 1 y 12, ambos inclusive.  
  
-   El valor del campo de días debe ser en el intervalo comprendido entre 1 y el número de días del mes. El número de días del mes se determina a partir de los valores de los campos de años y meses y puede ser 28, 29, 30 o 31. (El número de días del mes también puede depender de si es un año bisiesto).  
  
-   El valor del campo de hora debe ser entre 0 y 23, ambos inclusive.  
  
-   El valor del campo minutos debe ser entre 0 y 59, ambos inclusive.  
  
-   Para el campo de segundos al final de los tipos de datos de intervalo, el valor del campo de segundos debe estar entre 0 y 59.9 (*n*), ambos inclusive, donde *n* es el número de dígitos en la precisión de fracciones de segundo.  
  
-   Para el campo de segundos al final de los tipos de datos de fecha y hora, el valor del campo de segundos debe estar entre 0 y 61,9 (*n*), ambos inclusive, donde *n* especifica el número de dígitos "9" y el valor de *n*  es la precisión de fracciones de segundo. (El intervalo de segundos permite como máximo dos segundos intercalares mantener la sincronización de hora sidereal).
