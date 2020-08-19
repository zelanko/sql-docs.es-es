---
description: Literales prefijos y sufijos
title: Prefijos y sufijos literales | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0f658c401bfc31e69a6e5e2fc5110bc9a809f345
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424617"
---
# <a name="literal-prefixes-and-suffixes"></a>Literales prefijos y sufijos
En una instrucción SQL, un *literal* es una representación de caracteres de un valor de datos real. Por ejemplo, en la siguiente instrucción, ABC, FFFF y 10 son literales:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Los literales de algunos tipos de datos requieren prefijos y sufijos especiales. En el ejemplo anterior, el literal de carácter (ABC) requiere una comilla simple (') como prefijo y sufijo, el literal binario (FFFF) requiere los caracteres 0x como prefijo y el literal entero (10) no requiere un prefijo o sufijo.  
  
 En el caso de todos los tipos de datos, excepto la fecha, la hora y las marcas de tiempo, las aplicaciones interoperables deben usar los valores devueltos en las columnas LITERAL_PREFIX y LITERAL_SUFFIX en el conjunto de resultados creado por **SQLGetTypeInfo**. En el caso de los literales de fecha, hora, marca de tiempo y intervalo de DateTime, las aplicaciones interoperables deben usar las secuencias de escape descritas en la sección anterior.
