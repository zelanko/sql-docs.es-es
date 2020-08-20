---
description: Columnas del conjunto de resultados de enlace
title: Enlazar columnas del conjunto de resultados | Microsoft Docs
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
ms.openlocfilehash: e6a228de81deb5cdfdaa62ee7940185b14bcaef8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499948"
---
# <a name="binding-result-set-columns"></a>Columnas del conjunto de resultados de enlace
Las aplicaciones pueden enlazar tantas o tan pocas columnas del conjunto de resultados como elijan, incluido el enlace de ninguna columna. Cuando se captura una fila de datos, el controlador devuelve los datos de las columnas enlazadas a la aplicación. El hecho de que la aplicación enlace todas las columnas del conjunto de resultados depende de la aplicación. Por ejemplo, las aplicaciones que generan informes suelen tener un formato fijo. dichas aplicaciones crean un conjunto de resultados que contiene todas las columnas utilizadas en el informe y, a continuación, enlazan y recuperan los datos de todas estas columnas. Las aplicaciones que muestran pantallas llenas de datos a veces permiten al usuario decidir qué columnas se deben mostrar. estas aplicaciones crean un conjunto de resultados que contiene todas las columnas que el usuario podría querer, pero enlazan y recuperan los datos solo de las columnas elegidas por el usuario.  
  
 Los datos se pueden recuperar de las columnas sin enlazar llamando a **SQLGetData**. Normalmente, se llama a este método para recuperar datos largos, lo que a menudo supera la longitud de un búfer único y se debe recuperar en partes.  
  
 Las columnas se pueden enlazar en cualquier momento, incluso después de que se hayan capturado filas. Sin embargo, los nuevos enlaces no surtirán efecto hasta la próxima vez que se capture una fila; no se aplican a los datos de las filas que ya se han capturado.  
  
 Una variable permanece enlazada a una columna hasta que se enlaza una variable diferente a la columna, hasta que la columna quede desenlazada llamando a **SQLBindCol** con un puntero nulo como dirección de la variable, hasta que se desenlazan todas las columnas llamando a **SQLFreeStmt** con la opción SQL_UNBIND o hasta que se libere la instrucción. Por esta razón, la aplicación debe asegurarse de que todas las variables enlazadas sigan siendo válidas mientras estén enlazadas. Para obtener más información, consulte [asignación y liberación de búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Dado que los enlaces de columna son solo información asociada a la estructura de la instrucción, se pueden establecer en cualquier orden. También son independientes del conjunto de resultados. Por ejemplo, supongamos que una aplicación enlaza las columnas del conjunto de resultados generadas por la siguiente instrucción SQL:  
  
```  
SELECT * FROM Orders  
```  
  
 Si la aplicación ejecuta entonces la instrucción SQL  
  
```  
SELECT * FROM Lines  
```  
  
 en el mismo identificador de instrucción, los enlaces de columna para el primer conjunto de resultados siguen en vigor porque son los enlaces almacenados en la estructura de la instrucción. En la mayoría de los casos, se trata de una práctica de programación deficiente y debe evitarse. En su lugar, la aplicación debe llamar a **SQLFreeStmt** con la opción SQL_UNBIND para desenlazar todas las columnas antiguas y, a continuación, enlazar otras nuevas.
