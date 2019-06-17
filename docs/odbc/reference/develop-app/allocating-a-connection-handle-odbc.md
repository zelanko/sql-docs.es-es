---
title: Asignar un identificador de conexión ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83964bf1e76eef5c7c4ba4121b0c581e8d8a406b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288316"
---
# <a name="allocating-a-connection-handle-odbc"></a>Asignar un identificador de conexión ODBC
Antes de la aplicación puede conectarse a un origen de datos o un controlador, debe asignar un identificador de conexión, como se indica a continuación:  
  
1.  La aplicación declara una variable de tipo SQLHDBC. A continuación, llama **SQLAllocHandle** y pasa la dirección de esta variable, el identificador del entorno en el que se va a asignar la conexión y la opción de SQL_HANDLE_DBC. Por ejemplo:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  El Administrador de controladores se asigna a una estructura para almacenar información acerca de la instrucción y devuelve el identificador de conexión en la variable.  
  
 El Administrador de controladores no llama a **SQLAllocHandle** en el controlador en este tiempo ya que no sabe qué controlador para llamar a. Retrasa la llamada **SQLAllocHandle** en el controlador hasta que la aplicación llama a una función para conectarse a un origen de datos. Para obtener más información, consulte [rol del Administrador de controladores en el proceso de conexión](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), más adelante en esta sección.  
  
 Es importante tener en cuenta que asignar un identificador de conexión no es igual que carga un controlador. El controlador no se cargará hasta que se invoque una función de la conexión. Por lo tanto, después de asignar un identificador de conexión y antes de conectar con el controlador o el origen de datos, las únicas funciones que puede llamar la aplicación con el identificador de conexión son **SQLSetConnectAttr**, **SQLGetConnectAttr**, o **SQLGetInfo** con la opción SQL_ODBC_VER. Llamar a otras funciones con el identificador de conexión, como **SQLEndTran**, devuelve SQLSTATE 08003 (conexión no abierta). Para obtener información detallada, consulte [Apéndice B: Las tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obtener más información acerca de los identificadores de conexión, consulte [identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md).
