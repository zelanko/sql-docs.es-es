---
description: Asignar un identificador de conexión ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6c17003ed3746f2953eb167f2dc3d944659e352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456441"
---
# <a name="allocating-a-connection-handle-odbc"></a>Asignar un identificador de conexión ODBC
Para que la aplicación pueda conectarse a un origen de datos o un controlador, debe asignar un identificador de conexión, como se indica a continuación:  
  
1.  La aplicación declara una variable de tipo SQLHDBC. A continuación, llama a **SQLAllocHandle** y pasa la dirección de esta variable, el identificador del entorno en el que se va a asignar la conexión y la opción SQL_HANDLE_DBC. Por ejemplo:  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  El administrador de controladores asigna una estructura en la que almacenar información sobre la instrucción y devuelve el identificador de conexión en la variable.  
  
 En este momento, el administrador de controladores no llama a **SQLAllocHandle** en el controlador porque no sabe a qué controlador debe llamar. Retrasa la llamada a **SQLAllocHandle** en el controlador hasta que la aplicación llama a una función para conectarse a un origen de datos. Para obtener más información, vea [rol del administrador de controladores en el proceso de conexión](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), más adelante en esta sección.  
  
 Es importante tener en cuenta que la asignación de un identificador de conexión no es lo mismo que cargar un controlador. El controlador no se carga hasta que se llama a una función de conexión. Por lo tanto, después de asignar un identificador de conexión y antes de conectarse al controlador o el origen de datos, las únicas funciones a las que puede llamar la aplicación con el identificador de conexión son **SQLSetConnectAttr**, **SQLGetConnectAttr**o **SQLGetInfo** con la opción SQL_ODBC_VER. La llamada a otras funciones con el identificador de conexión, como **SQLEndTran**, devuelve SQLSTATE 08003 (la conexión no está abierta). Para obtener detalles completos, vea el [Apéndice B: tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obtener más información sobre los identificadores de conexión, vea [identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md).
