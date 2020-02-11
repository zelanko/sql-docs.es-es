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
ms.openlocfilehash: 730ead7bf90af3b6e6906fe184e0fa3312212137
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107258"
---
# <a name="statement-handles"></a>Identificadores de instrucciones
Una *instrucción* se considera más fácil como una instrucción SQL, como **SELECT \* from Employee**. Sin embargo, una instrucción es algo más que una instrucción SQL, que consta de toda la información asociada a esa instrucción SQL, como los conjuntos de resultados creados por la instrucción y los parámetros utilizados en la ejecución de la instrucción. Una instrucción no necesita incluso una instrucción SQL definida por la aplicación. Por ejemplo, cuando se ejecuta una función de catálogo como **SQLTables** en una instrucción, se ejecuta una instrucción SQL predefinida que devuelve una lista de nombres de tabla.  
  
 Cada instrucción se identifica mediante un identificador de instrucción. Una instrucción está asociada a una sola conexión y puede haber varias instrucciones en esa conexión. Algunos controladores limitan el número de instrucciones activas que admiten; la opción SQL_MAX_CONCURRENT_ACTIVITIES de **SQLGetInfo** especifica el número de instrucciones activas que admite un controlador en una sola conexión. Una instrucción se define como *activa* si tiene resultados pendientes, donde los resultados son un conjunto de resultados o el recuento de filas afectadas por una instrucción **Insert**, **Update**o **Delete** , o bien se envían datos con varias llamadas a **SQLPutData**.  
  
 Dentro de un fragmento de código que implementa ODBC (el administrador de controladores o un controlador), el identificador de instrucción identifica una estructura que contiene información de la instrucción, como:  
  
-   Estado de la instrucción  
  
-   Diagnósticos de nivel de instrucción actual  
  
-   Direcciones de las variables de aplicación enlazadas a las columnas de los parámetros y del conjunto de resultados de la instrucción  
  
-   La configuración actual de cada atributo de instrucción  
  
 Los identificadores de instrucción se utilizan en la mayoría de las funciones ODBC. En particular, se usan en las funciones para enlazar parámetros y columnas del conjunto de resultados (**SQLBindParameter** y **SQLBindCol**), preparar y ejecutar instrucciones (**SQLPrepare**, **SQLExecute**y **SQLExecDirect**), recuperar metadatos (**SQLColAttribute** y **SQLDescribeCol**), capturar resultados (**SQLFetch**) y recuperar diagnósticos (**SQLGetDiagField** y **SQLGetDiagRec**). También se usan en las funciones de catálogo (**SQLColumns**, **SQLTables**, etc.) y varias funciones.  
  
 Los identificadores de instrucción se asignan con **SQLAllocHandle** y se liberan con **SQLFreeHandle**.
