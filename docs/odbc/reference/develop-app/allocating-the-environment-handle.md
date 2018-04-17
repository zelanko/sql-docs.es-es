---
title: Asignar el identificador de entorno | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bcbfc5e9a8be2bf1fc543e9d458658a918e40b6d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="allocating-the-environment-handle"></a>Asignar el identificador de entorno
La primera tarea para cualquier aplicación ODBC es cargar el Administrador de controladores; cómo llevarlo a cabo depende del sistema operativo. Por ejemplo, en un equipo que ejecuta Microsoft® Windows NT® Server o Windows 2000 Server, Windows NT Workstation o Windows 2000 Professional o Microsoft Windows® 95 ó 98, la aplicación o se vincula a la biblioteca del Administrador de controladores o llamadas  **LoadLibrary** para cargar la DLL del Administrador de controladores.  
  
 La tarea siguiente, que debe realizarse antes de que una aplicación puede llamar a cualquier otra función ODBC, es inicializar el entorno de ODBC y asignar un identificador de entorno, como se indica a continuación:  
  
1.  La aplicación declara una variable de tipo SQLHENV. A continuación, se llama **SQLAllocHandle** y pasa la dirección de esta variable y la opción de SQL_HANDLE_ENV. Por ejemplo:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  El Administrador de controladores asigna una estructura en la que se va a almacenar información sobre el entorno y devuelve el identificador de entorno en la variable.  
  
 El Administrador de controladores no llama a **SQLAllocHandle** en el controlador a la vez debido a que no sabe qué controlador debe llamar. Retrasa la llamada **SQLAllocHandle** en el controlador hasta que la aplicación llama a una función para conectarse a un origen de datos. Para obtener más información, consulte [rol del Administrador de controladores en el proceso de conexión](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), más adelante en esta sección.  
  
 Cuando la aplicación ha terminado de usar ODBC, libera el identificador del entorno con **SQLFreeHandle**. Tras liberar el entorno, es un error de programación de aplicaciones para usar el identificador del entorno en una llamada a una función ODBC; al hacerlo de modo que tiene consecuencias no definidas, pero probablemente irrecuperables.  
  
 Cuando **SQLFreeHandle** se llama, las versiones de controlador la estructura que se utiliza para almacenar información acerca del entorno. Tenga en cuenta que **SQLFreeHandle** no se puede llamar para un identificador de entorno hasta después de que se haya liberado todos los identificadores de conexión de ese identificador de entorno.  
  
 Para obtener más información sobre el identificador de entorno, consulte [entorno controla](../../../odbc/reference/develop-app/environment-handles.md).
