---
title: Las matrices de valores de parámetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e65928cd078a3f05032f4e4fb400e3e2eb1f27a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077071"
---
# <a name="arrays-of-parameter-values"></a>Matrices de valores de parámetro
A menudo resulta útil para las aplicaciones pasar matrices de parámetros. Por ejemplo, con las matrices de parámetros y un parametrizada **insertar** instrucción, una aplicación puede insertar un número de filas a la vez. Hay varias ventajas al uso de matrices. En primer lugar, se reduce el tráfico de red porque los datos para muchas de las instrucciones se envían en un único paquete (si el origen de datos admite matrices de parámetros de forma nativa). En segundo lugar, algunos orígenes de datos pueden ejecutar instrucciones SQL mediante matrices con más rapidez que ejecutar el mismo número de instrucciones SQL independientes. Por último, cuando los datos se almacenan en una matriz, como suele ser el caso de los datos de la pantalla, la aplicación puede enlazar todas las filas de una columna en particular con una sola llamada a **SQLBindParameter** y actualizarlas mediante la ejecución de una sola instrucción.  
  
 Por desgracia, no muchos orígenes de datos admiten las matrices de parámetros. Sin embargo, un controlador puede emular las matrices de parámetros mediante la ejecución de una instrucción SQL una vez para cada conjunto de valores de parámetro. Esto puede provocar un aumento en velocidad porque el controlador, a continuación, puede preparar la instrucción que va a ejecutar una vez para cada conjunto de parámetros. También puede provocar al código de aplicación más sencillo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Las matrices de parámetros de enlace](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Utilizar matrices de parámetros](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
