---
title: Columnas del conjunto de resultados de enlace | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 107a89aeca70d7b28958c475994e3c41f417fa26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="binding-result-set-columns"></a>Columnas del conjunto de resultados de enlace
Las aplicaciones pueden enlazar como muchos o pocos como columnas del conjunto de resultados como que elijan, incluidos no enlace ninguna columna en absoluto. Cuando se captura una fila de datos, el controlador devuelve los datos de las columnas enlazadas a la aplicación. Si la aplicación enlaza todas las columnas del conjunto de resultados depende de la aplicación. Por ejemplo, las aplicaciones que generan informes suelen tengan un formato fijo; dichas aplicaciones crear un conjunto de resultados que contiene todas las columnas utilizadas en el informe y, a continuación, enlazar y recuperarán los datos de todas estas columnas. Aplicaciones que se muestran a veces pantallas llena de datos permiten al usuario decidir qué columnas desea mostrar; dichas aplicaciones crean un conjunto que contiene todas las columnas, el usuario podría desee, pero enlazar y recuperar los datos solo para las columnas seleccionadas por el usuario de resultados.  
  
 Se pueden recuperar datos de las columnas sin enlazar mediante una llamada a **SQLGetData**. Esto se denomina habitualmente para recuperar datos de tipo long, que a menudo supera la longitud de un único búfer y se deben recuperar en partes.  
  
 Las columnas pueden estar limitadas en cualquier momento, incluso después de filas se han capturado. Sin embargo, los nuevos enlaces no surtirán efecto hasta la próxima vez que se captura una fila; no se aplican a los datos de filas recuperadas ya.  
  
 Una variable estando enlazada a una columna hasta que se enlaza una variable diferente a la columna, hasta que la columna se han desenlazado mediante una llamada a **SQLBindCol** con un puntero nulo como dirección de la variable, hasta que todas las columnas que no están enlazadas mediante una llamada a **SQLFreeStmt** con la opción SQL_UNBIND o hasta que se libere la instrucción. Por este motivo, la aplicación debe asegurarse de que todas las variables enlazadas sigan siendo válidas mientras que están enlazados. Para obtener más información, consulte [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Dado que los enlaces de columna son simplemente información asociada a la estructura de la instrucción, se pueden establecer en cualquier orden. También son independientes del conjunto de resultados. Por ejemplo, suponga que una aplicación enlaza las columnas del conjunto de resultados generado por la siguiente instrucción SQL:  
  
```  
SELECT * FROM Orders  
```  
  
 Si la aplicación, a continuación, ejecuta la instrucción SQL  
  
```  
SELECT * FROM Lines  
```  
  
 en el mismo identificador de instrucción, los enlaces de columna para el primer conjunto de resultados son aún en vigor, ya que son los enlaces que se almacenan en la estructura de la instrucción. En la mayoría de los casos, esto es una práctica de programación deficiente y debe evitarse. En su lugar, la aplicación debe llamar a **SQLFreeStmt** con la opción SQL_UNBIND desenlazar todas las columnas antiguas y, a continuación, enlazar otros nuevos.
