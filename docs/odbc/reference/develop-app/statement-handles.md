---
title: Manijas de la declaración ( Statement Handles) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be90fe10d10a0b087d1c9724fed249805eb4dba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299681"
---
# <a name="statement-handles"></a>Identificadores de instrucciones
Una *instrucción* se considera más fácilmente como una instrucción SQL, como **SELECT \* FROM Employee**. Sin embargo, una instrucción es algo más que una instrucción SQL: consta de toda la información asociada a esa instrucción SQL, como los conjuntos de resultados creados por la instrucción y los parámetros utilizados en la ejecución de la instrucción. Una instrucción ni siquiera necesita tener una instrucción SQL definida por la aplicación. Por ejemplo, cuando se ejecuta una función de catálogo como **SQLTables** en una instrucción, ejecuta una instrucción SQL predefinida que devuelve una lista de nombres de tabla.  
  
 Cada instrucción se identifica mediante un identificador de instrucción. Una instrucción está asociada a una sola conexión y puede haber varias instrucciones en esa conexión. Algunos controladores limitan el número de instrucciones activas que admiten; la opción SQL_MAX_CONCURRENT_ACTIVITIES de **SQLGetInfo** especifica cuántas instrucciones activas admite un controlador en una sola conexión. Se define una instrucción para que esté *activa* si tiene resultados pendientes, donde los resultados son un conjunto de resultados o el recuento de filas afectadas por una instrucción **INSERT**, **UPDATE**o **DELETE,** o se envían datos con varias llamadas a **SQLPutData**.  
  
 Dentro de un fragmento de código que implementa ODBC (el Administrador de controladores o un controlador), el identificador de instrucción identifica una estructura que contiene información de instrucción, como:  
  
-   El estado de la declaración  
  
-   El diagnóstico actual a nivel de declaración  
  
-   Las direcciones de las variables de aplicación enlazadas a los parámetros de la instrucción y las columnas del conjunto de resultados  
  
-   La configuración actual de cada atributo de instrucción  
  
 Los identificadores de instrucción se utilizan en la mayoría de las funciones ODBC. En particular, se utilizan en las funciones para enlazar parámetros y columnas de conjunto de resultados (**SQLBindParameter** y **SQLBindCol**), preparar y ejecutar instrucciones (**SQLPrepare**, **SQLExecute**y **SQLExecDirect**), recuperar metadatos (**SQLColAttribute** y **SQLDescribeCol**), recuperar resultados (**SQLFetch**) y recuperar diagnósticos (**SQLGetDiagField** y **SQLGetDiagRec**). También se utilizan en funciones de catálogo (**SQLColumns**, **SQLTables**, etc.) y un número de otras funciones.  
  
 Los identificadores de instrucción se asignan con **SQLAllocHandle** y se liberan con **SQLFreeHandle**.
