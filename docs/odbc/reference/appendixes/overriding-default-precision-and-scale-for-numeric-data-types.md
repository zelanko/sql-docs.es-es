---
description: Invalidar la precisión y escala predeterminadas de tipos de datos numéricos
title: Reemplazar la precisión y la escala predeterminadas para tipos de datos numéricos | Microsoft Docs
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
ms.openlocfilehash: 798e607ff6584bde27791a29e4b20aeb1d7bb3cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466087"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>Invalidar la precisión y escala predeterminadas de tipos de datos numéricos
Cuando el campo de SQL_DESC_TYPE de una ARD se establece en SQL_C_NUMERIC, llamando a **SQLBindCol** o **SQLSetDescField**, el campo de SQL_DESC_SCALE de ARD se establece en 0 y el campo de SQL_DESC_PRECISION se establece en una precisión predeterminada definida por el controlador. Esto también se aplica cuando el campo SQL_DESC_TYPE de una APD se establece en SQL_C_NUMERIC, llamando a **SQLBindParameter** o **SQLSetDescField**. Esto se aplica a los parámetros de entrada, de entrada/salida o de salida.  
  
 Si alguno de los valores predeterminados descritos anteriormente no es aceptable para una aplicación, la aplicación debe establecer el SQL_DESC_SCALE o SQL_DESC_PRECISION campo mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Si la aplicación llama a **SQLGetData** para devolver datos a una estructura de SQL_C_NUMERIC, se usan los campos predeterminados SQL_DESC_SCALE y SQL_DESC_PRECISION. Si los valores predeterminados no son aceptables, la aplicación debe llamar a **SQLSetDescRec** o **SQLSetDescField** para establecer los campos y, a continuación, llamar a **SQLGetData** con un *TargetType* de SQL_ARD_TYPE para usar los valores de los campos de descriptor.  
  
 Cuando se llama a **SQLPutData** , la llamada utiliza los campos SQL_DESC_SCALE y SQL_DESC_PRECISION del registro del descriptor que corresponde al parámetro o la columna de datos en ejecución, que son campos de APD para las llamadas a los campos **SQLExecute** o **SQLExecDirect**, o ARD para las llamadas a **SQLBulkOperations** o **SQLSetPos**.
