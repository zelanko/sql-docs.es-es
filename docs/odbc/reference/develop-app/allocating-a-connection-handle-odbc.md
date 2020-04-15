---
title: Asignación de un controlador de conexión ODBC ( Connection Handle ODBC ) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12e9f65ee81612e269c1f86ebabd049588443cb8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288525"
---
# <a name="allocating-a-connection-handle-odbc"></a>Asignar un identificador de conexión ODBC
Antes de que la aplicación pueda conectarse a un origen de datos o controlador, debe asignar un identificador de conexión, como se indica a continuación:  
  
1.  La aplicación declara una variable de tipo SQLHDBC. A continuación, llama a **SQLAllocHandle** y pasa la dirección de esta variable, el identificador del entorno en el que se va a asignar la conexión y la opción SQL_HANDLE_DBC. Por ejemplo:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  El Administrador de controladores asigna una estructura en la que almacenar información sobre la instrucción y devuelve el identificador de conexión en la variable.  
  
 El Administrador de controladores no llama a **SQLAllocHandle** en el controlador en este momento porque no sabe qué controlador llamar. Retrasa la llamada a **SQLAllocHandle** en el controlador hasta que la aplicación llama a una función para conectarse a un origen de datos. Para obtener más información, consulte Rol del Administrador de [controladores en el proceso](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)de conexión , más adelante en esta sección.  
  
 Es importante tener en cuenta que la asignación de un identificador de conexión no es lo mismo que cargar un controlador. El controlador no se carga hasta que se llama a una función de conexión. Por lo tanto, después de asignar un identificador de conexión y antes de conectarse al controlador o al origen de datos, las únicas funciones a las que la aplicación puede llamar con el identificador de conexión son **SQLSetConnectAttr**, **SQLGetConnectAttr**o **SQLGetInfo** con la opción SQL_ODBC_VER. Al llamar a otras funciones con el identificador de conexión, como **SQLEndTran**, devuelve SQLSTATE 08003 (conexión no abierta). Para obtener detalles completos, consulte [Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .  
  
 Para obtener más información acerca de los identificadores de conexión, vea [Controladores de conexión](../../../odbc/reference/develop-app/connection-handles.md).
