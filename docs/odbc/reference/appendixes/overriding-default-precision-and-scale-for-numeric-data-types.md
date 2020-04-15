---
title: Reemplazar la precisión y la escala predeterminadas para los tipos de datos numéricos Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365c5f69d21dd3a4ad8e89805d81f1b3b0c9dcba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303596"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Invalidar la precisión y escala predeterminadas de tipos de datos numéricos
Cuando el campo SQL_DESC_TYPE de un ARD se establece en SQL_C_NUMERIC, llamando a **SQLBindCol** o **SQLSetDescField**, el campo SQL_DESC_SCALE de ARD se establece en 0 y el campo SQL_DESC_PRECISION se establece en una precisión predeterminada definida por el controlador. Esto también es cierto cuando el campo SQL_DESC_TYPE de un APD se establece en SQL_C_NUMERIC, llamando a **SQLBindParameter** o **SQLSetDescField**. Esto es cierto para los parámetros de entrada, entrada/salida o salida.  
  
 Si cualquiera de los valores predeterminados descritos anteriormente no es aceptable para una aplicación, la aplicación debe establecer el campo SQL_DESC_SCALE o SQL_DESC_PRECISION llamando a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Si la aplicación llama a **SQLGetData** para devolver datos a una estructura de SQL_C_NUMERIC, se usan los campos predeterminados SQL_DESC_SCALE y SQL_DESC_PRECISION. Si los valores predeterminados no son aceptables, la aplicación debe llamar a **SQLSetDescRec** o **SQLSetDescField** para establecer los campos y, a continuación, llamar a **SQLGetData** con un *TargetType* de SQL_ARD_TYPE usar los valores de los campos descriptores.  
  
 Cuando se llama a **SQLPutData,** la llamada utiliza los campos SQL_DESC_SCALE y SQL_DESC_PRECISION del registro descriptor que corresponde al parámetro o columna de datos en ejecución, que son campos APD para llamadas a **SQLExecute** o **SQLExecDirect**, o campos ARD para llamadas a **SQLBulkOperations** o **SQLSetPos**.
