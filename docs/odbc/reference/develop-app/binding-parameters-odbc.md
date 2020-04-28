---
title: Parámetros de enlace ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306386"
---
# <a name="binding-parameters-odbc"></a>Enlazar parámetros ODBC
Cada parámetro de una instrucción SQL debe estar asociado, o *enlazado,* a una variable de la aplicación antes de que se ejecute la instrucción. Cuando la aplicación enlaza una variable a un parámetro, describe ese tipo de datos de dirección variable y C, entre otros, en el controlador. También se describe el parámetro, el tipo de datos SQL, la precisión, etc. El controlador almacena esta información en la estructura que mantiene para esa instrucción y usa la información para recuperar el valor de la variable cuando se ejecuta la instrucción.  
  
 Los parámetros se pueden enlazar o reenlazar en cualquier momento antes de ejecutar una instrucción. Si un parámetro se vuelve a enlazar después de ejecutar una instrucción, el enlace no se aplica hasta que la instrucción se vuelva a ejecutar. Para enlazar un parámetro a una variable diferente, una aplicación simplemente vuelve a enlazar el parámetro con la nueva variable; el enlace anterior se libera automáticamente.  
  
 Una variable permanece enlazada a un parámetro hasta que se enlaza una variable diferente al parámetro, hasta que todos los parámetros se desenlazan llamando a **SQLFreeStmt** con la opción SQL_RESET_PARAMS o hasta que se libera la instrucción. Por esta razón, la aplicación debe asegurarse de que las variables no se liberen hasta que no se hayan desenlazado. Para obtener más información, consulte [asignación y liberación de búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Dado que los enlaces de parámetros son solo información almacenada en la estructura mantenida por el controlador para la instrucción, se pueden establecer en cualquier orden. También son independientes de la instrucción SQL que se ejecuta. Por ejemplo, supongamos que una aplicación enlaza tres parámetros y, a continuación, ejecuta la siguiente instrucción SQL:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Si la aplicación ejecuta inmediatamente la instrucción SQL  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 en el mismo identificador de instrucción, se usan los enlaces de parámetro para la instrucción **Insert** , ya que son los enlaces almacenados en la estructura de la instrucción. En la mayoría de los casos, se trata de una práctica de programación deficiente y debe evitarse. En su lugar, la aplicación debe llamar a **SQLFreeStmt** con la opción SQL_RESET_PARAMS para desenlazar todos los parámetros anteriores y, a continuación, enlazar otros nuevos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Marcadores de parámetros de enlace](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Enlazar parámetros por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Desplazamientos de enlace de parámetros](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Descripciones de parámetros](../../../odbc/reference/develop-app/describing-parameters.md)
