---
title: Asignar un identificador de instrucción ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d0f2bd2da071bb690443df9d5c0bdebb5a5e1e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="allocating-a-statement-handle-odbc"></a>Asignar un identificador de instrucción ODBC
Antes de la aplicación puede ejecutar una instrucción, debe asignar un identificador de instrucción como sigue:  
  
1.  La aplicación declara una variable de tipo HSTMT. A continuación, se llama **SQLAllocHandle** y pasa la dirección de esta variable, el identificador de la conexión en la que se va a asignar la instrucción y la opción de SQL_HANDLE_STMT. Por ejemplo:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  El Administrador de controladores asigna una estructura en la que se va a almacenar información acerca de la instrucción y llama **SQLAllocHandle** en el controlador con la opción de SQL_HANDLE_STMT.  
  
3.  El controlador asigna su propia estructura en la que se va a almacenar la información acerca de la instrucción y devuelve el identificador de instrucción de controlador para el Administrador de controladores.  
  
4.  El Administrador de controladores devuelve el identificador de instrucción de administrador de controladores a la aplicación en la variable de aplicación.  
  
 El identificador de instrucción identifica qué instrucción se debe usar al llamar a funciones ODBC. Para obtener más información sobre identificadores de instrucciones, consulte [identificadores de instrucciones](../../../odbc/reference/develop-app/statement-handles.md).
