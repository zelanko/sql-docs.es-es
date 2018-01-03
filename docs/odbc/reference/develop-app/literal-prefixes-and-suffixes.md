---
title: Literales prefijos y sufijos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbc8e513c33f6b924175719008bb7d97ce39af69
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="literal-prefixes-and-suffixes"></a>Literales prefijos y sufijos
En una instrucción SQL, un *literal* es una representación de caracteres de un valor de datos real. Por ejemplo, en la siguiente instrucción, ABC, FFFF y 10 son literales:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Literales para algunos tipos de datos requieren especial prefijos y sufijos. En el ejemplo anterior, el literal de carácter (ABC) requiere una comilla simple (') como prefijo y un sufijo, el literal binario (FFFF) requiere que los caracteres 0 x como prefijo y el literal entero (10) no requieren un prefijo o sufijo.  
  
 Para todos los tipos de datos excepto la fecha, hora y las marcas de tiempo, aplicaciones interoperables deben utilizar los valores devueltos de las columnas de caracteres LITERAL_PREFIX y LITERAL_SUFFIX en el conjunto de resultados creados por **SQLGetTypeInfo**. Para fecha, hora, marca de tiempo y literales de intervalo de fecha y hora, aplicaciones interoperables deben usar las secuencias de escape que se describe en la sección anterior.
