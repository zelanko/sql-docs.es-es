---
title: "Dígitos decimales | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1bb5222837dab705701e4a137c00f3b10867ae2a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="decimal-digits"></a>Dígitos decimales
El *dígitos decimales* de datos decimal y numeric tipos se define como el número máximo de dígitos a la derecha del separador decimal o la escala de los datos. Para columnas de número de punto flotante aproximadas o los parámetros, la escala no está definida porque el número de dígitos a la derecha del separador decimal no es fijo. Para los datos de fecha y hora o intervalo que contiene un componente de segundos, los dígitos decimales se define como el número de dígitos a la derecha del separador decimal en el componente de segundos de los datos.  
  
 Para los tipos de datos SQL_DECIMAL de ODBC y SQL_NUMERIC, la escala máxima es normalmente el mismo que la precisión máxima. Sin embargo, algunos orígenes de datos imponen un límite independiente en la escala máxima. Para determinar las escalas mínimas y máxima permitidas para un tipo de datos, una aplicación llama **SQLGetTypeInfo**.  
  
 Los dígitos decimales que se define para cada tipo de datos SQL concisa se muestra en la tabla siguiente.  
  
|Tipo SQL|dígitos decimales|  
|--------------|--------------------|  
|Todos los tipos de caracteres y binarios [a]|n/d|  
|SQL_DECIMAL<br />SQL_NUMERIC|El número definido de dígitos a la derecha del separador decimal. Por ejemplo, la escala de una columna definida como NUMERIC(10,3) es 3. Esto puede ser un número negativo para admitir el almacenamiento de números muy grandes sin utilizar la notación exponencial; Por ejemplo, "12000" se puede almacenar como "12" con una escala de -3.|  
|Todos los tipos numéricos exactos que no sean SQL_DECIMAL de ODBC y SQL_NUMERIC [a]|0|  
|Todos los tipos de datos aproximados [a]|n/d|  
|SQL_TYPE_DATE y todos los tipos de intervalo con ningún componente de segundos [a]|n/d|  
|Todos los tipos de fecha y hora excepto SQL_TYPE_DATE y todos los tipos de intervalo con un componente de segundos|El número de dígitos a la derecha del separador decimal en la segunda parte del valor (fracciones de segundo). Este número no puede ser negativo.|  
|SQL_GUID|n/d|  
  
 [a] la *ColumnSize* argumento de **SQLBindParameter** se omite para este tipo de datos.  
  
 Los valores devueltos para los dígitos decimales no corresponden a los valores en cualquier un campo descriptor. Los valores pueden proceder de la SQL_DESC_SCALE o el campo SQL_DESC_PRECISION, dependiendo del tipo de datos, como se muestra en la tabla siguiente.  
  
|Tipo SQL|Campo descriptor corresponde a<br /><br /> dígitos decimales|  
|--------------|----------------------------------------------------------|  
|Todos los tipos de caracteres y binarios|n/d|  
|Todos los tipos numéricos exactos|SCALE|  
|SQL_BIT|n/d|  
|Todos los tipos numéricos aproximados|n/d|  
|Todos los tipos de fecha y hora|PRECISION|  
|Todos los tipos de intervalo con un componente de segundos|PRECISION|  
|Todos los tipos de intervalo con ningún componente de segundos|n/d|
