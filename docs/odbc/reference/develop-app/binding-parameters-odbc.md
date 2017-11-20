---
title: "Enlazar parámetros ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 20879f658c1fdc2ca8a4527f76a540ab2700b98f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="binding-parameters-odbc"></a>Enlazar parámetros ODBC
Cada parámetro en una instrucción SQL debe estar asociado, o *enlazado,* a una variable en la aplicación antes de que se ejecuta la instrucción. Cuando la aplicación enlaza una variable a un parámetro, se describe esa variable: dirección, tipo de datos de C y así sucesivamente, para el controlador. También se describe el propio parámetro: datos de SQL tipo, precisión y así sucesivamente. El controlador almacena esta información en la estructura se mantiene para esa instrucción y usa la información para recuperar el valor de la variable cuando se ejecuta la instrucción.  
  
 Parámetros se pueden enlazar o Reenlazar en cualquier momento antes de que se ejecuta una instrucción. Si se vuelve a enlazar un parámetro después de ejecutar una instrucción, el enlace no se aplica hasta que la instrucción se ejecuta de nuevo. Para enlazar un parámetro a una variable distinta, una aplicación simplemente vuelve a enlazar el parámetro con la nueva variable; el enlace anterior se libera automáticamente.  
  
 Una variable estando enlazada a un parámetro hasta que se enlaza una variable diferente para el parámetro, hasta que todos los parámetros que no están enlazados mediante una llamada a **SQLFreeStmt** con la opción SQL_RESET_PARAMS o hasta que se libere la instrucción. Por este motivo, la aplicación debe asegurarse de que las variables no se liberarán hasta que cuando se encuentran sin enlazar. Para obtener más información, consulte [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Dado que los enlaces de parámetro son solo información almacenada en la estructura mantenida por el controlador de la instrucción, se pueden establecer en cualquier orden. También son independientes de la instrucción SQL que se ejecuta. Por ejemplo, suponga que una aplicación enlaza los tres parámetros y, a continuación, ejecuta la siguiente instrucción SQL:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Si la aplicación, a continuación, ejecuta de forma inmediata la instrucción SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 en el mismo identificador de instrucción, los enlaces de parámetro para la **insertar** instrucción se utilizan porque éstos son los enlaces que se almacenan en la estructura de la instrucción. En la mayoría de los casos, esto es una práctica de programación deficiente y debe evitarse. En su lugar, la aplicación debe llamar a **SQLFreeStmt** con la opción SQL_RESET_PARAMS para desenlazar todos los parámetros anteriores y, a continuación, enlazar otros nuevos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Marcadores de parámetros de enlace](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Enlazar parámetros por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Desplazamientos de enlace de parámetros](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descripciones de parámetros](../../../odbc/reference/develop-app/describing-parameters.md)

