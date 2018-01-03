---
title: Identificadores de instrucciones | Documentos de Microsoft
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
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d80db9c7ce795514dd362e37170aa58cce817c5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="statement-handles"></a>Identificadores de instrucciones
A *instrucción* es más fácil pensar de como una instrucción SQL, como **seleccione \* de empleados**. Sin embargo, una instrucción es algo más que una instrucción SQL, consta de toda la información asociada a esa instrucción SQL, como los conjuntos de resultados creados por la instrucción y los parámetros utilizados en la ejecución de la instrucción. Una instrucción no es necesario tener una instrucción SQL definida por la aplicación. Por ejemplo, cuando una función de catálogo como **SQLTables** se ejecuta en una instrucción, se ejecuta una instrucción SQL predefinida que devuelve una lista de nombres de tabla.  
  
 Cada instrucción se identifica mediante un identificador de instrucción. Una instrucción está asociada a una sola conexión, y puede haber varias instrucciones en esa conexión. Algunos controladores de limitan el número de instrucciones activas que admiten; opción el SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo** especifica cuántas instrucciones activas es compatible con un controlador en una sola conexión. Una instrucción se define como *active* si tiene resultados pendientes, donde resultados son un conjunto de resultados o el número de filas afectadas por un **insertar**, **actualización**, o **Eliminar** instrucción o los datos se están enviando con varias llamadas a **SQLPutData**.  
  
 Dentro de un fragmento de código que implementa ODBC (el Administrador de controladores o un controlador), el identificador de instrucción identifica una estructura que contiene información de la instrucción, como:  
  
-   Estado de la instrucción  
  
-   Los diagnósticos de nivel de instrucción actuales  
  
-   Las direcciones de las variables de aplicación enlazadas a los parámetros de la instrucción y dar lugar a columnas del conjunto de  
  
-   La configuración actual de cada atributo de instrucción  
  
 Identificadores de instrucciones se utilizan en la mayoría de las funciones ODBC. En concreto, se utilizan en las funciones para enlazar parámetros y columnas del conjunto de resultados (**SQLBindParameter** y **SQLBindCol**), preparar y ejecutar instrucciones (**SQLPrepare** **SQLExecute**, y **SQLExecDirect**), recuperar los metadatos (**SQLColAttribute** y **SQLDescribeCol**), fetch resultados (**SQLFetch**) y recuperar diagnósticos (**SQLGetDiagField** y **SQLGetDiagRec**). También se usan en las funciones de catálogo (**SQLColumns**, **SQLTables**, etc.) y un número de otras funciones.  
  
 Se asignan a identificadores de instrucciones **SQLAllocHandle** y liberado con **SQLFreeHandle**.
