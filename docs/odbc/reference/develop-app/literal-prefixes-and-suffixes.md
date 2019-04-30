---
title: Literales prefijos y sufijos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4eabc3e0c354e02ad8df790d896dc43ae49c9bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313008"
---
# <a name="literal-prefixes-and-suffixes"></a>Literales prefijos y sufijos
En una instrucción SQL, un *literal* es una representación de caracteres de un valor de datos real. Por ejemplo, en la siguiente instrucción, ABC, FFFF y 10 son literales:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Literales para algunos tipos de datos requieren especiales prefijos y sufijos. En el ejemplo anterior, el literal de carácter (ABC) requiere una comilla simple (') como prefijo y sufijo, el literal binario (FFFF) requiere que los caracteres 0 x como prefijo y el literal entero (10) no requieren un prefijo o sufijo.  
  
 Para todos los tipos de datos, excepto la fecha, hora y las marcas de tiempo, las aplicaciones interoperables deben usar los valores devueltos en las columnas de caracteres LITERAL_PREFIX y LITERAL_SUFFIX en el conjunto de resultados creados por **SQLGetTypeInfo**. Por fecha, hora, marca de tiempo y los literales de intervalo de fecha y hora, aplicaciones interoperables deben utilizar las secuencias de escape que se describen en la sección anterior.
