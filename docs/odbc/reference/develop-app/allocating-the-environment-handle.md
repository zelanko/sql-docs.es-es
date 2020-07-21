---
title: Asignando el identificador de entorno | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303008"
---
# <a name="allocating-the-environment-handle"></a>Asignar el identificador de entorno
La primera tarea para cualquier aplicación ODBC es cargar el administrador de controladores. la forma de hacerlo depende del sistema operativo. Por ejemplo, en un equipo que ejecuta Microsoft® Windows NT® Server/Windows 2000 Server, Windows NT Workstation/Windows 2000 Professional o Microsoft Windows® 95/98, la aplicación se vincula a la biblioteca del administrador de controladores o llama a **LoadLibrary** para cargar el archivo DLL del administrador de controladores.  
  
 La siguiente tarea, que debe realizarse antes de que una aplicación pueda llamar a cualquier otra función ODBC, es inicializar el entorno ODBC y asignar un identificador de entorno, como se indica a continuación:  
  
1.  La aplicación declara una variable de tipo SQLHENV. A continuación, llama a **SQLAllocHandle** y pasa la dirección de esta variable y la opción SQL_HANDLE_ENV. Por ejemplo:  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  El administrador de controladores asigna una estructura en la que almacenar información sobre el entorno y devuelve el identificador de entorno en la variable.  
  
 En este momento, el administrador de controladores no llama a **SQLAllocHandle** en el controlador porque no sabe a qué controlador debe llamar. Retrasa la llamada a **SQLAllocHandle** en el controlador hasta que la aplicación llama a una función para conectarse a un origen de datos. Para obtener más información, vea [rol del administrador de controladores en el proceso de conexión](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md), más adelante en esta sección.  
  
 Cuando la aplicación ha terminado de usar ODBC, libera el identificador del entorno con **SQLFreeHandle**. Después de liberar el entorno, se trata de un error de programación de la aplicación para usar el identificador del entorno en una llamada a una función ODBC. Si lo hace, tendrá consecuencias indefinidas pero probablemente graves.  
  
 Cuando se llama a **SQLFreeHandle** , el controlador libera la estructura usada para almacenar información sobre el entorno. Tenga en cuenta que no se puede llamar a **SQLFreeHandle** para un identificador de entorno hasta que se hayan liberado todos los identificadores de conexión de ese controlador de entorno.  
  
 Para obtener más información sobre el identificador de entorno, consulte [controladores de entorno](../../../odbc/reference/develop-app/environment-handles.md).
