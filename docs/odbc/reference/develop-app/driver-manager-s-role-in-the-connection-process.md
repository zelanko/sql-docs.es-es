---
title: "El Administrador de controladores &#39; s rol en el proceso de conexión | Documentos de Microsoft"
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
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32a6629892ad9667b7d56a6bb6752c68001dddc9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager39s-role-in-the-connection-process"></a>El Administrador de controladores &#39; s rol en el proceso de conexión
Recuerde que las aplicaciones no llamar a las funciones del controlador directamente. En su lugar, que llamen a funciones de administrador de controladores con el mismo nombre y el Administrador de controladores llama a las funciones de controlador. Normalmente, esto puede ocurrir casi inmediatamente. Por ejemplo, la aplicación llama **SQLExecute** en el Administrador de controladores y después algunas comprobaciones de errores, el Administrador de controladores llama **SQLExecute** en el controlador.  
  
 El proceso de conexión es diferente. Cuando la aplicación llama **SQLAllocHandle** con las opciones de SQL_HANDLE_ENV y SQL_HANDLE_DBC, la función asigna identificadores solo en el Administrador de controladores. El Administrador de controladores no llama a esta función en el controlador porque no sabe qué controlador para llamar a. De forma similar, si la aplicación pasa el identificador de una conexión no conectada a **SQLSetConnectAttr** o **SQLGetConnectAttr**, solo el Administrador de controladores se ejecuta la función. Almacena u Obtiene el valor del atributo de su conexión de controlar y devuelve SQLSTATE 08003 (conexión no abierta) al obtener el valor de un atributo que no se ha establecido y para qué ODBC no define un valor predeterminado.  
  
 Cuando la aplicación llama **SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**, el Administrador de controladores determina qué controlador se debe usar en primer lugar. A continuación, se comprueba para determinar si un controlador está cargado actualmente en la conexión:  
  
-   Si no se carga ningún controlador en la conexión, el Administrador de controladores comprueba si se ha cargado el controlador especificado en otra conexión en el mismo entorno. Si no es así, el Administrador de controladores carga el controlador en la conexión y las llamadas **SQLAllocHandle** en el controlador con la opción de SQL_HANDLE_ENV.  
  
     El Administrador de controladores, a continuación, llama **SQLAllocHandle** o no en el controlador con la opción de SQL_HANDLE_DBC, se acaba de cargar. Si la aplicación establece los atributos de conexión, el Administrador de controladores llama **SQLSetConnectAttr** en el controlador; si se produce un error, función de conexión del Administrador de controladores devuelve SQLSTATE IM006 (del controlador ** SQLSetConnectAttr** error). Por último, el Administrador de controladores llama a la función de conexión en el controlador.  
  
-   Si se carga el controlador especificado en la conexión, el Administrador de controladores llama a la función de conexión en el controlador. En este caso, el controlador debe asegurarse de que todos los atributos de conexión en la conexión conserven su configuración actual.  
  
-   Si se carga un controlador diferente en la conexión, el Administrador de controladores llama **SQLFreeHandle** en el controlador para liberar la conexión. Si no hay ninguna otra conexión que usan el controlador, el Administrador de controladores llama **SQLFreeHandle** en el controlador para liberar el entorno y descarga el controlador. El Administrador de controladores, a continuación, realiza las mismas operaciones que cuando un controlador no está cargado en la conexión.  
  
 El Administrador de controladores se bloqueará el identificador de entorno (*henv*) antes de llamar a un controlador **SQLAllocHandle** y **SQLFreeHandle** cuando *HandleType* se establece en **SQL_HANDLE_DBC**.  
  
 Cuando la aplicación llama **SQLDisconnect**, las llamadas de administrador de controladores **SQLDisconnect** en el controlador. Sin embargo, deja el controlador que se carga en caso de que la aplicación se vuelve a conectar el controlador. Cuando la aplicación llama **SQLFreeHandle** con la opción de SQL_HANDLE_DBC, el Administrador de controladores llama **SQLFreeHandle** en el controlador. Si el controlador no se usa ninguna otra conexión, el Administrador de controladores, a continuación, llama **SQLFreeHandle** en el controlador con el SQL_HANDLE_ENV opción y descarga el controlador.
