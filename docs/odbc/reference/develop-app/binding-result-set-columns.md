---
title: Columnas del conjunto de resultados de enlace | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: becda51a0fac924fce31e6cb15331321990d8a42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135003"
---
# <a name="binding-result-set-columns"></a>Columnas del conjunto de resultados de enlace
Las aplicaciones pueden enlazar como muchos o tan pocos columnas del conjunto de resultados como que elijan, incluidos el enlace en absoluto ninguna columna. Cuando se captura una fila de datos, el controlador devuelve los datos de las columnas enlazadas a la aplicación. Si la aplicación enlaza todas las columnas del conjunto de resultados depende de la aplicación. Por ejemplo, las aplicaciones que generan los informes suelen tengan un formato fijo; Estas aplicaciones creación un conjunto de resultados que contiene todas las columnas utilizadas en el informe y, a continuación, enlazar y recuperarán los datos de todas estas columnas. Aplicaciones que se muestran a veces pantallas completas de los datos permiten al usuario decidir qué columnas desea mostrar; Estas aplicaciones crean un conjunto que contiene todas las columnas, es posible que desee, pero enlazar y recuperar los datos solo para las columnas elegidas por el usuario de resultados.  
  
 Se pueden recuperar datos de las columnas sin enlazar mediante una llamada a **SQLGetData**. Esto se denomina habitualmente para recuperar datos largos, lo que a menudo supera la longitud de un solo búfer y se deben recuperar en partes.  
  
 Las columnas pueden estar limitadas en cualquier momento, incluso después de que las filas se han capturado. Sin embargo, los nuevos enlaces no surtirán efecto hasta la próxima vez que se captura una fila; no se aplican a los datos de filas recuperadas ya.  
  
 Una variable estando enlazada a una columna hasta que se enlaza una variable diferente a la columna, hasta que la columna se han desenlazado mediante una llamada a **SQLBindCol** con un puntero nulo como dirección de la variable, hasta que todas las columnas se han desenlazado mediante una llamada a **SQLFreeStmt** con la opción SQL_UNBIND, o hasta que se libere la instrucción. Por este motivo, la aplicación debe asegurarse de que todas las variables enlazadas sigan siendo válidas mientras están enlazados. Para obtener más información, consulte [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Dado que los enlaces de columna son simplemente información asociada con la estructura del informe, se puede establecer en cualquier orden. También son independientes del conjunto de resultados. Por ejemplo, suponga que una aplicación enlaza las columnas del conjunto de resultados generado por la instrucción SQL siguiente:  
  
```  
SELECT * FROM Orders  
```  
  
 Si la aplicación, a continuación, ejecuta la instrucción SQL  
  
```  
SELECT * FROM Lines  
```  
  
 en el mismo identificador de instrucción, los enlaces de columna para el primer conjunto de resultados están aún en vigor porque éstos son los enlaces que se almacenan en la estructura de la instrucción. En la mayoría de los casos, esto es una mala práctica de programación y debe evitarse. En su lugar, la aplicación debe llamar a **SQLFreeStmt** con la opción SQL_UNBIND desenlazar todas las columnas anteriores y, a continuación, enlazar otros nuevos.
