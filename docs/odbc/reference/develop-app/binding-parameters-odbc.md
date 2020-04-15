---
title: Parámetros de enlace ODBC ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e314bb9e3a1a979976a450e2a45a286ec54dfe7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306386"
---
# <a name="binding-parameters-odbc"></a>Enlazar parámetros ODBC
Cada parámetro de una instrucción SQL debe estar asociado o *enlazado* a una variable de la aplicación antes de ejecutar la instrucción. Cuando la aplicación enlaza una variable a un parámetro, describe esa variable - dirección, tipo de datos C, etc. - al controlador. También describe el propio parámetro: tipo de datos SQL, precisión, etc. El controlador almacena esta información en la estructura que mantiene para esa instrucción y utiliza la información para recuperar el valor de la variable cuando se ejecuta la instrucción.  
  
 Los parámetros se pueden enlazar o rebotar en cualquier momento antes de que se ejecute una instrucción. Si se vuelve a enlazar un parámetro después de ejecutar una instrucción, el enlace no se aplica hasta que se vuelve a ejecutar la instrucción. Para enlazar un parámetro a una variable diferente, una aplicación simplemente vuelve a enlazar el parámetro con la nueva variable; el enlace anterior se libera automáticamente.  
  
 Una variable permanece enlazada a un parámetro hasta que una variable diferente está enlazada al parámetro, hasta que todos los parámetros se desenlazan llamando a **SQLFreeStmt** con la opción SQL_RESET_PARAMS o hasta que se libera la instrucción. Por este motivo, la aplicación debe estar segura de que las variables no se liberan hasta después de que se desenlazan. Para obtener más información, consulte [Asignación y liberación de búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Dado que los enlaces de parámetros son solo información almacenada en la estructura mantenida por el controlador para la instrucción, se pueden establecer en cualquier orden. También son independientes de la instrucción SQL que se ejecuta. Por ejemplo, supongamos que una aplicación enlaza tres parámetros y, a continuación, ejecuta la siguiente instrucción SQL:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Si la aplicación, a continuación, ejecuta inmediatamente la instrucción SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 En el mismo identificador de instrucción, los enlaces de parámetro para la instrucción **INSERT** se usan porque son los enlaces almacenados en la estructura de la instrucción. En la mayoría de los casos, esta es una mala práctica de programación y debe evitarse. En su lugar, la aplicación debe llamar a **SQLFreeStmt** con la opción SQL_RESET_PARAMS para desenlazar todos los parámetros antiguos y, a continuación, enlazar los nuevos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Marcadores de parámetros de enlace](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Enlazar parámetros por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Desplazamientos de enlace de parámetros](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descripciones de parámetros](../../../odbc/reference/develop-app/describing-parameters.md)
