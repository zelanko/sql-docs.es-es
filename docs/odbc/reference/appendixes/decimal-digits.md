---
title: Dígitos decimales | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7b9a69941364b32e6b43d79f2d092511fd61f22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241000"
---
# <a name="decimal-digits"></a>Dígitos decimales
El *dígitos decimales* de datos decimal y numeric tipos se define como el número máximo de dígitos a la derecha del separador decimal, o la escala de los datos. Columnas de número de punto flotante aproximadas o los parámetros, la escala está definida porque el número de dígitos a la derecha del separador decimal no es fijo. Para los datos de fecha y hora o el intervalo que contiene un componente de segundos, los dígitos decimales se define como el número de dígitos a la derecha del separador decimal en el componente de segundos de los datos.  
  
 Para los tipos de datos SQL_DECIMAL y SQL_NUMERIC, la escala máxima suele ser el mismo que la precisión máxima. Sin embargo, algunos orígenes de datos imponen un límite independiente en la escala máxima. Para determinar las escalas mínimas y máxima permitidas para un tipo de datos, una aplicación llama a **SQLGetTypeInfo**.  
  
 Los dígitos decimales definidos para cada tipo de datos SQL concisa se muestra en la tabla siguiente.  
  
|Tipo SQL|Dígitos decimales|  
|--------------|--------------------|  
|Todos los tipos de caracteres y binarios [a]|n/d|  
|SQL_DECIMAL<br />SQL_NUMERIC|El número definido de dígitos a la derecha del separador decimal. Por ejemplo, la escala de una columna definida como NUMERIC(10,3) es 3. Esto puede ser un número negativo para admitir el almacenamiento de números muy grandes sin utilizar la notación exponencial; Por ejemplo, "12000" se pueden almacenar como "12" con una escala de -3.|  
|Todos los tipos numéricos exactos que no sean SQL_DECIMAL y SQL_NUMERIC [a]|0|  
|Todos los tipos de datos aproximados [a]|n/d|  
|SQL_TYPE_DATE y todos los tipos de intervalo con ningún componente de segundos [a]|n/d|  
|Todos los tipos de fecha y hora, excepto SQL_TYPE_DATE y todos los tipos de intervalo con un componente de segundos|El número de dígitos a la derecha del separador decimal en la parte de segundos del valor (fracciones de segundo). Este número no puede ser negativo.|  
|SQL_GUID|n/d|  
  
 [a] la *ColumnSize* argumento de **SQLBindParameter** se omite para este tipo de datos.  
  
 Los valores devueltos para los dígitos decimales no corresponden a los valores de cualquier campo descriptor uno. Los valores pueden proceder de la SQL_DESC_SCALE o el campo SQL_DESC_PRECISION, según el tipo de datos, como se muestra en la tabla siguiente.  
  
|Tipo SQL|Campo descriptor corresponde a<br /><br /> Dígitos decimales|  
|--------------|----------------------------------------------------------|  
|Todos los tipos de caracteres y binarios|n/d|  
|Todos los tipos numéricos exactos|SCALE|  
|SQL_BIT|n/d|  
|Todos los tipos numéricos aproximados|n/d|  
|Todos los tipos de fecha y hora|PRECISION|  
|Todos los tipos de intervalo con un componente de segundos|PRECISION|  
|Todos los tipos de intervalo con ningún componente de segundos|n/d|
