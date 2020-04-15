---
title: Asignación de la manija del entorno ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e33b850b2786960a368720deaf89a2203c7dd159
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303008"
---
# <a name="allocating-the-environment-handle"></a>Asignar el identificador de entorno
La primera tarea para cualquier aplicación ODBC es cargar el Administrador de controladores; cómo se hace esto depende del sistema operativo. Por ejemplo, en un equipo que ejecuta Microsoft® Windows NT® Server/Windows 2000 Server, Windows NT Workstation/Windows 2000 Professional o Microsoft Windows® 95/98, la aplicación se vincula a la biblioteca del Administrador de controladores o llama a **LoadLibrary** para cargar el archivo DLL del Administrador de controladores.  
  
 La siguiente tarea, que debe realizarse antes de que una aplicación pueda llamar a cualquier otra función ODBC, es inicializar el entorno ODBC y asignar un identificador de entorno, como se indica a continuación:  
  
1.  La aplicación declara una variable de tipo SQLHENV. A continuación, llama a **SQLAllocHandle** y pasa la dirección de esta variable y la opción SQL_HANDLE_ENV. Por ejemplo:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  El Administrador de controladores asigna una estructura en la que almacenar información sobre el entorno y devuelve el identificador de entorno en la variable.  
  
 El Administrador de controladores no llama a **SQLAllocHandle** en el controlador en este momento porque no sabe qué controlador llamar. Retrasa la llamada a **SQLAllocHandle** en el controlador hasta que la aplicación llama a una función para conectarse a un origen de datos. Para obtener más información, consulte Rol del Administrador de [controladores en el proceso](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)de conexión , más adelante en esta sección.  
  
 Cuando la aplicación ha terminado de usar ODBC, libera el identificador de entorno con **SQLFreeHandle**. Después de liberar el entorno, es un error de programación de aplicaciones para usar el identificador del entorno en una llamada a una función ODBC; hacerlo tiene consecuencias indefinidas, pero probablemente fatales.  
  
 Cuando **SQLFreeHandle** se llama, el controlador libera la estructura utilizada para almacenar información sobre el entorno. Tenga en cuenta que no se puede llamar a **SQLFreeHandle** para un identificador de entorno hasta que se hayan liberado todos los identificadores de conexión en ese identificador de entorno.  
  
 Para obtener más información sobre el identificador de entorno, vea [Controladores](../../../odbc/reference/develop-app/environment-handles.md)de entorno .
