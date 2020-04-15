---
title: Enlazar columnas de conjunto de resultados ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 558ceb79d42d82477b70a028395de82cc023c170
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306366"
---
# <a name="binding-result-set-columns"></a>Columnas del conjunto de resultados de enlace
Las aplicaciones pueden enlazar tantas o tan pocas columnas del conjunto de resultados como elijan, incluido el enlace sin columnas. Cuando se recupera una fila de datos, el controlador devuelve los datos de las columnas enlazadas a la aplicación. Si la aplicación enlaza todas las columnas del conjunto de resultados depende de la aplicación. Por ejemplo, las aplicaciones que generan informes suelen tener un formato fijo; estas aplicaciones crean un conjunto de resultados que contiene todas las columnas utilizadas en el informe y, a continuación, enlazan y recuperan los datos de todas estas columnas. Las aplicaciones que muestran pantallas llenas de datos a veces permiten al usuario decidir qué columnas mostrar; estas aplicaciones crean un conjunto de resultados que contiene todas las columnas que el usuario podría desear, pero enlazar y recuperar los datos solo para las columnas elegidas por el usuario.  
  
 Los datos se pueden recuperar de columnas sin enlazar llamando a **SQLGetData**. Esto se llama comúnmente para recuperar datos largos, que a menudo supera la longitud de un único búfer y se debe recuperar en partes.  
  
 Las columnas se pueden enlazar en cualquier momento, incluso después de que se hayan capturado filas. Sin embargo, los nuevos enlaces no surten efecto hasta la próxima vez que se captura una fila; no se aplican a los datos de las filas ya recuperadas.  
  
 Una variable permanece enlazada a una columna hasta que una variable diferente está enlazada a la columna, hasta que la columna se desenlaza llamando a **SQLBindCol** con un puntero nulo como dirección de la variable, hasta que todas las columnas se desenlazan mediante una llamada a **SQLFreeStmt** con la opción SQL_UNBIND o hasta que se libera la instrucción. Por este motivo, la aplicación debe estar segura de que todas las variables enlazadas siguen siendo válidas mientras estén enlazadas. Para obtener más información, consulte [Asignación y liberación de búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Dado que los enlaces de columna son solo información asociada a la estructura de instrucciones, se pueden establecer en cualquier orden. También son independientes del conjunto de resultados. Por ejemplo, supongamos que una aplicación enlaza las columnas del conjunto de resultados generado por la siguiente instrucción SQL:  
  
```  
SELECT * FROM Orders  
```  
  
 Si la aplicación, a continuación, ejecuta la instrucción SQL  
  
```  
SELECT * FROM Lines  
```  
  
 en el mismo identificador de instrucción, los enlaces de columna para el primer conjunto de resultados siguen en vigor porque esos son los enlaces almacenados en la estructura de la instrucción. En la mayoría de los casos, esta es una mala práctica de programación y debe evitarse. En su lugar, la aplicación debe llamar a **SQLFreeStmt** con la opción SQL_UNBIND para desenlazar todas las columnas antiguas y, a continuación, enlazar las nuevas.
