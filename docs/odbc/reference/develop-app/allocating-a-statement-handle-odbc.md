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
manager: craigg
ms.openlocfilehash: 9524f2e6b01d2a5827dcface3159b7c52a728c59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287870"
---
# <a name="allocating-a-statement-handle-odbc"></a>Asignar un identificador de instrucción ODBC
Antes de la aplicación puede ejecutar una instrucción, debe asignar un identificador de instrucción como sigue:  
  
1.  La aplicación declara una variable de tipo HSTMT. A continuación, llama **SQLAllocHandle** y pasa la dirección de esta variable, el identificador de la conexión en el que se va a asignar la instrucción y la opción de SQL_HANDLE_STMT. Por ejemplo:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  El Administrador de controladores se asigna una estructura en la que se va a almacenar información acerca de la instrucción y llama a **SQLAllocHandle** en el controlador con la opción de SQL_HANDLE_STMT.  
  
3.  El controlador asigna su propia estructura en la que se va a almacenar información acerca de la instrucción y devuelve el identificador de instrucción del controlador para el Administrador de controladores.  
  
4.  El Administrador de controladores, se devuelve el identificador de instrucción de administrador de controladores a la aplicación en la variable de aplicación.  
  
 El identificador de instrucción identifica qué instrucción se debe usar al llamar a funciones ODBC. Para obtener más información acerca de identificadores de instrucciones, consulte [identificadores de instrucciones](../../../odbc/reference/develop-app/statement-handles.md).
