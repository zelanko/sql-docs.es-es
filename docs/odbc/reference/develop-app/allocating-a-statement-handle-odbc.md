---
title: Asignación de un control de instrucción ODBC ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9a15bc4622b15afa9838327edd90383a812270
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288435"
---
# <a name="allocating-a-statement-handle-odbc"></a>Asignar un identificador de instrucción ODBC
Antes de que la aplicación pueda ejecutar una instrucción, debe asignar un identificador de instrucción de la siguiente manera:  
  
1.  La aplicación declara una variable de tipo HSTMT. A continuación, llama a **SQLAllocHandle** y pasa la dirección de esta variable, el identificador de la conexión en la que se va a asignar la instrucción y la opción SQL_HANDLE_STMT. Por ejemplo:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  El Administrador de controladores asigna una estructura en la que almacenar información sobre la instrucción y llama a **SQLAllocHandle** en el controlador con la opción SQL_HANDLE_STMT.  
  
3.  El controlador asigna su propia estructura en la que almacenar información sobre la instrucción y devuelve el identificador de instrucción de controlador al Administrador de controladores.  
  
4.  El Administrador de controladores devuelve el identificador de instrucción Administrador de controladores a la aplicación en la variable de aplicación.  
  
 El identificador de instrucción identifica qué instrucción usar al llamar a funciones ODBC. Para obtener más información acerca de los identificadores de instrucción, vea [Identificadores de instrucción](../../../odbc/reference/develop-app/statement-handles.md).
