---
title: Asignar un identificador de instrucción ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d50b0a31aed4935c805ca30620575ccff70d4a0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077197"
---
# <a name="allocating-a-statement-handle-odbc"></a>Asignar un identificador de instrucción ODBC
Antes de que la aplicación pueda ejecutar una instrucción, debe asignar un identificador de instrucción como se indica a continuación:  
  
1.  La aplicación declara una variable de tipo HSTMT. A continuación, llama a **SQLAllocHandle** y pasa la dirección de esta variable, el identificador de la conexión en la que se asigna la instrucción y la opción SQL_HANDLE_STMT. Por ejemplo:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  El administrador de controladores asigna una estructura en la que almacenar información sobre la instrucción y llama a **SQLAllocHandle** en el controlador con la opción SQL_HANDLE_STMT.  
  
3.  El controlador asigna su propia estructura en la que almacenar información sobre la instrucción y devuelve el identificador de la instrucción de controlador al administrador de controladores.  
  
4.  El administrador de controladores devuelve el identificador de la instrucción del administrador de controladores a la aplicación en la variable de aplicación.  
  
 El identificador de instrucción identifica la instrucción que se va a usar al llamar a funciones de ODBC. Para obtener más información sobre los identificadores de instrucciones, vea [identificadores de instrucciones](../../../odbc/reference/develop-app/statement-handles.md).
