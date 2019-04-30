---
title: Identificadores de instrucciones | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f249bb13ece6382e96dfe953b1d3c1d96c7bf65
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149003"
---
# <a name="statement-handles"></a>Identificadores de instrucciones
Un *instrucción* es más fácil pensar de como una instrucción SQL, tales como **seleccione \* de empleado**. Sin embargo, una instrucción es algo más que una instrucción SQL, consta de toda la información asociada con esa instrucción SQL, como los conjuntos de resultados creados por la instrucción y los parámetros utilizados en la ejecución de la instrucción. Una instrucción no es necesario tener una instrucción SQL definido por la aplicación. Por ejemplo, cuando una función de catálogo como **SQLTables** se ejecuta en una instrucción, se ejecuta una instrucción SQL predefinida que devuelve una lista de nombres de tabla.  
  
 Cada instrucción se identifica mediante un identificador de instrucción. Una instrucción está asociada con una sola conexión, y puede haber varias instrucciones en esa conexión. Algunos controladores de limitan el número de instrucciones activas que admiten; opción el SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo** especifica cuántas instrucciones activas que admite un controlador en una sola conexión. Una instrucción se define como *active* si tiene resultados pendientes, donde los resultados son un conjunto de resultados o el recuento de filas afectadas por una **insertar**, **actualización**, o **Eliminar** instrucción o datos que se envían con varias llamadas a **SQLPutData**.  
  
 Dentro de un fragmento de código que implementa ODBC (el Administrador de controladores o un controlador), el identificador de instrucción identifica una estructura que contiene información de la instrucción, como:  
  
-   Estado de la instrucción  
  
-   Los diagnósticos de nivel de instrucción actuales  
  
-   Las direcciones de las variables de aplicación enlazada a los parámetros de la instrucción y dar lugar a las columnas del conjunto  
  
-   La configuración actual de cada atributo de instrucción  
  
 Identificadores de instrucciones se usan en la mayoría de las funciones ODBC. En concreto, se usan en las funciones para enlazar parámetros y columnas del conjunto de resultados (**SQLBindParameter** y **SQLBindCol**), preparar y ejecutar instrucciones (**SQLPrepare** **SQLExecute**, y **SQLExecDirect**), recuperar los metadatos (**SQLColAttribute** y **SQLDescribeCol**), fetch los resultados (**SQLFetch**) y recuperar diagnósticos (**SQLGetDiagField** y **SQLGetDiagRec**). También se usan las funciones de catálogo (**SQLColumns**, **SQLTables**, etc.) y un número de otras funciones.  
  
 Se asignan a identificadores de instrucciones **SQLAllocHandle** y liberado con **SQLFreeHandle**.
