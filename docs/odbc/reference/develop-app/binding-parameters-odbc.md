---
title: Enlazar parámetros ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d62c0864678e116e30a0673bdf2625d70de0cedd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199609"
---
# <a name="binding-parameters-odbc"></a>Enlazar parámetros ODBC
Cada parámetro en una instrucción SQL debe estar asociado, o *enlazado,* a una variable en la aplicación antes de que se ejecuta la instrucción. Cuando la aplicación enlaza una variable a un parámetro, describe esa variable - dirección, tipo de datos C etc. - al controlador. También se describe el propio parámetro - tipo de datos SQL, precisión y así sucesivamente. El controlador almacena esta información en la estructura se mantiene para esa instrucción y usa la información para recuperar el valor de la variable cuando se ejecuta la instrucción.  
  
 Parámetros se pueden enlazar o Reenlazar en cualquier momento antes de que se ejecuta una instrucción. Si después de ejecutar una instrucción, se vuelve a enlazar un parámetro, el enlace no se aplica hasta que se vuelve a ejecutar la instrucción. Para enlazar un parámetro a otra variable, una aplicación simplemente vuelve a enlazar el parámetro con la nueva variable; el enlace anterior se libera automáticamente.  
  
 Una variable estando enlazada a un parámetro hasta que se enlaza una variable diferente para el parámetro, hasta que todos los parámetros se han desenlazado mediante una llamada a **SQLFreeStmt** con la opción SQL_RESET_PARAMS, o hasta que se libere la instrucción. Por este motivo, la aplicación debe asegurarse de que las variables no se liberan hasta que una vez que se independiente. Para obtener más información, consulte [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Dado que los enlaces de parámetro son solo información almacenada en la estructura mantenida por el controlador para la instrucción, se puede establecer en cualquier orden. También son independientes de la instrucción SQL que se ejecuta. Por ejemplo, imagine una aplicación enlaza tres parámetros y, a continuación, ejecuta la siguiente instrucción SQL:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Si la aplicación, a continuación, ejecuta la instrucción SQL de forma inmediata  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 en el mismo identificador de instrucción, los enlaces de parámetro para el **insertar** se utilizan la instrucción porque éstos son los enlaces que se almacenan en la estructura de la instrucción. En la mayoría de los casos, esto es una mala práctica de programación y debe evitarse. En su lugar, la aplicación debe llamar a **SQLFreeStmt** con la opción SQL_RESET_PARAMS desenlazar todos los parámetros de la antiguos y, a continuación, enlazar otros nuevos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Marcadores de parámetros de enlace](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Enlazar parámetros por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Desplazamientos de enlace de parámetros](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descripciones de parámetros](../../../odbc/reference/develop-app/describing-parameters.md)
