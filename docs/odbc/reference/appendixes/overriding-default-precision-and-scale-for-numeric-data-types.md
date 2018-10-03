---
title: Invalidar la precisión y escala predeterminadas de tipos de datos numéricos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f071cf4391c760f7d269382537c3cd4f2b758c3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772073"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Invalidar la precisión y escala predeterminadas de tipos de datos numéricos
Cuando se establece el campo SQL_DESC_TYPE de una descartar a SQL_C_NUMERIC, llamando **SQLBindCol** o **SQLSetDescField**, el campo SQL_DESC_SCALE en el descartar se establece en 0 y se establece el campo SQL_DESC_PRECISION con una precisión definidos por el controlador predeterminado. Esto también es cierto cuando se establece el campo SQL_DESC_TYPE en un APD a SQL_C_NUMERIC, llamando **SQLBindParameter** o **SQLSetDescField**. Esto es cierto para los parámetros de salida, entrada/salida o entrada.  
  
 Si anteriormente cualquiera de los valores predeterminados descritos no son aceptable para una aplicación, la aplicación debe establecer el campo SQL_DESC_SCALE o SQL_DESC_PRECISION mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Si la aplicación llama a **SQLGetData** para devolver datos en una estructura SQL_C_NUMERIC, se usan los campos predeterminados SQL_DESC_SCALE y SQL_DESC_PRECISION. Si los valores predeterminados no son aceptables, la aplicación debe llamar a **SQLSetDescRec** o **SQLSetDescField** para establecer los campos y, a continuación, llame a **SQLGetData** con un *TargetType* de SQL_ARD_TYPE para usar los valores en los campos de descriptor.  
  
 Cuando **SQLPutData** es llama, la llamada usa los campos SQL_DESC_SCALE y SQL_DESC_PRECISION del registro de descriptor que se corresponde con el parámetro de datos en ejecución o una columna, que son campos APD para las llamadas a  **SQLExecute** o **SQLExecDirect**, o los campos de Descartar para las llamadas a **SQLBulkOperations** o **SQLSetPos**.
