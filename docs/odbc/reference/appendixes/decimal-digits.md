---
title: Dígitos decimales ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4921a6162b6d711e657f223b5be5783dfa37bca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285165"
---
# <a name="decimal-digits"></a>Dígitos decimales
Los *dígitos decimales* de los tipos de datos decimales y numéricos se definen como el número máximo de dígitos a la derecha del punto decimal o la escala de los datos. Para las columnas o parámetros de número de punto flotante aproximados, la escala no está definida porque el número de dígitos a la derecha del punto decimal no es fijo. Para los datos de fecha y hora o intervalo que contienen un componente de segundos, los dígitos decimales se definen como el número de dígitos a la derecha del punto decimal en el componente de segundos de los datos.  
  
 Para los tipos de datos SQL_DECIMAL y SQL_NUMERIC, la escala máxima suele ser la misma que la precisión máxima. Sin embargo, algunos orígenes de datos imponen un límite independiente a la escala máxima. Para determinar las escalas mínima y máxima permitidas para un tipo de datos, una aplicación llama a **SQLGetTypeInfo**.  
  
 Los dígitos decimales definidos para cada tipo de datos SQL conciso se muestran en la tabla siguiente.  
  
|Tipo SQL|Dígitos decimales|  
|--------------|--------------------|  
|Todos los tipos binarios y de caracteres[a]|N/D|  
|SQL_DECIMAL<br />SQL_NUMERIC|El número definido de dígitos a la derecha del punto decimal. Por ejemplo, la escala de una columna definida como NUMERIC(10,3) es 3. Esto puede ser un número negativo para admitir el almacenamiento de números muy grandes sin usar notación exponencial; por ejemplo, "12000" podría almacenarse como "12" con una escala de -3.|  
|Todos los tipos numéricos exactos que no sean SQL_DECIMAL y SQL_NUMERIC[a]|0|  
|Todos los tipos de datos aproximados[a]|N/D|  
|SQL_TYPE_DATE y todos los tipos de intervalos sin componente de segundos[a]|N/D|  
|Todos los tipos datetime excepto SQL_TYPE_DATE y todos los tipos de intervalo con un componente seconds|El número de dígitos a la derecha del punto decimal en la parte de segundos del valor (segundos fraccionarios). Este número no puede ser negativo.|  
|SQL_GUID|N/D|  
  
 [a] El *DecimalDigits* argumento de **SQLBindParameter** se omite para este tipo de datos.  
  
 Los valores devueltos para los dígitos decimales no corresponden a los valores de ningún campo descriptor. Los valores pueden provenir del campo SQL_DESC_SCALE o SQL_DESC_PRECISION, según el tipo de datos, como se muestra en la tabla siguiente.  
  
|Tipo SQL|Campo descriptor correspondiente a<br /><br /> dígitos decimales|  
|--------------|----------------------------------------------------------|  
|Todos los tipos de caracteres y binarios|N/D|  
|Todos los tipos numéricos exactos|SCALE|  
|SQL_BIT|N/D|  
|Todos los tipos numéricos aproximados|N/D|  
|Todos los tipos de fecha y hora|PRECISION|  
|Todos los tipos de intervalo con un componente de segundos|PRECISION|  
|Todos los tipos de intervalos sin componente de segundos|N/D|
