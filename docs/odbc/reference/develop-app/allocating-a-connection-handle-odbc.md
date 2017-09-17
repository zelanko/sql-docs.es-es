---
title: "Asignar un identificador de conexión ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678ba0fa4e256402e9fc25e2e4e60ba4877c6c44
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="allocating-a-connection-handle-odbc"></a>Asignar un identificador de conexión ODBC
Antes de la aplicación puede conectarse a un origen de datos o el controlador, debe asignar un identificador de conexión, como se indica a continuación:  
  
1.  La aplicación declara una variable de tipo SQLHDBC. A continuación, se llama **SQLAllocHandle** y pasa la dirección de esta variable, el identificador del entorno en el que se va a asignar la conexión y la opción de SQL_HANDLE_DBC. Por ejemplo:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  El Administrador de controladores asigna una estructura en la que se va a almacenar la información acerca de la instrucción y devuelve el identificador de conexión en la variable.  
  
 El Administrador de controladores no llama a **SQLAllocHandle** en el controlador a la vez debido a que no sabe qué controlador debe llamar. Retrasa la llamada **SQLAllocHandle** en el controlador hasta que la aplicación llama a una función para conectarse a un origen de datos. Para obtener más información, consulte [rol del Administrador de controladores en el proceso de conexión](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), más adelante en esta sección.  
  
 Es importante tener en cuenta que asignar un identificador de conexión no es igual a cargar un controlador. El controlador no se cargará hasta que se invoque una función de conexión. Por lo tanto, después de asignar un identificador de conexión y antes de conectar con el controlador o el origen de datos, las funciones sola puede llamar la aplicación con el identificador de conexión son **SQLSetConnectAttr**, **SQLGetConnectAttr**, o **SQLGetInfo** con la opción SQL_ODBC_VER. Llamar a otras funciones con el identificador de conexión, como **SQLEndTran**, devuelve SQLSTATE 08003 (conexión no abierta). Para obtener información detallada, vea [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obtener más información acerca de los identificadores de conexión, vea [identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md).
